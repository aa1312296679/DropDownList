<template>
  <div class="listWrapper" @click="onListWrapperClick" ref="listWrapper" style="overflow: hidden">
    <span>{{selectedItemTxt}}</span>
    <ul :class="listState" >
       <li v-for="(item, index) in dataList" :key="index" @click="onLiClick(index, $event)">{{item['name']}}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'DropDownList',
  data () {
    return {
      listShow: false, // 显示状态
      activeIndex: 0 // 已选中的列表项索引
    }
  },
  props: {
    dataList: { // 列表信息
      type: Array,
      default () {
        return []
      }
    }
  },
  mounted () {
    this.onListWrapper(this.listShow)
  },
  methods: {
    /**
     * 列表容器点击事件
     * */
    onListWrapperClick () {
      this.listShow = !this.listShow
      this.onListWrapper(this.listShow)
    },
    /**
     * 列表项点击事件
     * @param index 被点击的列表项索引
     * */
    onLiClick (index) {
      this.activeIndex = index
      this.$emit('change', {
        index: index,
        value: this.dataList[index]
      })
    },
    /**
     * 列表容器所显示内容的溢出处理
     * @param listWrapper 溢出状态 true隐藏溢出元素,false为显示溢出元素
     */
    onListWrapper (listWrapper) {
      setTimeout(() => {
        (listWrapper) ? (this.$refs['listWrapper'].style.overflow = '') : (this.$refs['listWrapper'].style.overflow = 'hidden')
      }, 200)
    }
  },
  computed: {
    /**
     * 获取选中的列表项信息
     * @returns {String} 被选择的列表项信息
     */
    selectedItemTxt () {
      return this.dataList[this.activeIndex]['name']
    },
    /**
     * 更新列表项的显示状态
     * @returns {string} 显示状态
     */
    listState () {
      return this.listShow ? 'list_show' : 'list_hide'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  .listWrapper{
    display: inline-block;
    min-width: 100px;
    position: relative;
    span{
      display: block;
      height: 30px;
      line-height: 30px;
      background: #f1f1f1;
      font-size: 14px;
      text-align: center;
      color: #333333;
      border-radius: 4px;
      border: 1px solid red;
    }

    .list_show{
      transition:all 0.5s;
      transform:translateX(0) translateY(0px);
    }
    .list_hide{
      transition:all 0.5s;
      transform:translateX(0) translateY(-62px);
    }

    ul{
      z-index: -1;
      position: absolute;
      left: 0;
      width: 100%;
      margin: 0;
      padding: 0;
      border: solid 1px #f1f1f1;
      border-radius: 4px;
      overflow: hidden;
      li{
        list-style: none;
        height: 30px;
        line-height: 30px;
        font-size: 14px;
        border-bottom: solid 1px #f1f1f1;
        background: #ffffff;
      }
      li:last-child{
        border-bottom: none;
      }
      li:hover{
        background: #f6f6f6;
      }
    }
  }
</style>
