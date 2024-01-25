<template>
  <div class="text-start pet-registration container my-5 card">
    <img src="../assets/paws.png" class="mb-3">
    <h4 class="mb-4 default-color">Tell us about your pet</h4>
    <form @submit.prevent="submitForm">
      <div class="mb-3">
        <label for="petName" class="form-label">What is your pet's name?</label>
        <input
          type="text"
          class="form-control"
          id="petName"
          v-model="pet.name"
          placeholder="Name"
          required
        />
      </div>

      <div class="m-3">
        <div><strong>Choose One</strong></div>
        <div class="form-check">
          <input
            class="form-check-input"
            type="radio"
            name="type"
            id="cat"
            value="cat"
            v-model="pet.type"
          />
          <label class="form-check-label" for="cat">Cat</label>
        </div>
        <div class="form-check">
          <input
            class="form-check-input"
            type="radio"
            name="type"
            id="dog"
            value="dog"
            v-model="pet.type"
            @change="togglePetType"
          />
          <label class="form-check-label" for="dog">Dog</label>
        </div>
      </div>
      <div class="mb-3">
        <label for="breed" class="form-label">What breed are they?</label>
        <input
          type="dropdown"
          class="form-control"
          id="breed"
          v-model="pet.breed"
          list="breeds"
          placeholder="Select a breed"
          required
        />
        <datalist id="breeds">
          <option v-for="breed in breads" :key="breed" :value="breed">
            {{ breed }}
          </option>
        </datalist>
      </div>

      <div v-show="unknownBreed" class="m-3">
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
      <div v-show="unknownBreed && mixBreed" class="mb-3">
        <label for="selectedBreeds" class="form-label">Selected breeds</label>
        <input
          type="text"
          class="form-control"
          id="selectedBreeds"
          v-model="pet.breeds"
        />
      </div>

      <!-- Gender buttons -->
      <div class="mb-4">
        <label class="form-label d-block">What gender are they?</label>
        <div class="btn-group" role="group" aria-label="Gender selection">
          <input
            type="button"
            class="btn default-color"
            :class="{
              'btn-outline-primary': pet.gender !== 'female',
              'btn-primary': pet.gender === 'female',
            }"
            @click="setGender('female')"
            value="Female"
          />
          <input
            type="button"
            class="btn default-color"
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
        <button type="submit" class="btn btn-primary">Continue</button>
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
        type: "",
        breedChoice: "",
        gender: "",
        breed: [],
        showBreedInput: false,
      },
      catBreeds: ["Cat 1", "Cat 2", "Cat 3", "Cat 4", "Cat 5", "Cat 6", "Can't find it?"],
      dogBreeds: ["Dog 1", "Dog 2", "Dog 3", "Dog 4", "Dog 5", "Dog 6", "Can't find it?"]
    };
  },
  computed: {
    breads(){
      return this.pet.type === 'dog' ? this.dogBreeds : this.catBreeds
    },
    unknownBreed(){
      return this.pet.breed === "Can't find it?"
    },
    mixBreed(){
      return this.pet.breedChoice === "mix"
    },

  },
  methods: {
    submitForm() {
      if (this.mixBreed) {
        let breeds = this.pet.breeds.split(',')
        breeds.map((breed)=>{
          breed.trim()
        })
        this.pet.breeds = breeds
      }
      console.log(this.pet);
    },
    selectBreed(val){
      this.breads.push(val)
    },
    setGender(gender) {
      this.pet.gender = gender;
    },
  },
};
</script>

<style scoped>
.container{
  box-shadow: #090909;
  padding: 10px 40px 40px 40px;
  width: 30%;
  background-color: white;
}
.default-color{
  color: #00a0e5;

}
  .default-color:hover{
    background-color: #00a0e5;
  }
.btn-primary{
  background-color: #00a0e5;
  color: white;
  border: none;

}
.btn-primary:hover{
  background-color: #00a0e5;
}

.btn-outline-primary{
  border: 1px solid #00a0e5;
}

.form-check-input{
  background-color: #e0dfdf;
}

.form-check-input:checked{
  background-color: #00a0e5;
  border-color: #00a0e5;
}
</style>
