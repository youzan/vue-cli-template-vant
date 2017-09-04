<template>
<div>
  <div class="preview">
    <img :src="image" class="preview__image">
  </div>

  <van-row class="orders-preview">
    <van-col v-for="(item, index) in ordersData" span="6" :key="index">
      <a :href="item.type | getOrderLink">
        <p class="orders-preview__icon-container">
          <van-icon :name="item.icon" class="orders-preview__icon"></van-icon>
          <span v-if="item.num > 0" class="orders-preview__count" v-text="item.num"></span>
        </p>
        <p class="orders-preview__title">
          {{ item.title }}
        </p>
      </a>
    </van-col>
  </van-row>

  <van-cell-group>
    <van-cell isLink :url="'' | getOrderLink">
      <van-icon name="records" class="orders-icon"></van-icon>
      全部订单
    </van-cell>
  </van-cell-group>
</div>
</template>

<script>
import { Cell, CellGroup, Icon, Col, Row } from 'vant';
import each from 'lodash/each';
import orderShowConfig from '../config/orders-show-config';

export default {
  components: {
    [Cell.name]: Cell,
    [CellGroup.name]: CellGroup,
    [Icon.name]: Icon,
    [Col.name]: Col,
    [Row.name]: Row
  },

  props: {
    image: String,
    orders: Object
  },

  computed: {
    ordersData() {
      const ordersData = [];
      each(this.orders, (num, status) => {
        const showConfig = orderShowConfig[status] || {};
        const itemData = {
          icon: showConfig.icon || '',
          title: showConfig.title || '',
          num,
          type: status
        };

        ordersData.push(itemData);
      });

      return ordersData;
    }
  },

  filters: {
    getOrderLink(type) {
      return `/h5/trade/order/list?type=${type || 'all'}`;
    }
  }
};
</script>

<style>
.preview {
  text-align: center;
}

.preview__image {
  width: 100%;
  min-height: 200px;
}

.orders-preview {
  padding: 10px 0;
  background: white;
  text-align: center;
}
.orders-preview__icon-container {
  position: relative;
}
.orders-preview__icon {
  padding: 20px 0 10px;
  font-size: 24px;
  color: #333;
}
.orders-preview__title {
  padding-bottom: 10px;
  line-height: 1.4;
  font-size: 12px;
  color: #333;
}
.orders-preview__count {
  position: absolute;
  top: 15px;
  left: 50%;
  padding: 3px 6px;
  background: red;
  transform: translate3d(5px, 0, 0);
  border-radius: 100%;
  color: white;
  font-size: 12px;
  text-align: center;
}
</style>
