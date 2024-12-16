<script setup lang="ts">
import data_people from '@/data/data_people';
import { ref } from 'vue';
import type Person from '@/types/Person';
import PersonCard from '@/components/PersonCard.vue';

const people = ref<People[]>(sortFirstName(data_people.getPeople()));

let sort = (event: Event) => {
  let element = (event.target as HTMLSelectElement);

  if (element.selectedIndex == 0) {
    people.value = (sortFirstName(data_people.getPeople()))
  } else {
    people.value = (sortFirstNameDesc(data_people.getPeople()))
  }
}


function sortFirstName(people: Person[]): Person[] {
  return [...people].sort((a, b) => a.first_name.localeCompare(b.first_name));
}
function sortFirstNameDesc(people: Person[]): Person[] {
  return [...people].sort((a, b) => b.first_name.localeCompare(a.first_name));
}

</script>

<template>
  <h1 class="display-5">Emberek</h1>
  <div class="container">
    <label for="sort">Rendezés:</label>
    <select class="form-select my-2" name="sort" @change="sort">
      <option value="0" selected>A-Z</option>
      <option value="1">Z-A</option>
    </select>
    <div class="row">
      <PeopleCard v-for="p in people" :key="p.id" class="col-md-6 col-lg-3 mx-3 my-3" :person="p" />
    </div>
  </div>
</template>


<style scoped></style>