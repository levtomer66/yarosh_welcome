<template>
  <div  class="content countdown-timer">
    <p>{{ welcome }}</p>
    <button class="big-button" @click="generate_name">תן בי</button>
    <button class="big-button" @click="copy_text">העתק</button>
    <div style="height: 80px; width: 80px">
      <a :href="'https://wa.me/?text=' + welcome +'&lang=he'"><img style="position: relative; left: 100px" src="https://img.icons8.com/doodle/344/whatsapp.png" /></a>
    </div>
  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Amatic+SC&display=swap');
.content {
  max-width: 500px;
  margin: auto;
  text-align: right;
}
img {
    max-width: 100%;
    max-height: 100%;
}
:root {
  --backgroundColor: rgba(246, 241, 209);
  --colorShadeA: rgb(106, 163, 137);
  --colorShadeB: rgb(121, 186, 156);
  --colorShadeC: rgb(150, 232, 195);
  --colorShadeD: rgb(187, 232, 211);
  --colorShadeE: rgb(205, 255, 232);
}
* {
  box-sizing: border-box;
}
*::before, *::after {
  box-sizing: border-box;
}
body {
  font-family: 'Amatic SC', 'OpenSans', sans-serif;
  font-size: 6rem;
  line-height: 2;
  display: flex;
          align-items: center;
          justify-content: center;
  margin: 0;
  min-height: 100vh;
  background: var(--backgroundColor);
}
button {
  position: relative;
  display: inline-block;
  cursor: pointer;
  outline: none;
  border: 0;
  vertical-align: middle;
  text-decoration: none;
  font-size: 1.5rem;
    color:var(--colorShadeA);
  font-weight: 700;
  text-transform: uppercase;
  font-family: inherit;
}

button.big-button {
   padding: 1em 2em;
   border: 2px solid var(--colorShadeA);
  border-radius: 1em;
  background: var(--colorShadeE);
transform-style: preserve-3d;
   transition: all 175ms cubic-bezier(0, 0, 1, 1);
}
button.big-button::before {
  position: absolute;
  content: '';
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: var(--colorShadeC);
  border-radius: inherit;
    box-shadow: 0 0 0 2px var(--colorShadeB), 0 0.75em 0 0 var(--colorShadeA);
 transform: translate3d(0, 0.75em, -1em);
     transition: all 175ms cubic-bezier(0, 0, 1, 1);
}


button.big-button:hover {
  background: var(--colorShadeD);
  transform: translate(0, 0.375em);
}

button.big-button:hover::before {
  transform: translate3d(0, 0.75em, -1em);
}

button.big-button:active {
            transform: translate(0em, 0.75em);
}

button.big-button:active::before {
  transform: translate3d(0, 0, -1em);
  
      box-shadow: 0 0 0 2px var(--colorShadeB), 0 0.25em 0 0 var(--colorShadeB);

}
</style>

<script>
  export default {
    data() {
    return {
        welcome: "יראש קטטר",
        list1: [],
        list2: []
    }
  },
  async created() {
    this.list1 = (await this.$axios.get("/nouns.txt")).data.split('\n')
    this.list2 = (await this.$axios.get("/adjectives.txt")).data.split('\n')
  },
  methods: {
    generate_name: async function() {
      const let1 = Math.floor(Math.random() * this.list1.length);
      const let2 = Math.floor(Math.random() * this.list2.length);
      this.welcome = "י" + this.list1[let1] + " " + this.list2[let2]
    },
    copy_text: function () {
      this.$copyText(this.welcome).then(x => console.log(x)).catch(e=>console.log(e))
    }
  }

  }
</script>
