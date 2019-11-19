<template>
  <div class="login">
    <el-form :model="ruleForm" status-icon ref="ruleForm" class="demo-ruleForm">
      <el-form-item prop="username">
        <el-input type="text" v-model="ruleForm.username" autocomplete="off"></el-input>
      </el-form-item>
      <el-form-item prop="pass">
        <el-input type="text" v-model="ruleForm.pass" autocomplete="off"></el-input>
      </el-form-item>
      <!-- <el-form-item>
        <el-button type="primary" @click="submitForm('ruleForm')">提交</el-button>
      </el-form-item>-->
      <div
        class="move-icon"
        :style="styles"
        @click="submitForm('ruleForm')"
        @mouseenter="mouseEnter(0)"
        @mouseleave="mouseLeave(0)"
      ></div>
    </el-form>
  </div>
</template>

<script>
let _interval = []; // eslint-disable-line
export default {
  name: 'Login',
  data() {
    return {
      ruleForm: {
        pass: '',
        username: ''
      },
      rules: {},
      styles: {},
      tooIconObj: {
        frame: 120,
        s: [0],
        id: null,
        toolObjs: []
      }
    };
  },
  mounted() {
    // let le = document.getElementsByClassName('move-icon').length;
    // this.tooIconObj.s = new Array(le).fill(0);
  },
  methods: {
    submitForm(formName) {
      this.$refs[formName].validate(valid => {
        if (valid) {
          alert('submit!');
        } else {
          console.log('error submit!!');
          return false;
        }
      });
    },
    mouseEnter(i) {
      this.normal(i);
    },
    mouseLeave(i) {
      this.reverse(i);
    },
    rend(i) {
      this.styles = {
        'background-position': '0 -' + 100 * this.tooIconObj.s[i] + 'px'
      };
    },
    normal(i) {
      let self = this;
      self.tooIconObj.s[i]++;
      clearTimeout(_interval[i]);
      if (self.tooIconObj.s[i] < this.tooIconObj.frame) {
        self.rend(i);
        _interval[i] = setTimeout(function() {
          self.normal(i);
        }, 16);
      } else {
        self.tooIconObj.s[i] = self.tooIconObj.frame;
      }
    },
    reverse(i) {
      let self = this;
      self.tooIconObj.s[i]--;
      clearTimeout(_interval[i]);
      if (this.tooIconObj.s[i] >= 0) {
        self.rend(i);
        _interval[i] = setTimeout(function() {
          self.reverse(i);
        }, 16);
      } else {
        self.tooIconObj.s[i] = 0;
      }
    }
  }
};
</script>
<style lang="less">
.move-icon {
  width: 100px;
  height: 100px;
  background-size: 100%;
  background-position: 0 0;
  margin: 10px auto 0;
  background-image: url(../assets/icon-nlp.png);
}

.login {
  width: 400px;
  margin-left: auto;
  margin-right: auto;
}
</style>
