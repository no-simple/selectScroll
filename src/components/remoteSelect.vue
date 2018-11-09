<template>
  <div class="remote">
    <h5>数据长度：{{list.length}}</h5>
    <el-select class="remoteSelect" v-scroll="handleScroll" v-model="value">
      <el-option :value="item.id" v-for="item in list" :key="item.id">{{item.name}}</el-option>
    </el-select>
  </div>
</template>

<script type="text/ecmascript-6">
export default {
  data () {
    return {
      pageIndex: 1, // 分页中请求的页面
      value: '', // select绑定的实体
      list: [] // 下列列表的数据，接口获取
    }
  },
  methods: {
    /*********************************
      ** Fn: handleScroll
      ** Intro: 处理滚动行为
      ** @params: param 为true代表向下滚动
      ** @params: param 为false代表向上滚动
    *********************************/
    handleScroll (param) {
      if (param) {
        // 请求下一页的数据
        this.list.push(...this.ajaxData(++this.pageIndex))
      }
    },
    /*********************************
      ** Fn: ajaxData
      ** Intro: 模拟ajax请求数据,每次返回100条数据
      ** @params:  pageIndex 代表请求的页码
      ** Author: zyx
    *********************************/
    ajaxData (pageIndex) {
      // 每页数量
      let pageSize = 100
      let list = []
      for (let i = pageSize * (pageIndex - 1); i < pageSize * pageIndex; i++) {
        list.push({
          name: `这是一条测试数据 代号：${i}`,
          id: i
        })
      }
      return list
    }
  },
  created () {
    // 模拟ajax请求，初始加载第一页数据
    this.list = this.ajaxData(this.pageIndex)
  }
}
</script>
<style lang='stylus' rel='stylesheet/stylus'>
  .remote
      text-align center
</style>
