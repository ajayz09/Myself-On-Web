<template>
  <div class="brand">
    <h1> {{title}} </h1>
    <hr id="title-ul">
    <div class="tag-lines">
          <div v-for="(tag,i) in tagLines" class="tag" :id="'tag-'+i" v-bind:key="'tag-'+i">
          <h3 :id="'tag-'+i+'-contents'" :style="{'color': tag.color}" v-html="tag.text"></h3>
          </div>
    </div>
    <div class="container" >
      <div class="chevron" id="chevron"></div>
      <div class="chevron" id="chevron"></div>
      <div class="chevron" id="chevron"></div>
      <!-- <span class="text">Scroll down</span> -->
    </div>
  </div>

</template>

<script>

export default {
  name: 'TitleBrand',
  props: ["title","colors"],
  data () {
    return {
      tagCycler: null,
      tagLines: [
        {
          text: "Student &#8226; Developer &#8226; Nerd",
          color: "#afb5ba"
        },
        {
          text: "A real whizz with html",
          color: this.colors[0]
        },
        {
          text: "Loves python like a child",
          color: this.colors[2]
        },
        {
          text: "Only cries a little at seg faults",
          color: this.colors[3]
        }
      ],
      liveTag: 0
    }
  },
  methods: {
    cycleTagLines() {
      if (this.liveTag == this.tagLines.length-1) {
        this.liveTag = 0
        window.console.log("Tag Reset");
        this.resetTagLines()
        return
      }
      // get our elements
      let ul = document.getElementById("title-ul")
      let ti = this.liveTag
      let t = document.getElementById("tag-"+ti)
      let tc = document.getElementById("tag-"+ti+"-contents")
      // var scroll = document.getElementById("chevron").className="chevron:before"
      // document.styleSheets[0].addRule('chevron:before', 'background: green;');
      // document.styleSheets[0].addRule('chevron:after', 'background: green;');
      // // scroll.pseudoStyle("before","background","purple")
      // scroll.pseudoStyle("after","background","purple")
      window.Velocity(t, { 'min-width': '0%' }, 1000)
      window.Velocity(ul, { 'background-color': this.tagLines[ti+1].color}, 1000)
      window.Velocity(tc, { opacity: 0 }, 500)
      // window.Velocity(scroll, { 'background': this.tagLines[ti+1].color}, 1000)
      // let arr = document.getElementById()

      this.liveTag++

    },
    resetTagLines() {
      let ul = document.getElementById("title-ul")
      window.Velocity(ul, { 'background-color': this.tagLines[0].color}, 1000)
      for (var i in this.tagLines) {
        let t = document.getElementById("tag-"+i)
        let tc = document.getElementById("tag-"+i+"-contents")
        window.Velocity(t, {'min-width': '100%'}, 500)
        window.Velocity(tc, { opacity: 1 }, 1000)
      }
    }
  },
  created () {
    this.tagCycler = window.setInterval(this.cycleTagLines, 5000)
  },
  destroyed () {
    window.clearInterval(this.tagCycler);
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  @import url('https://fonts.googleapis.com/css?family=Roboto|Source+Sans+Pro|Ubuntu');
  .brand {
    width: 40vw;
    text-align: center;
    font-family: 'Ubuntu',sans-serif;
  }
  .brand hr{
    border: 0;
    height: 3px;
    border-radius: 25px;
    width: 100%;
    background-color: #919aa1;
  }
  .brand h1{
    font-size: 3rem;
    margin-top: 0;
  }
  .brand h3{
    font-size: 1.5rem;
    color: #919aa1;
    padding: 0;
    margin: 0;
    width: 100%;
  }
  .container {
  margin-top: 50px;
  justify-content: center;
  width: 24px;
  height: 24px;
}

.chevron {
  justify-content: center;
  position: absolute;
  left: 50%;
  width: 28px;
  height: 8px;
  opacity: 0;
  /* background: ; */
  transform: scale3d(0.5, 0.5, 0.5);
  animation: move 3s ease-out infinite;

}

.chevron:first-child {
  animation: move 3s ease-out 1s infinite;
}

.chevron:nth-child(2) {
  animation: move 3s ease-out 2s infinite;
}

.chevron:before,
.chevron:after {
  content: ' ';
  position: absolute;
  top: 0;
  height: 100%;
  width: 51%;
  background: #fff;
}


.chevron:before {
  left: 0;
  transform: skew(0deg, 30deg);
}

.chevron:after {
  right: 0;
  width: 50%;
  transform: skew(0deg, -30deg);
}

@keyframes move {
  25% {
    opacity: 1;

  }
  33% {
    opacity: 1;
    transform: translateY(30px);
  }
  67% {
    opacity: 1;
    transform: translateY(40px);
  }
  100% {
    opacity: 0;
    transform: translateY(55px) scale3d(0.5, 0.5, 0.5);
  }
}

.text {
  display: block;
  margin-top: 75px;
  margin-left: -30px;
  font-family: "Helvetica Neue", "Helvetica", Arial, sans-serif;
  font-size: 12px;
  color: #fff;
  text-transform: uppercase;
  white-space: nowrap;
  opacity: .25;
  animation: pulse 2s linear alternate infinite;
}

@keyframes pulse {
  to {
    opacity: 1;
  }
}
  /* roles animations */
  .brand .tag-lines {
    margin-top: 1.5rem;
    width: 100%;
    height: 1.7rem;
    overflow: hidden;
    display: flex;
    flex-direction: row;
  }
  .brand .tag-lines .tag {
    min-width: 100%;
  }
  @media screen and (max-width: 600px){
    .brand {
      width: 90vw;
      text-align: center;
      font-family: 'Ubuntu',sans-serif;
    }
  }
</style>
