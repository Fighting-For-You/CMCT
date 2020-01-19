<template>
  <div class="Dialog">
    <el-dialog
      title="详情"
      :visible.sync="centerDialogVisible"
      width="30%"
      top="0"
      @close="closeDialog"
      :class="{'fadeOutRightBig':isOut,'fadeInRightBig':isIn}"
    >
      <span v-if="index !== -1">
        <el-form ref="form" :model="form" label-width="80px">
          <el-form-item label="重命名">
            <el-input v-model="message[index].name"></el-input>
          </el-form-item>
          <el-form-item label="创建时间">{{message[index].date}}</el-form-item>
        </el-form>
      </span>
      <span slot="footer" class="dialog-footer">
        <el-button @click="centerDialogVisible = false">取 消</el-button>
        <el-button type="primary" @click="centerDialogVisible = false">确 定</el-button>
      </span>
    </el-dialog>
  </div>
</template>

<script>
export default {
  name: "DetailDialog",
  props: {
    message: Array
  },
  data() {
    return {
      form: {
        Rename: ""
      },
      index: -1,
      centerDialogVisible: false,
      isOut: false,
      isIn: false
    };
  },
  components: {},
  methods: {
    // 鼠标事件-右键
    FixedModel(index) {
      this.index = index;
      this.centerDialogVisible = true;
      this.isIn = true;
      this.isOut = false;
    },
    closeDialog() {
      this.isIn = false;
      this.isOut = true;
    }
  }
};
</script>
<style  lang="scss">
.el-dialog {
  height: 100%;
  box-sizing: border-box;
  margin: 0 auto 0px !important;
  right: 0px;
  position: absolute !important;
}
.fl {
  float: left;
}
.fr {
  float: right;
}
.clear {
  clear: both;
}
</style>
