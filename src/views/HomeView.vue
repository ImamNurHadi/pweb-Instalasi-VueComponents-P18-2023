<template>
  <div class="home">
    <Navbar />
    <Hero />
    <ShowUlasan :reviews="reviews" />
  </div>
</template>

<script>
import Navbar from '@/components/Navbar.vue';
import Hero from '@/components/Hero.vue';
import Ulasan from '@/components/Ulasan.vue'; 
import ShowUlasan from '@/components/ShowUlasan.vue';


export default {
  name: 'HomeView',
  components: {
    Navbar,
    Hero,
    Ulasan, 
    ShowUlasan,
  },
  data() {
    return {
      reviews: [], // Data untuk menyimpan ulasan
    };
  },
  methods: {
    // Metode ini akan menerima ulasan dari event dan menambahkannya ke data reviews
    addReview(newReview) {
      this.reviews.push(newReview);
    },
  },
  created() {
  console.log(this.reviews);
}
};
</script>
