<template>
  <div class="component-editor">
    <div>
      <span>标签样式：</span>
      <div class='list-type' @click='componentInfo.type = "1"'>
        <img src="https://ymm-maliang.oss-cn-hangzhou.aliyuncs.com/ymm-maliang/access/ymm_1564628917346.jpg" alt="样式1" />
        <i class="el-icon-circle-check" v-if='componentInfo.type == "1"'></i>
      </div>
      <div class='list-type' @click='componentInfo.type = "2"'>
        <img src="https://ymm-maliang.oss-cn-hangzhou.aliyuncs.com/ymm-maliang/access/ymm_1564628934471.jpg" alt="样式2" />
        <i class="el-icon-circle-check" v-if='componentInfo.type == "2"'></i>
      </div>
      <div class='list-type' @click='componentInfo.type = "3"'>
        <img src="https://ymm-maliang.oss-cn-hangzhou.aliyuncs.com/ymm-maliang/access/ymm_1564628948949.jpg" alt="样式3" />
        <i class="el-icon-circle-check" v-if='componentInfo.type == "3"'></i>
      </div>
      <div class='list-type' @click='componentInfo.type = "4"'>
        <img src="https://ymm-maliang.oss-cn-hangzhou.aliyuncs.com/ymm-maliang/access/ymm_1564628973103.jpg" alt="样式3" />
        <i class="el-icon-circle-check" v-if='componentInfo.type == "4"'></i>
      </div>
    </div>
    <div style='margin: 5px 0'>
      <span>颜色：</span>
      <el-color-picker v-model="componentInfo.color" show-alpha size="mini"></el-color-picker>
      <span>{{componentInfo.color}}</span>
    </div>
    <el-card class="box-card">
      <div slot="header" class="clearfix">
        <span>规则</span>
        <el-button style="float: right; padding: 3px 0" type="text" @click='addItem'>新增一列</el-button>
      </div>
      <div>
        <el-collapse>
          <el-collapse-item :name="i" v-for='(v, i) in componentInfo.list' :key='i'>
            <template slot="title">
              {{i+1}}<i class="el-icon-delete el-collapse-item__arrow del-item" @click.stop='delItem(i)'></i>
            </template>
            <attr-richtext :id='"rule"+i' v-model='componentInfo.list[i]'></attr-richtext>
          </el-collapse-item>
        </el-collapse>
      </div>
    </el-card>
  </div>
</template>

<script>
  export default {
    name: 'maliangeditor',
    props: {
      componentInfo: { // 固定字段，收集所有属性值
        type: [Object],
        default () {
          return {
            type: '1',
            list: [],
            color: '#6260e1'
          }
        }
      }
    },
    data: function () {
      return {
      }
    },
    computed: {
    },
    watch: {
      componentInfo: {
        hanlder: function (v) {
          console.log('editor index', v)
        },
      }
    },
    mounted: function () {
    },
    methods: {
      addItem () {
        this.componentInfo.list.push('码良是一个在线生成h5页面并提供页面管理和页面编辑的平台，用于快速制作H5页面')
      },
      delItem (i) {
        this.componentInfo.list.splice(i, 1)
      }
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus" type="text/stylus" scoped>
  .component-editor {
    .list-type{
      margin-top 10px
      width 100px
      position relative
      border-radius 5px
      display inline-block
      img{
        width 100%
      }
      i {
        position absolute
        right 0px
        bottom 0
        font-size 22px
        color #409EFF
      }
    }
    .del-item{
      color #F56C6C
      margin-right 15px
      display none
    }
    .el-collapse-item{
      &:hover{
        .del-item{
          display block
        }
      }
    }
    .tag{
      padding-right 80px
      position relative
      margin-bottom 5px
      .el-color-picker{
        position absolute
        right 30px
        top 0
      }
      i {
        display none
        position absolute
        right 0
        top 5px
        color #F56C6C
        cursor: pointer
      }
      &:hover {
        i {
          display block
        }
      }
    }
  }
</style>