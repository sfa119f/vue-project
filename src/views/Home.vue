<template>
  <div class="container-fluid">
    <h1>Hello Everyone!</h1>
    <div class="profil__container">
      <div class="profil__detail">
        <h2>Uddin is right here</h2>
        <h2>Welcome to my website</h2>
      </div>
      <div class="profil__photo">
        <img src="../assets/img/syarifuddin.png">
      </div>
    </div>
    <div class="sosmed__container">
      <h2>Follow my social media</h2>
      <div class="list__sosmed">
        <router-link to="https://www.linkedin.com/in/syarifuddinfa/" class="sosmed">
          <i class="fab fa-linkedin-in"></i>
        </router-link>
        <router-link to="https://www.instagram.com/sfa_arf" class="sosmed">
          <i class="fab fa-instagram"></i>
        </router-link>
        <router-link to="https://twitter.com/u_dinnn" class="sosmed">
          <i class="fab fa-twitter"></i>
        </router-link>
        <router-link to="https://github.com/sfa119f" class="sosmed">
          <i class="fab fa-github"></i>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Home'
  }
</script>

<style>
  @import '../assets/style/home.css'
</style>