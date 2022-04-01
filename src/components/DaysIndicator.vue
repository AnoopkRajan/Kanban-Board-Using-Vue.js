<template>
  <div class="dots-wrapper">
    <div class="dots-container" v-if="dotsNumber === 0 || dotsNumber === 1">
      <div class="all-dots">
        <span class="dot lightgrey"></span>
      </div>
    </div>
    <div class="dots-container" v-if="dotsNumber === 2">
      <div class="all-dots">
        <span class="dot lightgrey"></span>
        <span class="dot grey"></span>
      </div>
    </div>
    <div class="dots-container" v-if="dotsNumber === 3 || dotsNumber === 4">
      <div class="all-dots">
        <span class="dot lightgrey"></span>
        <span class="dot lightgrey"></span>
        <span class="dot yellow"></span>
      </div>
    </div>
    <div class="dots-container" v-if="dotsNumber >= 5 && dotsNumber <= 7">
      <div class="all-dots">
        <span class="dot lightgrey"></span>
        <span class="dot lightgrey"></span>
        <span class="dot lightgrey"></span>
        <span class="dot orange"></span>
      </div>
    </div>
    <div class="dots-container" v-if="dotsNumber >= 8 && dotsNumber <= 11">
      <div class="all-dots">
        <span class="dot lightgrey"></span>
        <span class="dot lightgrey"></span>
        <span class="dot orange"></span>
        <span class="dot orange"></span>
      </div>
    </div>
    <div class="dots-container" v-if="dotsNumber >= 12 && dotsNumber <= 19">
      <div class="all-dots">
        <span class="dot lightgrey"></span>
        <span class="dot orange"></span>
        <span class="dot orange"></span>
        <span class="dot orange"></span>
      </div>
    </div>
    <div class="dots-container" v-if="dotsNumber >= 20">
      <div class="all-dots">
        <span class="dot orange"></span>
        <span class="dot orange"></span>
        <span class="dot orange"></span>
        <span class="dot orange"></span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "DaysIndicator",
  props: ["dotsNumber"],
};
</script>

<style lang="scss" scoped>
$lightgrey: rgb(230, 230, 230);
$grey: rgb(207, 207, 207);
$yellow: yellow;
$orange: orange;

$circle-size: 5px;

.dots-container {
  display: flex;
  justify-content: space-evenly;
  align-items: center;
  width: 20%;
  margin: 10px auto;
}

.all-dots {
  display: flex;
  justify-content: space-evenly;
}

.dot {
  height: $circle-size;
  width: $circle-size;
  border-radius: 50%;
}

.lightgrey {
  background: $lightgrey;
}

.grey {
  background: $grey;
}

.yellow {
  background: $yellow;
}

.orange {
  background: $orange;
}
</style>
