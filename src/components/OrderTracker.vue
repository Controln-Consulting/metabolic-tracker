<template>
  <div class="controls">
    <button @click="updateOrder(-1)">Reset</button><br /><br />
    <button v-for="(item, idx) in progress" :key="idx" @click="updateOrder(idx)">
      {{ item.text }}
    </button>
  </div>

  <div class="wrapper">
    <div class="tracker">
      <div class="header">
        <h1>
          Order: <span>{{ orderNumber }}</span>
        </h1>

        <h2>
          Estimated Delivery: <span>{{ deliveryDate }}</span>
        </h2>
      </div>

      <div class="content">
        <div class="progress">
          <h3 v-for="(item, index) of progress" :key="index" :class="{ completed: item.state }">
            {{ item.text }}
          </h3>
        </div>
        <div class="icons">
          <div v-for="(item, index) of progress" :key="index" :class="{ iconCompleted: item.state }">
            <span v-if="item.state">✔</span>
          </div>
        </div>

        <h3>
          Arriving by <span>{{ deliveryDate }}.</span>
        </h3>
        <button>See Tracking Details</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { reactive } from 'vue'

const deliveryDate = 'Thursday, May 28'
const orderNumber = '#125654852'

const progress = reactive([
  {
    text: 'Preparing Order',
    state: true
  },
  {
    text: 'Shipped',
    state: false
  },
  {
    text: 'Delivered',
    state: false
  }
])

function updateOrder(index) {
  for (let i = 0; i <= index; i++) {
    progress[i].state = true
  }

  for (let i = index + 1; i < progress.length; i++) {
    progress[i].state = false
  }
}
</script>

<style scoped lang="scss">
$white: #fff;
$dark: #181919;
$lightGrayBg: #f7f7f2;
$primaryColor: #4d8721;
$darkGrayText: #707070;
$lightGrayText: #cecec9;
$fontWeight: 700;

.icons {
  position: relative;
  top: -30px;
  > div {
    background: $white;
    border: $lightGrayText 11px solid;
    width: 50px;
    height: 50px;
    border-radius: 50%;
    text-align: center;
    color: $white;
    font-size: 25px;
    line-height: 30px;
  }
}

.progress {
  h3 {
    color: $lightGrayText;
    padding-bottom: 30px;
    width: 50%;
    border-bottom: $lightGrayText 10px solid;
    text-align: center;
    -webkit-transition: border-bottom 0.5s ease-out;
    -moz-transition: border-bottom 0.5s ease-out;
    -o-transition: border-bottom 0.5s ease-out;
    transition: border-bottom 0.5s ease-out;

    -webkit-transition: color 0.5s ease-out;
    -moz-transition: color 0.5s ease-out;
    -o-transition: color 0.5s ease-out;
    transition: color 0.5s ease-out;

    &:first-child {
      text-align: left;
      &:before {
        margin: 30px 0 0 0px;
      }
    }
  }

  h3:last-child {
    text-align: right;
    &:before {
      margin: 30px 0 0 0px;
    }
  }
}

.controls {
  width: 300px;
  margin: 10px auto;
  text-align: center;

  button {
    margin: 5px;
    padding: 5px;
  }
}

.wrapper {
  background: $lightGrayBg;
  max-width: 700px;
  margin: 0 auto;
  padding: 20px;
}

.tracker {
  background: $white;
  color: #000;
  font-weight: $fontWeight;
  padding: 25px;

  .header,
  .progress,
  .icons {
    display: flex;
    justify-content: space-between;

    h1 {
      display: block;
      font-size: 30px;
      font-weight: $fontWeight;

      span {
        color: $dark;
        font-weight: $fontWeight;
        color: $darkGrayText;
      }
    }

    h2 {
      display: block;
      font-size: 23px;
      font-weight: $fontWeight;
      width: 230px;
      text-align: right;

      span {
        color: $dark;
        font-weight: $fontWeight;
        color: $darkGrayText;
      }
    }
  }

  .content {
    border-top: $dark dashed 1px;
    border-bottom: $dark dashed 1px;
    padding: 20px 0 40px 0;
    margin-top: 20px;
    position: relative;

    .completed {
      color: $primaryColor;
      border-bottom: $primaryColor 10px solid;
    }

    .iconCompleted {
      background: $primaryColor;
      border: $primaryColor 11px solid;
    }

    h3 {
      font-size: 20px;
      font-weight: $fontWeight;
      width: 100%;

      span {
        color: $dark;
        font-weight: $fontWeight;
        color: $darkGrayText;
      }
    }

    button {
      display: block;
      width: 100%;
      background: $dark;
      color: $lightGrayBg;
      padding: 20px 30px;
      border-radius: 50px;
      border: none;
      font-size: 20px;
      margin-top: 20px;
    }
  }
}
</style>
