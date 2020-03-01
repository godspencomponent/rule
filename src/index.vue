<template>
  <div class="component" :class='["style"+type]'>
    <div class="rule-wrap" v-for='(v, i) in list' :key='i'>
      <div class="no" :class='color' :style='colorSty'>{{i + 1 | noFil(type)}}</div>
      <div v-html='v'></div>
    </div>
  </div>
</template>

<script>
  import {VueExtend} from 'godspen-lib'
  function insertRule (sheet, selectorText, cssText, position) {
    try {
      if (sheet.cssRules[0].selectorText == selectorText) {
        sheet.removeRule(0)
      }
    } catch (e) {}
    if (sheet.insertRule) {
      sheet.insertRule(selectorText + '{' + cssText + '}', position)
    } else if (sheet.addRule) {
      sheet.addRule(selectorText, cssText, position)
    }
  }
  export default {
    mixins: [VueExtend.mixin],
    name: 'rule',
    label: process.env.LABEL,
    style: process.env.STYLE,
    props: {
      type: {
        type: [String, Number],
        default: 4
      },
      list: {
        type: Array,
        editor: {
          ignore: true
        },
        default () {
          return [
            '码良是一个在线生成h5页面并提供页面管理和页面编辑的平台，用于快速制作H5页面',
            '码良是一个在线生成h5页面并提供页面管理和页面编辑的平台，用于快速制作H5页面'
          ]
        }
      },
      color: {
        type: String,
        default: '#6260e1'
      }
    },
    computed: {
      colorSty () {
        if (this.type == 1) {
          this.$nextTick(() => {
            insertRule(document.styleSheets[0], '.no::after', `background-color: ${this.color || '#6260e1'} !important`)
          })
          return {}
        }
        if (this.type == 2) {
          return {
            color: this.color || '#6260e1'
          }
        }
        return {
          backgroundColor: this.color || '#6260e1'
        }
      }
    },
    editorMethods: {
    },
    watch: {
      color: {
        handler (val) {
          if (this.type == 1) {
            insertRule(document.styleSheets[0], '.no::after', `background-color: ${val || '#6260e1'} !important`)
          }
        },
        immediate: true
      }
    },
    filters: {
      noFil (val, type) {
        let no = val
        if (typeof val == 'number') {
          switch (+type) {
            case 1:
            case 3:
              no = val.toString().padStart(2, '0')
              break
            case 2:
              no = `${no}.`
              break
          }
        }
        return no
      }
    },
    methods: {
    }
  }
</script>
<style lang="stylus" rel="stylesheet/stylus" type="text/stylus" scoped>
  .component {
    width 100%
    .rule-wrap{
      position relative
      margin-bottom 10px
      padding-left 30px
      font-size 14px
      line-height 1.6
      color #333
      .no{
        position absolute
        left 0
        top 0
      }
    }
    &.style1{
      .no{
        &::after{
          content: "";
          position: absolute
          bottom: 3px
          left: 0
          width: 100%
          height: 3px
          background-color: #6260e1
        }
      }
    }
    &.style2{
      .no{
        color #6260e1
      }
    }
    &.style3{
      .no{
        line-height 1.3
        font-size 12px
        padding 1px 4px 0px
        border-radius: 2px
        color: #fff
        background-color: #6260e1
        top 3px
      }
    }
    &.style4{
      .no{
        font-size 12px
        height 18px
        width 18px
        text-align center
        border-radius: 10px
        color: #fff
        background-color: #6260e1
        top 2px
      }
    }
  }
</style>
