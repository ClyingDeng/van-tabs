<template>
  <div id="app">
    <div v-for="item in navList" :key="item.name">{{ item }}</div>
    <van-tabs
      v-model="active"
      swipe-threshold="4"
      class="tab"
      title-active-color="#3693FF"
      color="#3693FF"
      title-inactive-color="#4A4A4A"
    >
      <van-tab
        v-for="item in navList"
        :key="item.name"
        :name="item.name"
        :title="item.title"
      ></van-tab>
    </van-tabs>
  </div>
</template>
<script>
export default {
  name: 'App',
  data() {
    return {
      navList: [
        {
          title: '导航1',
          name: 'affairs',
        },
        {
          title: '导航2',
          name: 'collect',
        },
        {
          title: '导航3',
          name: 'dispatch',
        },
        {
          title: '其他导航目录',
          name: 'fine',
        },
      ],
      active: '',
      index: 1,
    }
  },
  mounted() {
    this.active = 'affairs'
    setTimeout(() => {
      this.navList = [
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
          title: '导航1',
          name: 'affairs',
          component: () => import('./views/First.vue'),
        },
        {
          title: '其他导航目录',
          name: 'fine',
          component: () => import('./views/HelloWorld.vue'),
        },
      ]
    }, 2000)
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
