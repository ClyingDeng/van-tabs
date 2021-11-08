<template>
<van-popup
  v-model="isSortNav"
  round
  position="bottom"
  :style="{ height: '70%' }"
  :overlay-style="{ opacity: 0.5 }"
  :close-on-click-overlay="false"
  @click-overlay="noSortNav"
>
  <div class="sortContent">
      <div class="packUp">
        <img src="@/assets/arrowDown.png" alt="" />
      </div>
      <div class="dataTittle">
        <div>全部数据项</div>
        <div class="rightTittle">长按右侧拖拽可排序</div>
      </div>
      <div class="dataOption">
        <vue-draggable
          :list="list"
          class="list-group"
          ghost-class="ghost"
          @start="dragging = true"
          @end="dragging = false"
        >
          <div v-for="item in list" :key="item.name" class="list-group-item">
            <div class="list-item-left">
              <div class="list-item-icon">
                <img :src="require('@/assets/drag/' + item.name + '.png')" alt="" />
              </div>
              <div class="list-item-title">
                {{ item.title }}
              </div>
              <div class="list-item-annotation">
                {{ item.annotation }}
              </div>
            </div>
            <div class="list-item-drag">
              <van-icon name="wap-nav" />
            </div>
          </div>
        </vue-draggable>
      </div>
  </div>
</van-popup>
</template>

<script>
import VueDraggable from 'vuedraggable'
export default {
  name: 'sortNav',
  components: {
    VueDraggable,
  },
  props: {
    list: {
      type: Array,
      default: () => [],
    },
    isSortNav: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {}
  },
  mounted() {
    console.log('父组件传入', this.isSortNav, this.list)
  },
  methods: {
noSortNav() {
  this.$emit('noSortshow', !this.isSortNav)
  this.$emit('newList', this.list)
},
  },
}
</script>

<style lang="scss" scoped>
.sortContent {
  padding: 8px;
  .packUp {
    align-items: center;
    display: flex;
    height: 20px;
    justify-content: center;
    .img {
      width: 22px;
    }
  }
  .dataTittle {
    color: rgb(128, 128, 128);
    display: flex;
    font-size: 12px;
    justify-content: space-between;
    .rightTittle {
      color: rgb(170, 170, 170);
    }
  }
  .dataOption {
    height: 390px;
    margin-top: 16px;
    overflow-y: scroll;
    .list-group {
      .list-group-item {
        align-items: center;
        background: rgb(249, 250, 251);
        border-radius: 6px;
        display: flex;
        height: 50px;
        justify-content: space-between;
        margin-top: 8px;
        padding-left: 17px;
        padding-right: 20px;
      }
      .list-item-left {
        align-items: center;
        display: flex;
        .list-item-icon {
          height: 17px;
          width: 17px;
          img {
            height: 17px;
            width: 17px;
          }
        }
        .list-item-title {
          color: rgb(51, 51, 51);
          font-weight: 500;
          margin-left: 8px;
        }
      }
      .list-item-annotation {
        color: rgb(170, 170, 170);
        font-size: 12px;
        margin-left: 18px;
      }
      .list-item-drag {
        height: 15px;
        width: 15px;
      }
    }
  }
}
</style>
