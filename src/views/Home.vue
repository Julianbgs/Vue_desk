<template>
  <div class="main">
    <Cards />
  </div>
</template>

<script>
// @ is an alias to /src
import Cards from '@/components/Cards.vue';
import Form from '@/components/Form.vue';

export default {
  name: 'Home',
  components: {
    Cards,
    Form
  }
}
</script>

<style>
  .main {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
  }
</style>
