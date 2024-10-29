<template>
  <div class="home">
    <virtual-list
      scrollable
      :page-mode="true"
      :data-key="'uid'"
      ref="virtual"
      :data-component="EmptyComponent"
      :data-sources="items"
    >
      <template #item="{ index, item }">
        <div class="_item" @click="jump">
          <div class="index">{{ index }}</div>
          <div class="left-pic">
            <img :src="item.img" alt="" />
          </div>
          <div class="right-info">
            <span>姓名：{{ item.name }}</span>
            <span>描述：{{ item.des }}</span>
            <span>标题：{{ item.title }}</span>
            <span>时间：{{ item.time }}</span>
          </div>
        </div>
      </template>
    </virtual-list>
  </div>
</template>

<script>
import HelloWorld from "@/components/HelloWorld.vue";
import VirtualList from "vue-virtual-scroll-list";
export default {
  name: "home",
  data() {
    return {
      items: [],
      EmptyComponent: {},
      scrollTop: 0,
      fromPath:''
    };
  },
  components: {
    HelloWorld,
    components: { "virtual-list": VirtualList },
  },
  activated() {
    if(this.fromPath == '/about'){
      this.$refs.virtual.reset();
      this.$refs.virtual.scrollToOffset(this.scrollTop);
    }else{
      this.getData();
    }
  },
  created() {
    
  },
  methods: {
    getData() {
      for (let i = 0; i < 1000; i++) {
        this.items.push({
          uid: i,
          name: Math.random(),
          text: "hhhhhh",
          des: "描述",
          title: "标题",
          img: "https://thirdqq.qlogo.cn/ek_qqapp/AQE9ReDTODxicvQOEMSV8kZ1E9BxQt0FPnXSpDnK5AoQaZKKw4MiaVumgP90RS5A77n119EN3l/100",
          time: "2024/12/10",
        });
      }
    },
    jump() {
      this.$router.push({ path: "/about" });
    },
  },
  beforeRouteLeave(to, from, next) {
    try {
      this.scrollTop = this.$refs.virtual.getOffset();
      next();
    } catch (error) {
      next();
    }
  },
  beforeRouteEnter(to, from, next) {
    next((vm) => {
      vm.fromPath = from.path;
    });
  },
};
</script>
<style lang="less">
._item {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  border-bottom: 1px solid rgb(187, 167, 167);
  position: relative;
  .index {
    color: red;
    font-size: 20px;
    position: absolute;
    right: 0;
    top: 0;
  }
  .left-pic {
    width: 100px;
    img {
      width: 100%;
    }
  }
  .right-info {
    padding-left: 20px;
    text-align: left;
    span {
      display: block;
      &:last-child {
        word-break: break-all;
      }
    }
  }
}
</style>
