<template>
    <div class="home-view-container">
        <h1>Adopt a new best friend.</h1>

        <h2>{{ animalsCount }}</h2>
        <h3> number of Cat {{ getAllCats.length }}</h3>

        <button @click="togglePetFrom" class="btn btn-primary">Add New Pet</button>


        <b-form @submit.prevent="handleSubmit" v-if="showPetForm">

            <b-form-group id="input-group-1" label="Pet's Name:" label-for="input-1">
                <b-form-input
                        id="input-1"
                        v-model="formData.name"
                        required
                        placeholder="Enter name"
                ></b-form-input>
            </b-form-group>

            <b-form-group id="input-group-2" label="Species:" label-for="input-2">
                <b-form-select
                        id="input-2"
                        v-model="formData.species"
                        :options="['cats', 'dogs']"
                        required
                ></b-form-select>
            </b-form-group>

            <b-form-group id="input-group-3" label="Pet's Age:" label-for="input-4">
                <b-form-input
                        id="input-3"
                        v-model="formData.age"
                        required
                        placeholder="Enter Age"
                ></b-form-input>
            </b-form-group>

            <b-button type="submit" variant="primary">Submit</b-button>
            <b-button type="reset" variant="danger">Reset</b-button>
        </b-form>
    </div>
</template>

<script>
    import  { mapActions, mapGetters } from 'vuex'
    export default {
        name: 'home',
        data() {
            return {
                showPetForm: false,
                formData: {
                    name: '',
                    age: 0,
                    species: null
                }
            }
        },
        computed: {
            ...mapGetters([
                'animalsCount',
                'getAllCats'
            ])
        },
        methods: {
            ...mapActions([
                'addPet'
            ]),
            togglePetFrom() {
                this.showPetForm = !this.showPetForm
            },
            handleSubmit() {
                const {species, age, name} = this.formData
                const payload = {
                    species,
                    pet: {
                        name,
                        age
                    }
                }
                this.addPet(payload)
                this.formData = {
                    name: '',
                    age: 0,
                    species: null
                }
            }
        }
    }
</script>
