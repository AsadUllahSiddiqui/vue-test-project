<template>
  <div class="pet-registration container my-5">
    <h2 class="text-center mb-4">Tell us about your dog</h2>
    <form @submit.prevent="submitForm">
      <!-- Dog's name input -->
      <div class="mb-3">
        <label for="petName" class="form-label">What is your dog's name?</label>
        <input
          type="text"
          class="form-control"
          id="petName"
          v-model="pet.name"
          placeholder="Monte"
          required
        />
      </div>

      <!-- Breed input with search -->
      <div class="mb-3">
        <label for="breed" class="form-label">What breed are they?</label>
        <input
          type="search"
          class="form-control"
          id="breed"
          v-model="pet.breed"
          list="breeds"
          placeholder="Can't find it?"
          required
        />
        <datalist id="breeds">
          <option v-for="breed in allBreeds" :key="breed" :value="breed">
            {{ breed }}
          </option>
        </datalist>
      </div>

      <!-- Breed choice radios -->
      <div class="mb-3">
        <div><strong>Choose One</strong></div>
        <div class="form-check">
          <input
            class="form-check-input"
            type="radio"
            name="breedChoice"
            id="unknown"
            value="unknown"
            v-model="pet.breedChoice"
          />
          <label class="form-check-label" for="unknown">I don't know</label>
        </div>
        <div class="form-check">
          <input
            class="form-check-input"
            type="radio"
            name="breedChoice"
            id="mix"
            value="mix"
            v-model="pet.breedChoice"
            @change="toggleBreedInput"
          />
          <label class="form-check-label" for="mix">It's a mix</label>
        </div>
      </div>

      <!-- Selected breeds display -->
      <div v-if="showBreedInput" class="mb-3">
        <label for="selectedBreeds" class="form-label">Selected breeds</label>
        <input
          type="text"
          class="form-control"
          id="selectedBreeds"
          readonly
          :value="pet.selectedBreeds.join(', ')"
        />
      </div>

      <!-- Gender buttons -->
      <div class="mb-4">
        <label class="form-label d-block">What gender are they?</label>
        <div class="btn-group" role="group" aria-label="Gender selection">
          <input
            type="button"
            class="btn"
            :class="{
              'btn-outline-primary': pet.gender !== 'female',
              'btn-primary': pet.gender === 'female',
            }"
            @click="setGender('female')"
            value="Female"
          />
          <input
            type="button"
            class="btn"
            :class="{
              'btn-outline-primary': pet.gender !== 'male',
              'btn-primary': pet.gender === 'male',
            }"
            @click="setGender('male')"
            value="Male"
          />
        </div>
      </div>

      <!-- Submission button -->
      <div class="d-grid">
        <button type="submit" class="btn btn-success">Continue</button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      pet: {
        name: "",
        breed: "",
        breedChoice: null,
        gender: null,
        selectedBreeds: [],
        showBreedInput: false,
      },
    };
  },
  computed: {
    allBreeds() {
      return ["Breed 1", "Breed 2", "Breed 3", "Breed 4", "Breed 5", "Breed 6"];
    },
  },
  methods: {
    submitForm() {
      console.log(this.pet);
    },
    toggleBreedInput() {
      this.showBreedInput = this.pet.breedChoice === "mix";
    },
    setGender(gender) {
      this.pet.gender = gender;
    },
  },
};
</script>

<style scoped></style>
