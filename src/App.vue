<template>
  <main class="container mw-100 pt-5 main-container">
    <div class="row justify-content-center">
      <h1 class="text-center mb-5 col-12">{{ title }}</h1>
      <form class="col-6 form-container">
        <input v-model="inputedValue" type="text" class="text-center form-control m-auto" placeholder="Enter repository name"/>
        <button @click.prevent="search" class="btn mt-4 w-100 btn-secondary">Искать</button>
      </form>
      <div class="col-12 mt-5" v-if="isSearched">
        <div class="form-container mb-3 container" v-for="repo in searchResults" :key="repo.id">
          <h3 class="text-center mb-5">{{ repo.name }}</h3>
          <div class="row mb-5 justify-content-center align-items-center">
            <img width="2%" src="@/assets/img/star.svg" />
            <p class="mb-0 mr-5">{{ repo.stargazers_count }}</p>
            <img width="2%" src="@/assets/img/branch.svg" />
            <p class="mb-0">{{ repo.forks_count }}</p>
          </div>
          <p v-if="repo.language" class="text-center">{{ repo.language }}</p>
          <p v-else class="text-center">No defined language</p>
          <p v-if="repo.description" class="text-center mb-5">{{ repo.description }}</p>
          <p v-else class="text-center mb-5">No description</p>
          <div class="row justify-content-center align-items-center">
            <b-img width="70%" rounded="circle" :src="repo.owner.avatar_url"></b-img>
            <p class="text-center ml-4 mb-0">{{ repo.owner.login }}</p>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      title: 'Repos Searcher',
      inputedValue: '',
      searchResults: null,
      isSearched: false
    };
  },

  methods: {
    search () {
      this.isSearched = true
      axios.get(`https://api.github.com/search/repositories?q=${this.inputedValue}`).then(res => {
        this.searchResults = res.data.items
      })
    }
  }

}
</script>

<style>
@font-face {
  font-family: Roboto;
  src: url(./assets/fonts/Roboto-Regular.ttf) !important;
}

h1, h2, h3, p, button, input {
  font-family: Roboto,monospace;
  color: aliceblue;
  text-overflow: ellipsis;
  overflow: hidden;
}

.main-container {
  min-height: 100vh;
  height: 100%;
  background: linear-gradient(darkslategrey, darkcyan);
  overflow-x: hidden;
  width: 100%;
}

.form-container {
  padding: 1.5rem;
  border: 2px solid aliceblue;
  border-radius: 6px;
}

button {
  background: darkcyan
}
</style>
