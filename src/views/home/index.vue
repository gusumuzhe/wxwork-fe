<template>
  <div>
    <div class="title">企业微信消息通知测试</div>
    <div class="form-container">
      <van-form @submit="onSubmit">
        <van-field
          readonly
          clickable
          name="picker"
          :value="type"
          label="消息类型"
          placeholder="点击选择消息类型"
          @click="showPicker = true"
        />
        <van-popup v-model="showPicker" position="bottom">
          <van-picker
            show-toolbar
            :columns="columns"
            @confirm="onConfirm"
            @cancel="showPicker = false"
          />
        </van-popup>
        <van-field
          v-model="content"
          name="消息内容"
          label="消息内容"
          type="textarea"
          placeholder="请输入消息内容"
          :rules="[{ required: true, message: '请输入消息内容' }]"
        />

        <div style="margin: 16px">
          <van-button round block type="info" native-type="submit">提交</van-button>
        </div>
      </van-form>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import MyFooter from "@/components/MyFooter.vue";
import SvgIcon from "@/components/SvgIcon.vue";
import axios from "axios";
import { Notify } from "vant";

@Component({
  name: "Home",
  components: { MyFooter, SvgIcon },
})
export default class Home extends Vue {
  private columns: Array<any> = ["通知", "警告"];
  private typeDatas: Array<any> = [
    { name: "通知", key: "info" },
    { name: "警告", key: "warning" },
  ];
  private type: string = "通知";
  private content: string = "";
  private showPicker: boolean = false;

  created() {}

  mounted() {}
  onConfirm(value) {
    this.type = value;
    this.showPicker = false;
  }
  onSubmit(values) {
    console.log("submit", values);
    const item = this.typeDatas.find((item) => item.name === this.type);
    axios.post("/api/send", { type: item.key, content: this.content }).then((res: any) => {
      if (res.data.code === 0) {
        Notify({ type: "success", message: "消息发送成功" });
      }
    });
  }
  // onClickAdd() {
  //   this.$store.commit("moduleMain/increment");
  // }

  // onClickSub() {
  //   this.$store.commit("moduleMain/subtraction");
  // }

  // login() {
  //   var options = {
  //     user: "zd2",
  //     pwd: "1",
  //     appKey: "easemob-demo#easeim",
  //   };
  // }
}
</script>

<style lang='less' scoped>
.title {
  font-size: 20px;
  font-weight: bold;
  text-align: center;
  padding: 30px 0;
}
</style>
















