<template>
  <div class="header">
    <div class="wrapper">
      <div class="inner-wrapper">
        <!-- icon section-->
        <div class="icon">
          <!-- <img :src="icon('')" alt=""> -->
        </div>

        <!-- menu section-->
        <div class="menu">
          <span v-for="name in menu" :key="name" :class="{'active' : name === 'calendar'}">
            {{ name | capitalize }}

            <img v-if="['reports', 'setup'].includes(name)" :src="icon('expand-arrow')" alt="">
          </span>
        </div>
      </div>

      <!-- options section -->
      <div class="options">
        <div class="options-left" >
          <span class="msg">Send Mesages</span>
          <div class="toggle" @click="toggle = !toggle"
            :style="{ 'background-color' : toggle ? '' : '#C1C1C1 !important' }">
            <img :src="icon('appointment-completed-icon')" alt="">
            <!-- button -->
            <div class="toggle-button" :class="toggle ? 'toggle-right' : 'toggle-left'" 
              ></div>
          </div>
        </div>

        <div class="options-right">
          <div class="help">?</div>
          <div class="user">
          </div>
          <img style="cursor: pointer;" 
            :src="icon('expand-arrow')" alt="">
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import Vue from 'vue'
  
  export default Vue.extend({
    data() {
      return {
        menu: ['calendar', 'online booking', 'customer', 'messages', 'reports', 'setup'],
        toggle: true
      }
    },
    methods: {
      icon(iconName) {
        return require(`@/assets/SVG/${iconName}.svg`)
      },
    },
    filters: {
      capitalize: function (value) {
        if (!value) return ''
        value = value.toString()
        return value.charAt(0).toUpperCase() + value.slice(1)
      }
    }
  })
</script>

<style lang="scss" scoped>
  .header {
    width: 100%;
    height: 78px;
    display: flex;
    justify-content: center;
    background-color: white;
    position: sticky;
    top: 0;
    z-index: 10;
    box-shadow: 0px 0px 5px rgba(0, 0, 0, 0.1) ; 
  }
  .wrapper {
    display: flex;
    align-items: center;
    justify-content: space-between;
    // border: 1px solid red;
    width: 100%;
    max-width: 1588px;
    height: 100%;

    .inner-wrapper {
      display: flex;
      justify-content: space-between;
      align-items: center;
      max-width: 908px;
      width: 100%;
      
      .icon {
        width: 40px;
        height: 40px;
        border: 2px solid #30A26B;
        border-radius: 100%;
      }
    }
  }
  
  .menu {
    span {
      margin-left: 55px;
      cursor: pointer;
      color: #3D4140;
      
      img {
        width: 12px;
        // height: 10px
      }
    }
    span:first-child {
      margin-left: 0px !important;
    }
    span:hover {
      color: #30A26B;
    }
  }

  .toggle {
    display: flex;
    position: relative;
    // justify-content: space-around;
    align-items: center;
    background-color: #30A26B;
    width: 71px;
    height: 32px;
    border-radius: 50px;
    padding: 3px;
    cursor: pointer;

    img {
      width: 17px;
      height: 13px;
      margin-left: 10px;
      filter: invert(1)
      // path {
      //   fill: #fff
      // }
    }
    .toggle-button {
      position: absolute;
      width: 26px;
      height: 26px;
      background-color: white;
      border-radius: 100%;
    }
  }

  .options {
    display: flex;
    align-items: center;

    .options-left {
      display: flex;
      align-items: center;
      margin-right: 41px;
      .msg {
        font-size: 16px;
        margin-right: 9px;
      }
    }

    .options-right {
      display: flex;
      justify-content: center;
      align-items: center;
      
      .help {
        width: 32px;
        height: 32px;
        border: 2px solid #30A26B;
        display: flex;
        justify-content: center;
        align-items: center;
        border-radius: 50px;
        font-size: 20px;
        margin-right: 20px;
      }
      .user {
        width: 40px;
        height: 40px;
        background-color: #30A26B;
        border-radius: 50px;
        margin-right: 7px;
      }
      img {
        width: 14px;
        // height: 7px;
      }
    }
  }
  
  .active {
    color: #30A26B !important;
  }

  .toggle-right {
    right: 3px
  }
  .toggle-left {
    left: 3px;
  }
</style>