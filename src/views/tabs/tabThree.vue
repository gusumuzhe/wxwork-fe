<template>
  <div class="home-model tcenter">
    <van-tabs v-model="activeTab">
      <van-tab v-for="index in 4" :title="'tab' + index" :key="index">
        content of tab {{ index }}
      </van-tab>
    </van-tabs>
    <div class="single">tabThree</div>
    <div class="single">tabThree</div>
    <div class="single">tabThree</div>
    <div class="single">tabThree</div>
    <div class="single">tabThree</div>
    <div class="single">tabThree</div>
    <div class="single">tabThree</div>
    <div class="single">tabThree</div>
    <MyFooter :active="2"></MyFooter>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import MyFooter from "@/components/MyFooter.vue";

@Component({
  name: "TabThree",
  components: { MyFooter },
})
export default class TabThree extends Vue {
  private activeTab = 0;
}
</script>

<style lang='less' scoped>
.home-model {
  width: 100%;
  height: 100vh;
  padding: 10px;
}

.single {
  width: 100%;
  height: 50px;
  margin-top: 20px;
}
</style>
