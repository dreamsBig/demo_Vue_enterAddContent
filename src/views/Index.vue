<template>
  <div class="index">
    <div class="indexFrame">
      <div>使用回车可以添加内容</div>
      <input
        type="text"
        @keyup.enter="onEnter"
        v-model="InputText"
        @input="getWord(InputText)"
        placeholder="请输入的文本"
      >
      <hr>
      <label
        style="display:block; color:blue"
        for=""
      >显示文本</label>
      <ul>
        <li
          v-for="(key,index) in addList"
          :key="index"
          class="addText"
        >
          <span class="addList_font" :title="key">{{key}}</span><span @click="deleteCurrent(index)" class="deleteList">删除</span>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      /* 输入框的值 */
      InputText: '',
      /* 添加列表的值 */
      addList: ''
    }
  },
  mounted () {
    this.addList = JSON.parse(localStorage.getItem('addList')) || []
  },
  methods: {
    getWord (InputText) {
      // console.log(InputText)
    },
    onEnter () {
      // 开头添加
      this.addList.unshift(this.InputText)
      // 先判断是否重复的值---在增加
      let arrs = new Set(this.addList)
      this.addList = Array.from(arrs)
      // 添加到本地存储
      localStorage.setItem('addList', JSON.stringify(this.addList))
      // 初始化的值
      this.InputText = ''
    },
    // 删除当前的文件
    deleteCurrent (index) {
      this.addList.splice(index, 1)
      // 添加到本地存储
      localStorage.setItem('addList', JSON.stringify(this.addList))
    }
  }
}
</script>

<style lang="less" scoped>
.indexFrame {
  margin: 20px;
}
ul {
  list-style: none;
  margin: 0px;
  padding: 0px;
  .addText {
    color: skyblue;
    width: 180px;
    .addList_font {
      float: left;
      width: 120px;
      overflow: hidden;
      text-overflow: ellipsis;
      white-space: nowrap;
    }
    .deleteList {
      float: right;
      color: red;
      cursor: pointer;
    }
  }
}
</style>
