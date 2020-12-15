<template>
  <div class="App">
    <div class="Content">
      <p v-if="isLoading">
        Loading!
      </p>

      <p v-if="error">
        An error happened :(
      </p>

      <TestimonialGrid v-if="!isLoading" :testimonials="testimonials"></TestimonialGrid>
    </div>
  </div>
</template>

<script>
import TestimonialGrid from './components/TestimonialGrid.vue'
import { onMounted, ref} from "vue";

export default {
  name: 'App',
  components: {
    TestimonialGrid
  },
  setup() {
    const testimonials = ref(null);
    const isLoading = ref(true);
    const error = ref(null);

    onMounted(() => {
      fetch('http://localhost:3000/testimonials')
          .then(res => {
            if (!res.ok) {
              const error = new Error(res.statusText);
              error.json = res.json();
              throw error;
            }
            return res.json();
          })
          .then(data => testimonials.value = data)
          .catch(e => error.value = e)
          .finally(() => isLoading.value = false)
    });

    return {testimonials, isLoading, error};
  }
}
</script>

<style>
* {
  box-sizing: border-box;
}

body {
  --color-primary-violet: hsl(263, 55%, 52%);
  --color-primary-dark-grayish-blue: hsl(217, 19%, 35%);
  --color-primary-dark-blackish-blue: hsl(219, 29%, 14%);
  --color-primary-white: hsl(0, 0%, 100%);
  --color-primary-white-rgb: 255, 255, 255;

  --color-neutral-light-grey: hsl(0, 0%, 81%);
  --color-neutral-greyish-blue: hsl(210, 46%, 95%);


  margin: 0;
  font-family: 'Barlow Semi Condensed', -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', 'Oxygen',
  'Ubuntu', 'Cantarell', 'Fira Sans', 'Droid Sans', 'Helvetica Neue',
  sans-serif;
  font-size: 13px;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background-color: var(--color-neutral-greyish-blue);
}

code {
  font-family: source-code-pro, Menlo, Monaco, Consolas, 'Courier New',
  monospace;
}

.App {
  text-align: center;
  height: 100vh;
}

.Content {
  display: flex;
  justify-content: center;
  align-items: center;

  max-width: 1440px;
  height: 100%;
  margin: 0 auto;
  padding: 16px;
}

@media only screen and (max-width: 1024px) {
  .Content {
    align-items: start;
  }
}

</style>
