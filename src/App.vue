<template>
  <LocationForm v-if="!formSubmitted" @form-submitted="onFormSubmitted" />
  <MapComp v-else @close="onMapClosed"/>
</template>

<script>
import MapComp from './components/LocationMap.vue';
import LocationForm from './components/LocationForm.vue';

export default {
  name: 'App',
    components: {
      LocationForm,
      MapComp
  },
  data(){
    return {
      formSubmitted: false,
    };
  },
  methods: {
    onFormSubmitted() {
      this.formSubmitted = true;
    },
    onMapClosed() {
      this.formSubmitted = false;
    },
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 30px;
}

</style>
