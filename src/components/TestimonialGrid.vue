<template>
  <div class="testimonial-grid">
    <Testimonial v-for="(tm,i) in testimonials" v-bind:key="tm.id" :class="'tm' + (i + 1)"
                 :review="tm.review" :summary="tm.summary" :user="tm.user"></Testimonial>
  </div>
</template>

<script>
import Testimonial from "@/components/Testimonial";
export default {
  name: 'TestimonialGrid',
  components: {
    Testimonial
  },
  props: {
    testimonials: Array
  }
}
</script>

<style scoped>
.testimonial-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: repeat(2, 280px);
  grid-template-areas: 
            "tm1 tm1 tm2 tm5"
            "tm3 tm4 tm4 tm5";
  column-gap: 30px;
  row-gap: 24px;

  max-width: 1110px;
  max-height: calc(2 * 280px + 24px);
}

.tm1 {
  grid-area: tm1;
}

.tm2 {
  grid-area: tm2;
}

.tm3 {
  grid-area: tm3;
}

.tm4 {
  grid-area: tm4;
}

.tm5 {
  grid-area: tm5;
}

@media only screen and (min-width: 541px) and (max-width: 1024px) {
  .testimonial-grid {
    grid-template-columns: repeat(2, 1fr);
    grid-template-rows: repeat(3, 280px);
    grid-template-areas: 
            "tm1 tm1"
            "tm2 tm3"
            "tm5 tm5"
            "tm4 tm4";
  }

}



@media only screen and (max-width: 540px) {
  .testimonial-grid {
    display: flex;
    flex-direction: column;
  }

}


</style>
