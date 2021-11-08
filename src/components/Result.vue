<template>
  <div id="app">
    <!-- <div v-for="item in navList" :key="item.name">{{ item }}</div> -->
    <div class="nav">
      <div class="selectSort" @click="showSort">
        <van-icon name="wap-nav" size="28" />
      </div>
      <van-tabs
        v-model="active"
        swipe-threshold="4"
        class="tab"
        title-active-color="#3693FF"
        color="#3693FF"
        title-inactive-color="#4A4A4A"
        @click-tab="chooseNav"
      >
        <van-tab
          v-for="(item, index) in navList"
          :key="index"
          :name="item.name"
          :title="item.title"
        >
          <component :is="item.component" class="tabPanel"></component>
        </van-tab>
      </van-tabs>
    </div>
    <sort-nav
      :isSortNav="isSortNav"
      :list="navListClone"
      @newList="newList"
      @noSortshow="noSortshow"
    ></sort-nav>
  </div>
</template>

<script>
import SortNav from './SortNav.vue'
import { cloneDeep } from 'lodash'
export default {
  name: 'App',
  components: {
    SortNav,
  },
  data() {
    return {
      navList: [
        {
          title: '导航1',
          name: 'affairs',
          component: () => import('./views/First.vue'),
        },
        {
          title: '导航2',
          name: 'collect',
          component: () => import('./views/Second.vue'),
        },
        {
          title: '导航3',
          name: 'dispatch',
          component: () => import('./views/Third.vue'),
        },
        {
          title: '其他导航目录',
          name: 'fine',
          component: () => import('./views/HelloWorld.vue'),
        },
      ],
      navListClone: [],
      isSortNav: false,
      active: '',
      index: 1,
    }
  },
  created() {
    this.active = 'affairs'
    this.navListClone = cloneDeep(this.navList)
  },
  methods: {
    // 法一：通过nextTick，重新更改绑定的值
    // newList(val) {
    //   this.navList = []
    //   this.$nextTick(() => {
    //     this.navList = val
    //     console.log(this.active)
    //   })
    // },
    // 法二：van-tabs 绑定:key="index"。通过修改key值触发更新
    // newList(val) {
    //   this.navList = val
    //   this.index++
    // },
    // 法三：通过tab的key值绑定index
    newList(val) {
      this.navList = val
    },
    noSortshow(val) {
      console.log('子组件触发，拖拽弹框关闭状态', val)
      this.isSortNav = val
    },
    chooseNav(item) {
      this.active = item
    },
    showSort() {
      this.isSortNav = true
    },
  },
}
</script>

<style lang="scss" scoped>
.content {
  height: 100vh;
  width: 100wh;
  background: red;
}
.nav {
  background: rgba(246, 247, 249, 1);
  display: flex;
  flex-direction: column;
  height: calc(100% - 50px);
  left: 0;
  position: relative;
  right: 0;
  .title {
    color: rgb(51, 51, 51);
    font-size: 18px;
    font-weight: bold;
    line-height: 40px;
  }
  .selectSort {
    align-items: center;
    color: rgb(74, 74, 74);
    background: #fff;
    display: flex;
    height: 45px;
    width: 45px;
    justify-content: center;
    // float: right;
    position: fixed;
    right: 0;
    z-index: 2;
  }
  .tabPanel {
    height: 100%;
    // background: blue;
  }
}
::v-deep .van-tabs__wrap {
  width: calc(100vw - 45px);
}
</style>
