<template>
  <div class="hello">
    
  </div>
</template>

<script>
export default {
  data () {
    return {
      // note: changing this line won't causes changes
      // with hot-reload because the reloaded component
      // preserves its current state and we are modifying
      // its initial state.
      msg: 'Hello World!',
      startGame: false,
      blockArray: []
    }
  },
  methods: {
    initGame () {
      console.log('数据看累了？来玩一局游戏吧')
      window.onkeydown = this.handleKeyDown
      console.log('点击页面并按回车键进入游戏模式')
      var args = [
        'Dock your console to main window, press %cENTER%c to start and use %arrow key%c or %cWASD%c to play 2048 in console!'
        ,'color:red;font-weight:bold;',''
        ,'color:red;font-weight:bold;',''
        ,'color:red;font-weight:bold;',''
      ]
      console.log.apply(console,args)
      let a = ['%c1%c %c1%c \n %c1%c %c1%c'];
      console.log.apply(console, a.concat(['color:red;font-weight:bold;','','color:red;font-weight:bold;','','color:red;font-weight:bold;','','color:red;font-weight:bold;','']))
    },
    handleKeyDown (e) {
      let keyNum = e.keyCode || e.which
      let keyChart
      const map = {
        72: '1',
        74: '2',
        75: '3',
        76: '4'
      }
      if (!this.startGame) {
        if (keyNum === 13) {
          this.startGame = true
          this.renderGame()
        }
        return
      } else {
        this.runGame(map[keyNum] || 0)
      }
    },
    runGame (key) {
      if (key) {
        console.clear()
        this.blockArray.slice()
        this.blockArray.pop()
        this.blockArray.unshift(this.getRandom())
        console.table(this.blockArray)
      }
    },
    renderGame () {
      console.log('开始渲染游戏')

      this.$log('blockArray')
    },
    InitBlockArray () {
      var arr = [];
      for (let i = 0; i < 4; i++) {
        arr.push(this.getRandom())
      }
      return arr
    },
    getRandom () {
      let arr = [0, 0, 0, 0]
      arr[Math.floor(4 * Math.random())] = 1;
      return arr
    },
  },
  destory () {
    window.onkeydown = null;
  },
  ready () {
    this.initGame()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  color: #42b983;
}
</style>
