<template>
  <div class="app">
    <div class="hamburgermenu__container" :class="{'hamburgermenu':showMenu}">
      <BurgerMenu/>
    </div>
    <header>
      <nav class="navigation" id="burgermenu" v-if="!desktopView">
        <div class="navigation__brand">
          <div class="navigation__logo">
            <img id="nav-logo" src="@/assets/img/logo.png" alt="">
          </div>
          <div class="navigation__brandname">
            SFA Web
          </div>
        </div>
        <div class="navigation__hamburgermenu" id="change_hamburgermenu" @click="showMenu = !showMenu">
          <i :class="{'fas fa-bars':showMenu, 'fas fa-times':!showMenu}"></i>
        </div>
      </nav>
      <Navbar v-if="desktopView"/>
    </header>
    <router-view/>
    <Footer/>
  </div>
</template>

<script>
  import Navbar from './components/Navbar'
  import BurgerMenu from './components/BurgerMenu'
  import Footer from './components/Footer'

  export default {
    components: {
      Navbar,
      BurgerMenu,
      Footer
    },
    data: () => {
      return {
        desktopView: true,
        showMenu: false
      }
    },
    methods: {
      handleView() {
        this.desktopView = window.innerWidth > 800 ? true : false;
      }
    },
    created() {
      this.handleView();
      window.addEventListener('resize', this.handleView);
    }
  }
</script>

<style>
  @import './assets/style/common.css';
  @import './assets/style/all.min.css';
  @import './assets/style/solid.min.css';
  @import './assets/style/navbar.css';
</style>
