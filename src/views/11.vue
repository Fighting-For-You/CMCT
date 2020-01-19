<template>
  <div class="home">
    <Header />
    <div class="main">
      <div class="mainL fl">
        <LeftMenu />
      </div>
      <div class="mainR fl">
        <div class="mainRTop">
          <img src="../assets/new-file.jpg" alt />
        </div>
        <div class="switchMode">
          <div class="fl">
            <el-checkbox
              :indeterminate="isIndeterminate"
              v-model="checkAll"
              @change="handleCheckAllChange"
            >全选</el-checkbox>
          </div>
          <div class="fr">
            <!-- <i class="el-icon-s-operation"></i> -->
            <i class="el-icon-menu" @click="Switchclik"></i>
          </div>
          <div class="clear"></div>
        </div>
        <div :class="{styleSmall,styleBig}">
          <ul>
            <li>
              <el-checkbox-group v-model="checkedCities" @change="handleCheckedCitiesChange">
                <el-checkbox
                  v-for="(item, index) in listObj"
                  :label="item"
                  :key="item.name"
                  class="width100"
                >
                  <div @contextmenu.prevent="showDialog(index)" class="focus">
                    <i class="files-icon"></i>
                    <a href="#" @click.stop="test()">
                      <span class="name">{{item.name}}</span>
                    </a>
                  </div>
                </el-checkbox>
              </el-checkbox-group>
            </li>
          </ul>
        </div>
      </div>
      <div class="clear"></div>
    </div>
    <!-- DetailDialog -->
    <DetailDialog :message="listObj" ref="DetailDialog" />
  </div>
</template>

<script>
// @ is an alias to /src
import Header from "@/components/Header.vue";
import LeftMenu from "@/components/LeftMenu.vue";
// DetailDialog
import DetailDialog from "@/components/DetailDialog.vue";
const cityOptions = [
  { id: 1, name: "test01test01test01" },
  { id: 2, name: "test02" },
  { id: 3, name: "test03" },
  { id: 4, name: "test04" },
  { id: 5, name: "test05" },
  { id: 6, name: "test06" }
];
export default {
  name: "home",
  data() {
    return {
      styleSmall: true,
      styleBig: false,
      listObj: cityOptions,
      checkAll: false,
      checkedCities: [],
      isIndeterminate: false
    };
  },
  components: {
    Header,
    LeftMenu,
    DetailDialog
  },
  mounted() {},
  methods: {
    Leftclick(item, event) {},
    //鼠标事件
    showDialog(index) {
      this.$refs.DetailDialog.FixedModel(index);
    },
    // 样式切换
    Switchclik() {
      this.styleSmall = !this.styleSmall;
      this.styleBig = !this.styleBig;
    },
    handleCheckAllChange(val) {
      this.checkedCities = val ? cityOptions : [];
      this.isIndeterminate = false;
    },
    handleCheckedCitiesChange(value) {
      window.console.log(value);
      let checkedCount = value.length;
      this.checkAll = checkedCount === this.listObj.length;
      this.isIndeterminate =
        checkedCount > 0 && checkedCount < this.listObj.length;
    }
  }
};
</script>
<style lang="scss">
.v-modal-enter {
  animation: v-modal-in 0.2s ease;
}
.v-modal-leave {
  animation: v-modal-out 0.2s ease forwards;
}
@keyframes v-modal-in {
  0% {
    opacity: 0;
  }
}
@keyframes v-modal-out {
  to {
    opacity: 0;
  }
}
.v-modal {
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  opacity: 0.5;
  background: #000;
  z-index: 99;
}
.animated {
  position: fixed;
  right: 0px;
  top: 0px;
  z-index: 100;
  width: 300px;
  height: 100%;
  background: #fff;
  &.fadeInRightBig {
    display: block;
  }
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
a {
  color: #42b983;
}
.main {
  width: 100%;
  position: relative;
  overflow: hidden;
  .mainL {
    color: #333;
  }
  .mainR {
    .switchMode {
      width: 80%;
      .fr {
        i {
          font-size: 30px;
          color: #09aaff;
          cursor: pointer;
        }
      }
    }
    width: 100%;
    position: absolute;
    left: 200px;
    background: #fff;
    .styleSmall {
      ul {
        li {
          display: block;
          text-align: left;
          .width100 {
            width: 100%;
            border-bottom: 2px solid #f2f6fd;
            border-top: 2px solid #fff;
            &:hover {
              background: #f4fbff;
              border-top: 2px solid #f2f6fd;
            }
            .el-checkbox__label {
              width: 100%;
              line-height: 50px;
            }
          }
          span {
            display: inline-block;
            cursor: pointer;
          }
          i.files-icon {
            background: url("../assets/file-icon.png");
            background-size: 100%;
            width: 26px;
            height: 26px;
            display: inline-block;
            margin: 0px 10px -8px 10px;
          }
        }
      }
    }
    .styleBig {
      ul {
        overflow: hidden;
        li {
          .width100 {
            width: 100px;
            display: block;
            float: left;
            border: 1px solid #fff;
            padding: 10px 10px 10px 10px;
            &:hover {
              background-color: #f1f5fa;
              border: 1px solid #90d8ff;
              border-radius: 5px;
            }
          }
          span {
            display: block;
          }
          span.name {
            cursor: pointer;
            overflow: hidden;
            text-overflow: ellipsis;
            white-space: nowrap;
          }
          i.files-icon {
            background: url("../assets/files-icon.png");
            background-size: 100%;
            width: 56px;
            height: 56px;
            display: inline-block;
            margin: 0px 10px -8px 10px;
          }
        }
      }
    }
    .mainRTop {
      text-align: left;
      img {
        height: auto;
      }
    }
  }
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
