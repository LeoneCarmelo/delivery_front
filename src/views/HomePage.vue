<script>
import SearchBar from "../components/SearchBar.vue";
import StaticSections from "../components/StaticSections.vue";
import Footer from "../components/Footer.vue";
import { store } from "../store";
export default {
  components: {
    SearchBar,
    Footer,
    StaticSections
  },
  data() {
    return {};
  },
  methods: {},
  mounted() {
    if (this.$route.params.message) {
      //reset carrello e storage
      localStorage.clear()
      store.cart = []
      setTimeout(() => {
        this.$router.replace({ params: { message: null } });
        const alertMessage = document.querySelector('.alert')
        alertMessage.classList.add('d-none')
      }, 3000)
    }
  },
};
</script>

<template>
  <div class="main">
    <main>
      <div class="alert alert-success mb-0" v-if="$route.params.message">
        <p class="mb-0 p-0">{{ $route.params.message }}</p>
      </div>
      <div class="container h-100 d-flex flex-column justify-content-end justify-content-md-center">
        <div class="row justify-content-center justify-content-md-start">
          <div class="col mb-4">
            <h1 class="">Seleziona il tipo di ristorante e scegli cosa mangiare</h1>
            <SearchBar />
          </div>
        </div>
      </div>
    </main>
    <StaticSections />
    <Footer />
  </div>
</template>


<style lang="scss" scoped>
@use '../styles/variables.scss' as *;
@use '../styles/general.scss';

main {
  height: 100vh;
  background: url('./img/cheesburger.png'), linear-gradient(122deg, $d-boo-background 50%, $d-boo-orange 50%);

  background-repeat: no-repeat;

  .alert-success {
    margin-top: 90px;
    position: absolute;
    width: 100%;
  }

}

@media screen and (max-width: 768px) {
  main {
    background-position: top 50% right 50%, center;
  }
  h1 {
    width: 100%;
    text-align: center;
  }
}

@media screen and (min-width: 768px) {
  main {
    background-position: top 50% right 10%, center;
  }
  h1 {
    width: 50%;
    text-align: start;
  }
}
</style>