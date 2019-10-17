<template>
  <div class="about">


    <h1>This is an about2 page</h1>
    <router-link :to="{ name: 'about', params: { id: this.variable }}">Edit</router-link>
    <button class="btn btn-danger" @click.prevent="redirecciona()">Redirecciona a About</button>
  </div>
</template>
<script>
export default {
  data() {
        return {
           variable: 'marano de granja'
        }
      },
      methods: {
      redirecciona()
      {
         this.$router.push({name: 'about'});
        }
      }
    }

</script>
