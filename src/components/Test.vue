<template>
  <div>
    <h1>打字练习</h1>
    <select @change="change" :value="seedIndex">
      <option v-for="(x,i) in groups" :key="i" :value="i">{{x[0]}},{{x[1]}}</option>
    </select>
    <div>
      <span class="typed" v-for="(x,index) in typedList" :key="index">{{x}}</span>
      <span v-for="(x,index) in list" :key="index">{{x}}</span>
    </div>
    <button @click="flush">再来一次</button>
    <button @click="reflush">新数据</button>
  </div>
</template>

<script>
const typedList = []
const groups = [
  ['a',';'],
  ['s','l'],
  ['d','k'],
  ['f','j'],
  ['q','u'],
  ['w','i'],
  ['e','o'],
  ['r','p'],
  ['z','m'],
  ['x',','],
  ['c','.'],
  ['v','/'],
]
const rand = () => {
  const r = Math.random()
  return r > 0.5
}

const seedList = (seeds) => {
  const list = []
  for (let index = 0; index < 20; index++) {
    let status = rand()
    if(status) {
      list.push(seeds[1])
    } else {
      list.push(seeds[0])
    }
  }

  return list
}
let seedIndex = 0
let ruList = seedList(groups[seedIndex])
export default {
  data() {
    return {
      typedList:typedList.slice(),
      list: ruList.slice(),
      groups: groups,
      seedIndex: seedIndex,
    }
  },
  mounted() {
document.addEventListener('keydown',(e) => {
  console.log(e)
  if(this.list.length > 0 && e.key === this.list[0]) {
    this.typedList.push(this.list[0])
    this.typedList = this.typedList.slice()
    this.list = this.list.slice(1)
  }
})
  },
  methods: {
    change(e) {
      console.log("change",e)
      this.seedIndex = e.target.value
      this.reflush()
      seedIndex = e.target.value
    },
    flush() {
      this.typedList = typedList.slice()
      this.list = ruList.slice()
      console.log(this)
    },
    keyup(e) {
      console.log(e,"KSRJErPamdhWKxCBykRuoOtCZ8")
    },
    reflush() {
      console.log(this)
      this.typedList = []
      this.list = seedList(this.groups[this.seedIndex])
      ruList = this.list.slice()
      console.log(this)
    }
  }
}
</script>

<style scoped>
div {
  margin: 15px;
}
div span {
  padding: 10px;
  border: 1px solid black
}
.typed {
  color: red;
}
</style>