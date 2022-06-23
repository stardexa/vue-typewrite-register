<template>
  <div class="container fs-40">
    <div class="row">
      <div class="col-8 offset-2">
        <span ref="giris" style="font-size: 30px"></span>
        <br>
        <br>
        <span ref="name" ></span>
        <div class="d-flex mb-4" v-if="this.process.step2 === 1">
          <span class="color-red mr-2">></span>
          <input autofocus v-model="data.name" type="text" class="m-2 balt"   @keydown.enter="step(3)">
        </div>

        <span ref="email" ></span>
        <div class="d-flex mb-4" v-if="this.process.step3 === 1">
          <span class="color-red mr-2">></span>
          <input autofocus v-model="data.email" type="text" class="m-2 balt"    @keydown.enter="step(4)">
        </div>

        <span ref="password" ></span>
        <div class="d-flex mb-4" v-if="this.process.step4 === 1">
          <span class="color-red mr-2">></span>
          <input autofocus v-model="data.password" type="text" class="m-2 balt"    @keydown.enter="step(5)">
        </div>

        <span ref="repassword" ></span>
        <div class="d-flex mb-4" v-if="this.process.step5 === 1">
          <span class="color-red mr-2">></span>
          <input autofocus v-model="data.repassword" type="text" class="m-2 balt"    @keydown.enter="step(6)">
        </div>
      </div>
    </div>
  </div>
  <button @click="dets">dets</button>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      i: 0,
      process: {
        step1:0,
        step2:0,
        step3:0,
        step4:0,
        step5:0,
      },
      data:{}
    }
  },
  mounted() {
    this.step(1)
  },
  watch: {
    'process.step1'() {
      this.step(2)
      this.process.step2 = 1
    },
  },
  methods: {
    onSave() {
      console.log(this.process)
    },
    writeClear() {
      this.i = 0
    },
    // stepControl(val){
    //   if (val === 2){
    //     this.step(2)
    //     this.process.step2 = 1
    //   }
    //   if (val === 3){
    //     this.step(3)
    //     this.process.step3 = 1
    //   }
    //   if (val === 4){
    //     this.step(4)
    //     this.process.step4 = 1
    //   }
    //   if (val === 5){
    //     this.step(5)
    //     this.process.step5 = 1
    //   }
    // },
    typeWriterText(_title, _ref, _speed = 60, _step = 1) {
      if (this.i < _title.length) {
        let output = '';
        output += _title.charAt(this.i);
        this.i = this.i + 1;
        this.$refs[_ref].innerHTML += output
        this.$refs[_ref].className = 'blink_me'
        setTimeout(() => {
          this.typeWriterText(_title, _ref, _speed)
        }, _speed);
      } else {
        this.writeClear()
        setTimeout(() => {
          this.process['step'+_step] = 1
          this.$refs[_ref].className = ''
          this.$refs[_ref].focus()
        }, 500);

      }
    },
    step(val) {
      if (val === 1){
        this.typeWriterText('Merhaba ben KAM sizin kayıt işleminizi bugun ben yapıcagım.', 'giris', '30', 1)
      }
      if (val === 2 && this.process.step2 === 0){
        this.typeWriterText('İsminiz nedir ?', 'name', '30', 2)
        this.process.step2= 1
      }
      if (val === 3 && this.process.step3 === 0){
        this.typeWriterText('Email Adresiniz Nedir ?', 'email', '30', 3)
        this.process.step3 = 1
      }
      if (val === 4 && this.process.step4=== 0){
        this.typeWriterText('Password Giriniz..', 'password', '30', 4)
        this.process['step'+val] = 1
      }
      if (val === 5 && this.process.step5 === 0){
        this.typeWriterText('RePassword Giriniz..', 'repassword', '30', 5)
        this.process['step'+val] = 1
      }
      if (val === 6 && this.process.step6 === 0){
        this.typeWriterText('Email Adresiniz Nedir ?', 'email', '30', 6)
        this.process['step'+val] = 1
      }


    }
  }
}
</script>
<style>
body {
  padding-top:5% ;
  background-color: black !important;
  color: #58ff00 !important;
}

.fs-40 {
  font-size: 19px;
}

.balt {
  width: 100%;
  background: none !important;
  border: none;
  border-bottom: 1px solid white !important;
  color: white;
}

.color-red {
  color: orangered;
}


.balt:focus {
  outline: 1px;
}


/*.blink_me { */
/*  animation: blinker 0.9s linear infinite;*/
/*}*/
.blink_me:after {
  animation: blinker 0.9s linear infinite;
  content: '|';
}
@keyframes blinker {
  50% {
    opacity: 0;
  }

}
</style>