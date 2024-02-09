<template>
  <div class=" ">
    <div class="bg-black mx-auto px-5 sm:px-10 md:px-20 lg:px-40 pb-5">
      <div class="justify-center text-center align-center pt-10">
        <div class="flex justify-center text-center align-center px-10 pt-20">
          <h1 class="flex text-3xl md:text-6xl font-bold text-white w-[700px]">
            The Complete Stripe™ Alternatives List
          </h1>
        </div>
        <div class="flex text-center justify-center align-center pt-10">
          <P class="text-md font-small text-white w-[700px]">
            Explore the best alternatives to Stripe for your business. Compare
            features, pricing, and find the perfect solution for your needs.
          </P>
        </div>
      </div>
      <div class="mt-10">
        <input
          type="text"
          id="first_name"
          v-model="searchText"
          class="bg-transparent p-3 text-white text-sm rounded-xl focus:ring-blue-500 border border-gray-800 focus:border-gray-900 block w-full p-2.5"
          placeholder="Search among 36 payment gateways..."
          required
          @input="searchByText($event)"
        />
      </div>
      <div class="mt-10 flex flex-wrap">
        <div
          type="button"
          class="rounded-full my-2 text-gray-400 text-sm font-medium uppercase px-5 hover:cursor-pointer py-2.5 hover:text-white"
          :class="
            activeCat == -1 ? '  bg-[#9E72D4]   text-black  hover:text-black' : ''
          "
          @click="onCatClick('All', -1)"
        >
          All
        </div>
        <div
          type="button"
          v-for="(item, index) in featuresList"
          :key="index"
          class="rounded-full my-2 text-gray-400 text-sm font-medium uppercase px-5 hover:cursor-pointer py-2.5 hover:text-white"
          :class="
            activeCat == index
              ? '   bg-[#9E72D4]   text-black  hover:text-black'
              : ''
          "
          @click="onCatClick(item, index)"
        >
          {{ item.label }}
        </div>
      </div>

      <div class="mt-6 flex flex-wrap">
        <div
          :class="
            activeFeature == -1
              ? '  bg-white   text-black  hover:text-black'
              : ''
          "
          type="button"
          class="rounded-full my-2 text-gray-400 text-sm font-medium uppercase px-5 hover:cursor-pointer py-2.5 hover:text-white"
          @click="onFeatureClick('All', -1)"
        >
          All
        </div>
        <div
          type="button"
          v-for="(item, index) in allFeatures"
          :key="index"
          class="rounded-full my-2 text-gray-400 text-sm font-medium uppercase px-5 hover:cursor-pointer py-2.5 hover:text-white"
          :class="
            activeFeature == index
              ? '  bg-white   text-black  hover:text-black'
              : ''
          "
          @click="onFeatureClick(item, index)"
        >
          {{ item }}
        </div>
      </div>
      <div class="mt-6 text-white">
        <div
          class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4 w-full"
        >
          <div
            v-for="(item, index) in filteredSitesList"
            :key="index"
            class="flex justify-center"
          >
            <a
              href="#"
              class="relative text-gray-300 w-full block max-w-sm p-6 bg-black border border-gray-600 rounded-lg shadow hover:text-gray-400 hover:border-gray-700"
            >
              <h5 class="mb-2 text-2xl font-bold tracking-tight">
                {{ item?.name }}
              </h5>
              <p class="font-normal pb-14">
                {{ item?.description }}
              </p>
              <div class="flex items-center absolute bottom-5 right-5">
                <svg
                  v-for="(star, index) in setStars(item.rating / 2)"
                  :key="index"
                  :class="{
                    'w-4 h-4 text-yellow-300 ms-1': star === 'yellow',
                    'w-4 h-4 ms-1 text-gray-300 dark:text-gray-500':
                      star === 'gray',
                  }"
                  aria-hidden="true"
                  xmlns="http://www.w3.org/2000/svg"
                  fill="currentColor"
                  viewBox="0 0 22 20"
                  class=""
                >
                  <path
                    d="M20.924 7.625a1.523 1.523 0 0 0-1.238-1.044l-5.051-.734-2.259-4.577a1.534 1.534 0 0 0-2.752 0L7.365 5.847l-5.051.734A1.535 1.535 0 0 0 1.463 9.2l3.656 3.563-.863 5.031a1.532 1.532 0 0 0 2.226 1.616L11 17.033l4.518 2.375a1.534 1.534 0 0 0 2.226-1.617l-.863-5.03L20.537 9.2a1.523 1.523 0 0 0 .387-1.575Z"
                  />
                </svg>
              </div>
            </a>
          </div>
        </div>
      </div>
    </div>

    <div class="bg-white pt-10">
      <div class="flex justify-center text-center align-center px-10">
        <h4 class="flex text-3xl md:text-4xl font-bold text-black">
          Add your service to our list
        </h4>
      </div>
      <div class="max-w-4xl mx-auto mt-8">
        <form
          @submit.prevent="saveForm"
          class="px-5 sm:px-0 grid  grid-cols-1 sm:grid-cols-2  gap-6"
        >
          <!-- Left Side -->
          <div class="mb-4  ">
            <label for="name" class="block text-gray-600">Name</label>
            <input
              v-model="formData.name"
              type="text"
              id="name"
              name="name"
              class="w-full mt-1 p-2 border border-gray-300 rounded-md"
            />

            <label for="email" class="block text-gray-600 mt-4">Email</label>
            <input
              v-model="formData.email"
              type="email"
              id="email"
              name="email"
              class="w-full mt-1 p-2 border border-gray-300 rounded-md"
            />

            <label for="url" class="block text-gray-600 mt-4">URL</label>
            <input
              v-model="formData.url"
              type="url"
              id="url"
              name="url"
              class="w-full mt-1 p-2 border border-gray-300 rounded-md"
            />
          </div>

          <!-- Right Side -->
          <div class="mb-4   ">
            <label for="category" class="block text-gray-600  "
              >Category</label
            >
            <select
              v-model="formData.category"
              id="category"
              name="category"
              class="w-full mt-1 p-2 border border-gray-300 rounded-md"
            >
              <option value="category1">Category 1</option>
              <option value="category2">Category 2</option>
              <option value="category3">Category 3</option>
              <!-- Add more categories as needed -->
            </select>
            <label for="shortDescription" class="mt-4 block text-gray-600"
              >Short Description</label
            >
            <textarea
              v-model="formData.shortDescription"
              id="shortDescription"
              name="shortDescription"
              rows="4"
              class="w-full mt-1 p-2 border border-gray-300 rounded-md"
            ></textarea>
          </div>

          <!-- Submit Button -->
          <div class=" flex justify-center  sm:col-span-2  mt-4">
            <button
              type="submit"
              class="px-20 text-center p-2 bg-gray-700 text-white rounded-md hover:bg-gray-900"
            >
              Submit
            </button>
          </div>  
        </form>
      </div>
    </div>
    <div
      class="px-4 py-6 md:flex md:items-center md:justify-between mx-auto px-5 sm:px-10 md:px-20 lg:px-40 pb-5"
    >
      <span class="text-sm text-gray-500 dark:text-gray-300 sm:text-center">
        © 2024 Not affiliated with Stripe™.
      </span>
      <div
        class="flex mt-4 sm:justify-center md:mt-0 space-x-5 rtl:space-x-reverse"
      >
        <a
          href="#"
          class="text-gray-400 hover:text-gray-900 dark:hover:text-white"
        >
          <svg
            class="w-4 h-4"
            aria-hidden="true"
            xmlns="http://www.w3.org/2000/svg"
            fill="currentColor"
            viewBox="0 0 8 19"
          >
            <path
              fill-rule="evenodd"
              d="M6.135 3H8V0H6.135a4.147 4.147 0 0 0-4.142 4.142V6H0v3h2v9.938h3V9h2.021l.592-3H5V3.591A.6.6 0 0 1 5.592 3h.543Z"
              clip-rule="evenodd"
            />
          </svg>
          <span class="sr-only">Facebook page</span>
        </a>
        <a
          href="#"
          class="text-gray-400 hover:text-gray-900 dark:hover:text-white"
        >
          <svg
            class="w-4 h-4"
            aria-hidden="true"
            xmlns="http://www.w3.org/2000/svg"
            fill="currentColor"
            viewBox="0 0 20 17"
          >
            <path
              fill-rule="evenodd"
              d="M20 1.892a8.178 8.178 0 0 1-2.355.635 4.074 4.074 0 0 0 1.8-2.235 8.344 8.344 0 0 1-2.605.98A4.13 4.13 0 0 0 13.85 0a4.068 4.068 0 0 0-4.1 4.038 4 4 0 0 0 .105.919A11.705 11.705 0 0 1 1.4.734a4.006 4.006 0 0 0 1.268 5.392 4.165 4.165 0 0 1-1.859-.5v.05A4.057 4.057 0 0 0 4.1 9.635a4.19 4.19 0 0 1-1.856.07 4.108 4.108 0 0 0 3.831 2.807A8.36 8.36 0 0 1 0 14.184 11.732 11.732 0 0 0 6.291 16 11.502 11.502 0 0 0 17.964 4.5c0-.177 0-.35-.012-.523A8.143 8.143 0 0 0 20 1.892Z"
              clip-rule="evenodd"
            />
          </svg>
          <span class="sr-only">Twitter page</span>
        </a>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import fList from "./featuresList.json";
