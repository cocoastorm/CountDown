<template>
  <div class="countdown">
    <div class="block">
      <p class="digit">{{ days | two_digits }}</p>
      <p class="text">Days</p>
    </div>

    <div class="block">
      <p class="digit">{{ hours | two_digits }}</p>
      <p class="text">Hours</p>
    </div>

    <div class="block">
      <p class="digit">{{ minutes | two_digits }}</p>
      <p class="text">Minutes</p>
    </div>

    <div class="block">
      <p class="digit">{{ seconds | two_digits }}</p>
      <p class="text">Seconds</p>
    </div>
  </div>
</template>

<script>
  export default {
    props: ['date'],
    data() {
      return {
        now: Math.trunc((new Date()).getTime() / 1000)
      }
    },
    created: function () {
      var vm = this
      setInterval(function () {
        vm.now = Math.trunc((new Date().getTime()) / 1000)
      }, 1000)
    },
    computed: {
      dateObj() {
        return Math.trunc(Date.parse(this.date) / 1000)
      },

      seconds() {
        return (this.dateObj - this.now) % 60
      },

      minutes() {
        return Math.trunc((this.dateObj - this.now) / 60) % 60
      },

      hours() {
        return Math.trunc((this.dateObj - this.now) / 60 / 60) % 24
      },

      days() {
        return Math.trunc((this.dateObj - this.now) / 60 / 60 / 24)
      }
    },
    filters: {
      two_digits: function (value) {
        var strValue = value.toString()
        if (strValue <= 1) {
          return "0" + strValue
        }
        return strValue
      }
    }
  }
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Lato|Roboto');

body {
  font-family: 'Roboto', 'Helvetica', sans-serif;
  font-size: 16px;
}

h1, h2, h3, h4, h5, h6 {
  font-family: 'Lato', serif;
}

.countdown {
  display: flex;
  flex-direction: row;
  justify-content: center;
}

.block {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 25px;
}

.text {
  font-size: 1.2em;
  font-family: 'Lato', serif;
  margin: 10px auto;
  text-align: center;
}

.digit {
  font-size: 4em;
  font-family: 'Roboto', serif;
  margin: 10px;
  text-align: center;
}
</style>
