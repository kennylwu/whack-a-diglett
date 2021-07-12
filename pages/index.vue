<template>
  <div class="bg-gray-300 h-screen">
    <div class="container mx-auto py-5">
      <div class="flex justify-center">
        <h1 class="text-5xl py-5">Whack a Diglett</h1>
      </div>
        <div class="flex justify-center">
          <table class="table-auto">
            <tbody>
              <tr>
                <td class="w-1/3 bg-white">
                  <button ref="1" class="mt-3 hidden"><img src="\img\Diglett_AG_anime.png" alt="diglett" class="pt-2 fadeInBottom cssanimation" v-on:click="click(1)" :v-model="score"></button>
                </td>
                <td class="w-1/3">
                  <button ref="2" class="mt-3 hidden"><img src="\img\Diglett_AG_anime.png" alt="diglett" class="pt-2 fadeInBottom cssanimation" v-on:click="click(2)" :v-model="score"></button>
                </td>
                <td class="w-1/3">
                  <button ref="3" class="mt-3 hidden"><img src="\img\Diglett_AG_anime.png" alt="diglett" class="pt-2 fadeInBottom cssanimation" v-on:click="click(3)" :v-model="score"></button>
                </td>
              </tr>
              <tr>
                <td>
                  <button ref="4" class="mt-3 hidden"><img src="\img\Diglett_AG_anime.png" alt="diglett" class="pt-2 fadeInBottom cssanimation" v-on:click="click(4)" :v-model="score"></button>
                </td>
                <td>
                  <button ref="5" class="mt-3 hidden"><img src="\img\Diglett_AG_anime.png" alt="diglett" class="pt-2 fadeInBottom cssanimation" v-on:click="click(5)" :v-model="score"></button>
                </td>
                <td>
                  <button ref="6" class="mt-3 hidden"><img src="\img\Diglett_AG_anime.png" alt="diglett" class="pt-2 fadeInBottom cssanimation" v-on:click="click(6)" :v-model="score"></button>
                </td>
              </tr>
              <tr>
                <td>
                  <button ref="7" class="mt-3 hidden"><img src="\img\Diglett_AG_anime.png" alt="diglett" class="pt-2 fadeInBottom cssanimation" v-on:click="click(7)" :v-model="score"></button>
                </td>
                <td>
                  <button ref="8" class="mt-3 hidden"><img src="\img\Diglett_AG_anime.png" alt="diglett" class="pt-2 fadeInBottom cssanimation" v-on:click="click(8)" :v-model="score"></button>
                </td>
                <td>
                  <button ref="9" class="mt-3 hidden"><img src="\img\Diglett_AG_anime.png" alt="diglett" class="pt-2 fadeInBottom cssanimation" v-on:click="click(9)" :v-model="score"></button>
                </td>
              </tr>
            </tbody>
          </table>
          <div class="pl-5">
            <h3 class="text-3xl">Score: {{ score }}</h3><br>
             <label class="inline-flex items-center">
              <input type="radio" class="form-radio" name="radio" value="easy" checked v-on:click="changeLevel(1500)">
              <span class="ml-2">Easy</span>
            </label>
            <label class="inline-flex items-center ml-6">
              <input type="radio" class="form-radio" name="radio" value="medium" v-on:click="changeLevel(1000)">
              <span class="ml-2">Medium</span>
            </label>
            <label class="inline-flex items-center ml-6">
              <input type="radio" class="form-radio" name="radio" value="hard" v-on:click="changeLevel(500)">
              <span class="ml-2">Hard</span>
            </label>
            <br><br>
            <button v-if="start == false" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded" v-on:click="startGame()" :v-model="start">
              Start
            </button>
            <button v-else class="bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded" v-on:click="stopGame()" :v-model="start">
              Stop
            </button>
            <br>
            <h3 class="text-2xl pt-5">Previous Score: {{ previousScore }}</h3>
          </div>   
        </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
     return {
        start: false,
        score: 0,
        diglett: 0,
        time: 60,
        level: 1500,
        intervalId: 0,
        previousScore: 0
     }
   },
  methods: {
    startGame () {
      this.start = !this.start;
      if (this.start == true) {
        this.intervalId = setInterval(this.activate, this.level)
      }
    },
    activate () {
      if (this.start == true) {
        this.diglett = Math.floor(Math.random() * 9) + 1;
        let previous = this.diglett
        console.log('activate', this.diglett);
        this.$refs[this.diglett].classList.remove("hidden")
        this.$refs[this.diglett].classList.add("active")
        setTimeout(() => {this.hide(previous)}, 2000);
      }
    },
    timeout () {
      setTimeout(function() {console.log('hello')}, 5000);
    },
    hide (numb) {
      this.$refs[numb].classList.remove("active")
      this.$refs[numb].classList.add("hidden")
      console.log('removed', numb)
    },
    stopGame () {
      this.start = false;
      clearInterval(this.intervalId);
      this.clear();
      this.previousScore = this.score;
      this.score = 0;
      console.log('stop')
    },
    click (numb) {
      console.log(numb)
      this.$refs[numb].classList.remove("active")
      this.$refs[numb].classList.add("hidden")
      this.score += 1;
    },
    changeLevel (int) {
      this.stopGame();
      this.level = int;
    },
    clear () {
      for (let i = 1 ; i <= 9; i++) {
        this.$refs[i].classList.remove("active")
        this.$refs[i].classList.add("hidden")
      }
    }
  },
}
</script>

<style scoped>
table {
  background-color: white;
}
td {
  border: 1px solid black;
  min-width: 260px;
  height: 260px;
}

.cssanimation {
    animation-duration: 1s;
    animation-fill-mode: both;
}

.fadeInBottom { animation-name: fadeInBottom }
@keyframes fadeInBottom {
    from {
        opacity: 0;
        transform: translateY(10%);
    }
    to { opacity: 1 }
}

.active {
  display: block;
}
</style>