import sList from "./sitesList.json";

const featuresList = ref(fList);
const filteredSitesList = ref([]);

const activeCat = ref(-1);
const searchText = ref("");
const activeFeature = ref(-1);

const allFeatures = ref([]);

const setactiveCat = (i) => {
  activeCat.value = i;
};
const setactiveFeature = (i) => {
  activeFeature.value = i;
};

const formData = ref({
  name: "",
  email: "",
  shortDescription: "",
  url: "",
  category: "category1", // Set a default category
});

const saveForm = () => {
  // Implement your save logic here using formData.value
  console.log("Form data submitted:", formData.value);
  // Reset form data after submission
  formData.value = {
    name: "",
    email: "",
    shortDescription: "",
    url: "",
    category: "category1",
  };
};

const selectedCategory = ref(null);

const onCatClick = (item, index) => {
  selectedCategory.value = item;

  setactiveCat(index);
  filteredSitesList.value = [];
  setactiveFeature(-1);

  filterArray(item.name || "All", "All");
};

const filterArray = (type, feature) => {
  let x = sList.filter((item) => {
    const isTypeMatch = type === "All" || item.type === type;
    const isFeatureMatch =
      feature === "All" ||
      item.features.join(" ").toLowerCase().includes(feature.toLowerCase());

    return isTypeMatch && isFeatureMatch;
  });

  filteredSitesList.value = x;
};

const searchByText = () => {
  activeCat.value = -1;

  activeFeature.value = -1;

  const st = searchText.value.toLowerCase();

  let x = sList.filter((item) => {
    const allFeatures = item.features.join(" ").toLowerCase();

    // Check if the search text is present in the name or features
    return item.name.toLowerCase().includes(st) || allFeatures.includes(st);
  });

  filteredSitesList.value = x;
};

const onFeatureClick = (feature, index) => {
  setactiveFeature(index);

  let category = selectedCategory.value?.name || "All";
  filterArray(category, feature);
};
const extractAllFeatures = () => {
  allFeatures.value = featuresList.value.flatMap((group) => group.features);
  filteredSitesList.value = sList;
};

onMounted(extractAllFeatures);

const setStars = (v) => {
  return Array.from({ length: 5 }, (_, index) =>
    index < v ? "yellow" : "gray"
  );
};
</script>

<style>
.completed {
  text-decoration: line-through;
}
</style>
