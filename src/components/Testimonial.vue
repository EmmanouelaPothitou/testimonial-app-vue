<template>
  <div class='testimonial'>
    <div class="user-info">
      <img :src="imgUrl" alt="avatar"/>
      <div class="user-details">
        <div class="name">{{ user.name }}</div>
        <div class="title">{{ user.title }}</div>
      </div>
    </div>
    <h2 class="summary">{{ summary }}</h2>
    <div class="review">“{{ review }}”</div>
  </div>
</template>

<script>
export default {
  name: 'Testimonial',
  props: {
    summary: String,
    review: String,
    user: {
      name: String,
      title: String,
      avatar: String
    }
  },
  computed: {
    imgUrl() {
      return `/images/${this.user.avatar}`
    }
  }
}
</script>

<style scoped>
.testimonial {
  position: relative;
  padding: 25px 35px 35px 30px;
  color: var(--color-primary-white);
  border-radius: 10px;
  text-align: left;
  line-height: 1.35em;
}

.user-info {
  display: flex;
  margin-bottom: 20px;
}

.user-info img {
  width: 32px;
  height: 32px;
  border: 2px solid rgba(var(--color-primary-white-rgb), 40%);
  border-radius: 50%;
  margin-right: 15px;
}

.user-info .user-details {
  text-align: left;
}

.user-info .user-details .name {
  font-size: 1.05em;
}

.user-info .user-details .title {
  font-size: 0.9em;
  opacity: 50%;
}

.summary {
  font-size: 1.5em;
  margin: 20px 0;
  line-height: 1.25em;
}

.review {
  opacity: 70%;
}

.testimonial:nth-of-type(1) {
  background-color: var(--color-primary-violet);
  z-index: 1;
}

.testimonial:nth-of-type(1)::before {
  content: "";
  position: absolute;
  width: 110px;
  height: 100px;
  background-image: url("../assets/bg-pattern-quotation.svg");
  background-repeat: no-repeat;
  top: 0;
  right: 14%;
  z-index: -1;
}

.testimonial:nth-of-type(2) {
  background-color: var(--color-primary-dark-grayish-blue);
}

.testimonial:nth-of-type(3),
.testimonial:nth-of-type(5) {
  color: var(--color-primary-dark-grayish-blue);
  background-color: var(--color-primary-white);
  box-shadow:
      6px 20px 20px rgba(0, 0, 0, 0.034),
      2px 6px 20px rgba(0, 0, 0, 0.06),
      7px 9px 16px rgba(0, 0, 0, 0.086),
      9px 8px 50px rgba(0, 0, 0, 0.12);

}

.testimonial:nth-of-type(4) {
  background-color: var(--color-primary-dark-blackish-blue);
}

.testimonial:nth-of-type(2) img,
.testimonial:nth-of-type(3) img,
.testimonial:nth-of-type(5) img {
  border: 2px solid transparent;
}

@media only screen and (max-width: 375px) {
  .testimonial {
    padding: 22px;
  }
}
</style>
