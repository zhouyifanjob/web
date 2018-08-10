<template>
  <div>
   <span @click="TabTure" :class="flag==1?'bc':''">用户管理</span>
   <span @click="Tab" :class="flag==0?'bc':''">用户字段</span>
   <div v-if="flag">
    <ul>
      <li v-for="item, index in data" :key="index">
        <el-tree :data="data" :props="defaultProps" @node-click="handleNodeClick"></el-tree>
      </li>
    </ul>
   </div>
  </div>
</template>

<script>
export default {
  name: 'Usermanage',
  data() {
    return {
      flag: 1,
      data: [{

      }],
      defaultProps: {
        children: 'children',
        label: 'label'
      }
    }
  },
  props: {
    isActive: {
      type: Boolean,
      default: false
    },
    toggleClick: {
      type: Function,
      default: null
    }
  },
  methods: {
    Tab() {
      this.flag = 0
    },
    TabTure() {
      this.flag = 1
    },
    reqRoc() {
      const url = this.HOST + '/departments'
      // const urls = require('../../../../../static/userManage.json')
      this.$axios.get(url)
        .then(res => {
          // this.data = res.data
          console.log(this.data)
          const objs = {}
          for (let i = 0; i <= this.data.length; i++) {
            objs.label = res.data[i].name
            // objs.children.label = res.data[i].createTime
            // objs.children.children.label = res.data[i].name
            this.data.push(objs)
          }
        })
        .catch(error => {
          console.log(error)
        })
      // this.$axios.get(url)
      //   .then(res => {
      //     this.data = res.data
      //     console.log(this.data)
      //   })
      //   .then(error => {
      //     console.log(error)
      //   })
    },
    handleNodeClick(data) {
      console.log(data)
    }
  },
  created() {
    this.reqRoc()
  }
}
</script>

<style scoped>
.hamburger {
	display: inline-block;
	cursor: pointer;
	width: 20px;
	height: 20px;
	transform: rotate(90deg);
	transition: .38s;
	transform-origin: 50% 50%;
}

.hamburger.is-active {
	transform: rotate(0deg);
}
.bc{
  background-color: gray;

}
</style>
