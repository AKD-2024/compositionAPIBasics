<template>
  <div class="home">
    <h1>Home</h1>
    <input type="text" v-model="search" />
    <p>search term - {{ search }}</p>
    <div v-for="name in matchingNames" :key="name">{{ name }}</div>
    <button @click="handleClick">stop watching</button>
    <!-- <h1>Home</h1>
    <p ref="p">My name is {{ name }} and my age is {{ age }}</p> -->
    <!-- <p>My name is {{ name }} and my age is {{ age }}</p>
    <button @click="handleClick">click me</button>
    <button @click="age++">Increment Age</button>
    <input type="text" v-model="name">
    <h2>Refs</h2>
    <p>{{ ninjaOne.name }} - {{ ninjaOne.age }} - {{ nameOne }}</p>
    <button @click="updateNinjaOne">Update ninja one</button>
    <h2>Reactive</h2>
    <p>{{ ninjaTwo.name }} - {{ ninjaTwo.age }} - {{ nameTwo }}</p>
    <button @click="updateNinjaTwo">Update ninja Two</button> -->
  </div>
</template>

<script>
import { ref, reactive, computed, watch, watchEffect } from "vue";
export default {
  name: "HomeView",
  setup() {
    //Computed Values
    const search = ref("");
    const names = ref([
      "mario",
      "yoshi",
      "luigi",
      "toad",
      "bowser",
      "koopa",
      "peach",
    ]);

    const stopWatch = watch(search, () => {
      console.log("watch function ran");
    });

    const stopEffect = watchEffect(() => {
      console.log('watchEffect function ran', search.value);
    });

    const matchingNames = computed(() => {
      return names.value.filter((name) => {
        return name.includes(search.value);
      });
    });

    const handleClick = () => {
      stopWatch();
      stopEffect();
    }

    return { names, search, matchingNames, handleClick };

    const ninjaOne = ref({ name: "anjali", age: 22 });
    const ninjaTwo = reactive({ name: "mario", age: 40 });

    //reactive can't be used for primitive types
    const nameOne = ref("dino");
    const nameTwo = reactive("deno");

    const updateNinjaOne = () => {
      ninjaOne.value.age = 23;
    };

    const updateNinjaTwo = () => {
      ninjaTwo.age = 63;
      // nameTwo = "dino"; won't change as reactive doesn't work for primitive types
    };

    // return {
    //   ninjaOne,
    //   updateNinjaOne,
    //   ninjaTwo,
    //   updateNinjaTwo,
    //   nameOne,
    //   nameTwo,
    // };
    // console.log(this); -- undefined

    // const p = ref(null);
    // console.log(p, p.value); p- ref object and p.value will be null as we passed null above it will be whatever  we pass there

    // const name = ref("mario");
    // const age = ref(30);

    // const handleClick = () => {
    //   name.value = "Anjali";
    //   age.value = 22;
    // console.log(p, p.value); // p is ref object and p.value is the <p>...</p> tag
    // p.value.classList.add('test');
    // p.value.textContent = "Hello Everyone!"

    // }

    // return { name, age, handleClick};
    // return { name: name, age: age };
    // return { name, age, handleClick, p }; since the key and the variable we are assigning to key have same name we can do like this.
  },
};
</script>
