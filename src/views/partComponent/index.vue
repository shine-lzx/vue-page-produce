<template>
  <div class="root_container">
    <div class="top_container">
      <top-part></top-part>
    </div>
    <div class="main_container">
      <div class="left_container">
        <left-part></left-part>
      </div>
      <div class="middle_container">
        <middle-part></middle-part>
      </div>
      <div class="right_container">
        <right-part></right-part>
      </div>
    </div>
  </div>
</template>

<script>
import topPart from './topPart'
import leftPart from './leftPart'
import middlePart from './middlePart'
import rightPart from './rightPart'

export default {
  components: {
    topPart,
    leftPart,
    middlePart,
    rightPart
  }
}
</script>

<style lang="scss" scoped>
.root_container {
  .top_container {
    width: 100%;
    height: 50px;
    background-color: #1f1e1c;
  }
  .main_container {
    display: flex;
    width: 100%;
    height: calc(100vh - 50px);

    .left_container {
      width: 200px;
      // background-color: red;
    }
    .middle_container {
      flex: 1;
      position: relative;
      border-left: 1px solid #f3f1f1;
      border-right: 1px solid #f3f1f1;
      background-color: #ffffff
    }
    .right_container {
      // flex: 2;
      width: 300px;
      // background-color: yellow;
    }
  }
}
</style>
