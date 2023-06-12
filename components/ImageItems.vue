<script setup>
import pic from "../assets/images/bg.webp";

defineExpose({ search });

const items = ref([]);
const selectedImage = ref(pic);
const activeItem = ref("");
const loading = ref(false);
const emit = defineEmits(["emptyValue"]);

async function search(value) {
  try {
    loading.value = true;
    await useFetch(
      `https://free-food-menus-api-production.up.railway.app/${value}`,
      {
        onResponse(response) {
          items.value = response.response._data;
          emit("emptyValue");
        },
        onResponseError() {
          alert("No Data Found");
        },
      }
    );
  } catch (error) {
  } finally {
    loading.value = false;
  }
}

function selectedItem(value) {
  selectedImage.value = value.img;
  const filteredItem = items.value.find((x) => {
    return x.id === value.id;
  });
  activeItem.value = filteredItem.id;
}
</script>
<template>
  <div class="col-lg-5">
    <div class="d-flex align-items-center justify-content-center vh-100">
      <div class="food-img">
        <img :src="selectedImage" alt="default" />
      </div>
    </div>
  </div>
  <div class="col-lg-3 px-0 all-items">
    <div class="d-flex align-items-center w-100">
      <div v-if="loading">
        <Loader />
      </div>
      <ul v-else class="items">
        <li
          v-for="item in items"
          :key="item.id"
          @click="selectedItem(item)"
          :class="activeItem === item.id ? 'active' : ''"
        >
          <div class="item-content">
            <div class="small-img">
              <img :src="item.img" :alt="item.id" />
            </div>
            <div class="content">
              <h6>{{ item.name }}</h6>
              <p class="text-success">
                <b>{{ item.price }}$</b>
              </p>
              <Rating :ratings="item.rate" />
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>
