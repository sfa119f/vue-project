<template>
  <div class="navigation" id="navigation">
    <div class="navigation__brand">
      <div class="navigation__logo">
        <img id="nav-logo" src="@/assets/img/logo.png" alt="">
      </div>
      <div class="navigation__brandname">
        SFA Web
      </div>
    </div>
    <div class="navigation__linkcontainer" id="navigation__linkcontainer">
      <router-link to="/" class="navigation__link">
        <span class="navigation__linkhover">
          Home
        </span>
      </router-link>
      <router-link to="/calculator" class="navigation__link">
        <span class="navigation__linkhover">
          Calculator
        </span>
      </router-link>
      <router-link to="/table" class="navigation__link">
        <span class="navigation__linkhover">
          Table
        </span>
      </router-link>
    </div>
    <div class="navigation__hamburgermenu" id="change_hamburgermenu">
      <i class="fas fa-bars"></i>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Navbar'
  }
</script>