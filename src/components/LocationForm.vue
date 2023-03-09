<template>
    <div class="top-division">
        <form class="location-form"  @submit.prevent="submitForm">
      <label class="location-form__label">
        <span class="location-form__label-text">Location Name:</span>
        <input class="location-form__input" type="text" v-model="locationName" @input="updateLocalStorage">
      </label>
      <label class="location-form__label" style="width: 300px;">
        <span class="location-form__label-text">Description:</span>   
        <input class="location-form__input" style="height: 50px;" type="text" v-model="description" @input="updateLocalStorage">
      </label>

      <label class="location-form__label">
      <span class="location-form__label-text">Latitude (up to 2 decimal points):</span>
      <input class="location-form__input" style="width: 200px; align-self: center;" type="number" step="0.01" v-model.number="latitude" @input="updateLocalStorage">
    </label>

    <label class="location-form__label">
      <span class="location-form__label-text">Longitude (up to 2 decimal points):</span>
      <input class="location-form__input" style="width: 200px; align-self: center;" type="number" step="0.01" v-model.number="longitude" @input="updateLocalStorage">
    </label>

      <button class="location-form__submit-btn" type="submit" :disabled="isDisabled">Submit</button>

      <div class="last-desc">Enter the Fields to search your Location</div>
    </form>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        locationName: localStorage.getItem('locationName') || '',
        description: localStorage.getItem('description') || '',
        latitude: parseFloat(localStorage.getItem('latitude')) || null,
        longitude: parseFloat(localStorage.getItem('longitude')) || null,
      };
    },
    methods: {
        submitForm() {
      this.$emit('form-submitted');
    },
      updateLocalStorage() {
        localStorage.setItem('locationName', this.locationName);
        localStorage.setItem('description', this.description);
        localStorage.setItem('latitude', this.latitude);
        localStorage.setItem('longitude', this.longitude);
      },
    },
    computed: {
        isDisabled() {
        return !this.locationName || !this.description || !this.latitude || !this.longitude;
        },
    },
  };
  </script>
  

  <style scoped>
  .top-division{
    display: flex;
    justify-content: center;
  }
  .last-desc{
    margin-top: 50px;
    color: black;
    font-family: Arial, Helvetica, sans-serif;
    font-size: 20px;
    font-weight: bold;
  }

  form {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 2rem;
    background-color: #f0f0f0;
    border-radius: 10px;
  }
  
  label {
    margin: 1rem 0;
    font-size: 1.2rem;
  }
  
  input[type="text"],
  input[type="number"] {
    padding: 0.5rem;
    border: none;
    border-radius: 5px;
    background-color: #e0e0e0;
    font-size: 1rem;
    width: 100%;
  }
  
  input[type="submit"] {
    padding: 0.5rem 1rem;
    background-color: #007aff;
    color: white;
    border: none;
    border-radius: 5px;
    font-size: 1.2rem;
    cursor: pointer;
    margin-top: 2rem;
    width: 50%;
    transition: background-color 0.2s ease-in-out;
  }
  
  input[type="submit"]:hover:not(:disabled) {
    background-color: #005dff;
  }
  
  input[type="submit"]:disabled {
    background-color: #bbb;
    cursor: not-allowed;
  }
  
  input[type="text"]:focus,
  input[type="number"]:focus {
    outline: none;
    box-shadow: 0 0 3px rgba(0, 0, 0, 0.3);
  }
  
  @media only screen and (max-width: 768px) {
    input[type="submit"] {
      width: 80%;
    }
  }

  .location-form {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 2rem;
  height: 600px;
  margin-left: 400px;
  margin-right: 400px;
  background-color: rgb(109, 133, 109);
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  min-width: 500px;
}

.location-form__label {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  margin-bottom: 1.5rem;
}

.location-form__label-text {
  margin-bottom: 0.5rem;
  font-size: 1.2rem;
  font-weight: 600;
}

.location-form__input {
  padding: 0.75rem;
  border: none;
  border-radius: 5px;
  background-color: #f0f0f0;
  font-size: 1.2rem;
  width: 100%;
  box-sizing: border-box;
  box-shadow: 0 0 3px rgba(0, 0, 0, 0.1);
}

.location-form__submit-btn:disabled {

  padding: 0.75rem 1.5rem;
  background-color: #007aff;
  color: #fff;
  border: none;
  border-radius: 5px;
  opacity: 0.5;
  cursor: not-allowed;
}

.location-form__submit-btn:enabled {
    padding: 0.75rem 1.5rem;
    cursor: pointer;
  background-color: #007aff;
  color: #fff;
  border: none;
  border-radius: 5px
}
  </style>
