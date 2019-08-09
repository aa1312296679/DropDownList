<template>
  <div class="home">
    <!--<img alt="Vue logo" src="../assets/logo.png">-->
    <DropDownList :dataList="listItems"/>
  </div>
</template>

<script>

import DropDownList from '@/components/DropDownList.vue'

export default {
  name: 'home',
  data () {
    return {
      listItems: [{ name: '选项一' }, { name: '选项二' }, { name: '选项三' }]
    }
  },
  components: {
    DropDownList
  }
}
</script>
