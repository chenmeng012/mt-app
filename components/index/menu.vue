<template>
  <div class="m-menu">
    <dl class="nav" @mouseleave="menuLeave">
      <dt>全部菜单</dt>
      <dd v-for="(item, index) in menu" :key="index" @mouseenter="menuEnter">
        <i :class="item.type"></i>{{item.name}}<span class="arrow"></span>
      </dd>
    </dl>
    <div class="detail" v-if="kind" @mouseenter="detailEnter" @mouseleave="detailLeave">
      <template v-for="(item, index) in currDetail.child">
        <h4 :key="index">{{item.title}}</h4>
        <span v-for="(vitem, vindex) in item.child" :key="vitem">{{vitem}}</span>
      </template>
    </div>
  </div>
</template>

<script>
export default {
  name: 'my-menu',
  data() {
    return {
      _timer: null,
      kind: '',
      menu: [
        {
          type: 'food',
          name: '美食',
          child: [
            {
              title: '美食',
              child: ['代金券','甜点饮品','火锅','自助餐','小吃快餐']
            }
          ]
        }, {
          type: 'takeout',
          name: '外卖',
          child: [
            {
              title: '外卖',
              child: ['美团外卖']
            }
          ]
        }, {
          type: 'hotel',
          name: '酒店',
          child: [
            {
              title: '酒店',
              child: ['经济型','舒适/三星','高档/四星','豪华/五星']
            }
          ]
        },
      ]
    }
  },
  computed: {
    currDetail() {
      let menu = this.menu.filter((item) => {
        return item.type === this.kind
      });
      return menu.length>0? menu[0] : {}
    }
  },
  methods: {
    menuLeave() {
      this._timer = setTimeout(() => {
        this.kind = '';
      }, 150)
    },
    menuEnter(e) {
      this.kind = e.target.querySelector('i').className
    },
    detailEnter() {
      clearTimeout(this._timer);
    },
    detailLeave() {
      this.kind = '';
    }
  }
}
</script>

<style scoped>

</style>
