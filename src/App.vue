<template>
  <div>
    <div v-if="popup">
      <PopUp @togglePopup="togglePopup" />
    </div>
    <NavBar />
    <MainPage @togglePopup="togglePopup" />
  </div>
</template>

<script >
import NavBar from "./components/NavBar.vue";
import MainPage from "./pages/MainPage.vue";
import PopUp from './components/PopUp.vue';


export default {
  components: { NavBar, MainPage, PopUp },
  data() {
    return { popup: true }
  },
  methods: {
    togglePopup() {
      this.popup = !this.popup
    },
  }
}
</script>
