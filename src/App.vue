<template>
  <div id="app">
    <div>
      <form v-show="isshow">
        <div class="form-item">
          <h1>领取专属守护犬</h1>
          <div class="form-filed">
            <label>姓名: <input type="text" name="name" v-model="name"></label>
          </div>
          <div class="form-filed">
            性别:
            <label>
                <input type="radio" v-model="gender" name="gender" value="1">
                男
            </label>
            or
            <label>
                <input type="radio" v-model="gender" name="gender" value="2">
                女
            </label>
          </div>
          <div class="submit" @click="submit">
            <button >生成</button>
          </div>
        </div>
      </form>
      <div v-show="isshow" id="stage" v-if="dog">
        <div class="content">
          <span>恭祝：</span>
          <h1>天狗守吉祥 天狗保平安</h1>
          <div >
            <img height="80" width="80" :src="dogs[dog]" class="main-img">
            <div class="dog-tips">
              我是<strong>{{dogNamesCn[dog]}}</strong>
            </div>
          </div>
        </div>
        <div class="logo_rccode">
          <img src="./assets/orc.jpg">
        </div>
      </div>
      <div v-show="!isshow" style="text-align: center; margin-bottom: 20px;"> 长按狗狗保存图片 分享祝福</div>
    </div>
  </div>
</template>

<script>
import html2canvas from 'html2canvas'
export default {
  name: 'app',
  data() {
    return {
      proverb: [
        "狗年大吉，旺旺旺",
        "狗富贵，一起旺",
        "金犬玉狗，汪到福到",
        "汪汪年!人旺旺!",
        "天狗守吉祥 天狗保平安",
        "旺旺狗年，幸福吉祥！",
        "旺旺狗年，幸福吉祥！",
        "瑞狗迎春"
      ],
      isshow: true,
      name: '',
      gender: '',
      dog: null,
      dogNames: [
        'beagle',
        'tuffpugg',
        'bassed',
        'boldercollie',
        'bullterrier',
        'cocker',
        'doberman',
        'husky',
        'pitbull',
        'shepherd',
        'gussy',
        'chihuahua'
      ],
      dogNamesCn: {
        'beagle': '贝高',
        'tuffpugg': '八哥',
        'bassed': '巴吉度 小短腿',
        'boldercollie': '博得 牧羊犬',
        'bullterrier': '红雷㹴',
        'cocker': '曲卡',
        'doberman': '杜宾',
        'husky': '哈士奇',
        'pitbull': '法斗',
        'shepherd': '牧羊犬',
        'gussy': '泰迪',
        'chihuahua': '吉娃娃'
      },
      dogs: {
        beagle: require('./assets/beagle.jpg'),
        tuffpugg: require('./assets/tuffpugg.jpg'),
        bassed: require('./assets/bassed.jpg'),
        boldercollie: require('./assets/boldercollie.jpg'),
        bullterrier: require('./assets/bullterrier.jpg'),
        cocker: require('./assets/cocker.jpg'),
        doberman: require('./assets/doberman.jpg'),
        husky: require('./assets/husky.jpg'),
        pitbull: require('./assets/pitbull.jpg'),
        shepherd: require('./assets/shepherd.jpg'),
        gussy: require('./assets/gussy.jpg'),
        chihuahua: require('./assets/chihuahua.jpg')
      }
    }
  },
  components: {
  },
  methods: {
    getRandomNumber(name, gender) {
      var resultCode = (name.charCodeAt(0) * name.length * gender) % 12;
      return resultCode;
    },
    submit(e) {
      e.preventDefault()
      if (!this.name || !this.gender) {
        return;
      }
      const code = this.getRandomNumber(this.name, this.gender);
      this.tip = this.proverb[code % 8];
      this.dog = this.dogNames[code];
      setTimeout(() => {
        html2canvas(document.querySelector("#stage")).then(canvas => {
            document.body.appendChild(canvas)
          this.isshow = false;
        });
      }, 300);
    }
  }
}
</script>

<style>
html{
  font-size: 100px;
}
body{
  font-size: 16px;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#stage{
  height: 3rem;
  width: 3rem;
  color: red;
  /*border: 1px solid red;*/
  position: relative;
}
#stage .content {
  position: absolute;
  right: 0;
}
.main-img{
  margin: .3rem;
}
.content h1{
  /*padding: 20px;*/
  font-size: 28px;
  padding-top: 0px;
  margin-top: 0px;
  margin-bottom: 10px;
}
.dog-tips{
  color: slategrey;
}
.logo_rccode{
  height: 28px;
  width: 28px;
  position: absolute;
  bottom: 0px;
  right:0px;
}
.logo_rccode img {
  width: inherit;
}
.form-item{
  padding: .3rem;
}
.form-filed{
    border-bottom: 1px solid #999;
    text-align: left;
    line-height: 2.5;
}
.submit{
  padding-top:.5rem;
}
button{
    font-size: 14px;
    color: #fff;
    height: 40px;
    padding: 5px 1rem;
    background: #1b93fb;
    border-radius: 6px;
}
</style>
