<template>
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
    <router-link to="table" class="navigation__link">
      <span class="navigation__linkhover">
        Table
      </span>
    </router-link>
  </div>
</template>

<script>
  export default {
    name: 'BurgerMenu'
  }
</script>