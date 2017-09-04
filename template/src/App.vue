<template>
  <div id="app">
    <vm-preview
      :image="image"
      :orders="orders"
    ></vm-preview>

    <van-cell-group class="item-list">
      <van-cell isLink>
        <van-icon name="points" class="orders-icon"></van-icon>
        我的积分
      </van-cell>
      <van-cell isLink>
        <van-icon name="gift" class="orders-icon"></van-icon>
        我收到的礼物
      </van-cell>
    </van-cell-group>
  </div>
</template>

<script>
import { Cell, CellGroup, Icon } from 'vant';
import 'vant/lib/vant-css/reset.css';
import Preview from './components/preview.vue';

export default {
  components: {
    [Cell.name]: Cell,
    [CellGroup.name]: CellGroup,
    [Icon.name]: Icon,
    'vm-preview': Preview
  },

  data() {
    return {
      image: 'https://img.yzcdn.cn/upload_files/2017/07/19/Fml_7Kkd2H6pLolssY8bqoAPwyU5.png',
      orders: {
        topay: 0,
        toaccept: 0,
        tosend: 6,
        send: 0
      }
    };
  }
};
</script>

<style>
.orders-icon {
  margin-right: 5px;
  font-size: 20px;
}
.item-list {
  margin-top: 10px;
}
</style>
