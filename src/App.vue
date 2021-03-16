<template>
  <main class="container mw-100 pt-5 main-container">
    <div class="row justify-content-center">
      <h1 class="text-center mb-5 col-12">{{ title }}</h1>
      <form class="col-6 form-container">
        <input type="text" class="text-center form-control m-auto" placeholder="Enter repository name"/>
        <button @click.prevent class="btn mt-4 w-100 btn-secondary" style="background: darkcyan">Искать</button>
      </form>
    </div>
  </main>
</template>

<script>

export default {
  data() {
    return {
      title: 'Repos Searcher',
    };
  },

}
</script>

<style>
@font-face {
  font-family: Roboto;
  src: url(./assets/fonts/Roboto-Regular.ttf) !important;
}

h1, p, button, input {
  font-family: Roboto,monospace;
  color: aliceblue;
}

.main-container {
  height: 100vh;
  background: linear-gradient(darkslategrey, darkcyan);
}

.form-container {
  padding: 1.5rem;
  border: 2px solid aliceblue;
  border-radius: 6px;
}
</style>
