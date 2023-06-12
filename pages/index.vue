<script setup>
const search = ref("");
const instance = getCurrentInstance();
function searchItem(value) {
  instance.refs.imageItem.search(value);
}
function onEmptyValue() {
  search.value = "";
}
onMounted(() => {
  instance.refs.searchRef.focus();
});
</script>
<template>
  <div class="container-fluid vh-100 px-0">
    <div class="row px-0 mx-0">
      <div class="col-lg-4">
        <div class="d-flex align-items-center h-100 bg-b-dark">
          <div class="px-5">
            <h1>Food Menu App</h1>
            <p>
              It is a food app developed by
              <span class="text-success"><b>Zeeshan Siddique</b></span> using
              <b>Nuxt 3</b>
            </p>
            <div class="my-5">
              <h4>Description</h4>
              <ul class="description">
                <li>Nuxt 3</li>
                <li>SCSS & Bootstrap 5</li>
                <li>Components & Pages</li>
                <li>
                  Used APIs with nearly 700 dishes and 15 menus (Available
                  listed below items only).
                </li>
                <li>
                  bbqs,best-foods,breads,burgers,chocolates,desserts,drinks,pizzas
                  <span
                    >ice-cream,fried-chicken,porks,sandwiches,sausages,steaks,our-foods</span
                  >
                </li>
              </ul>
            </div>
            <div class="mt-5">
              <div class="input-group">
                <input
                  ref="searchRef"
                  v-model="search"
                  type="text"
                  class="form-control"
                  placeholder="Food Name..."
                />
                <div class="input-group-append">
                  <button
                    class="btn btn-outline-success"
                    type="button"
                    @click="searchItem(search)"
                  >
                    Search
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <ImageItems ref="imageItem" @emptyValue="onEmptyValue" />
    </div>
  </div>
</template>
