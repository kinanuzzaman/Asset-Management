<template>
  <div>
    <q-layout>
      <div>
        <div class="q-ml-md">
          <q-input
            label="Search"
            label-color="primary"
            class="q-mr-xl"
            v-model="search"
            type="text"
            @keyup.enter="getProduct(search)"
            hint="Numeric Product Number"
          >
            <template v-slot:append>
              <q-icon name="search" />
            </template>
          </q-input>
        </div>
        <div>
          <p class="bg-grey-4 q-mt-md q-pa-md">Product Details</p>
          <!--  v-for="(product, index) in products" :key="index"-->
          <q-list>
            <q-item>
              <q-item-section>
                <q-item-label v-model="brand">
                  {{ brand }}
                </q-item-label>
                <q-item-label v-model="model">
                  {{ model }}
                </q-item-label>
                <q-item-label v-model="description">
                  {{ description }}</q-item-label
                >
              </q-item-section>
            </q-item>
          </q-list>
        </div>
        <q-btn
          type="submit"
          @click="assignProduct(search)"
          class="q-ma-md"
          color="blue"
          text-color="white"
          unelevated
          label="Assign"
          no-caps
        />
        <!-- :to="`/main/users/details/${id}`" -->
      </div>
    </q-layout>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      id: this.$route.params.id,
      search: "",
      products: null,
      user_id: "",
      brand: "",
      model: "",
      description: "",
    };
  },
  created() {},
  methods: {
    getProduct(search) {
      const options = {
        method: "GET",
        url: "http://127.0.0.1:8000/api/products/" + search,
        headers: {
          Authorization: "Bearer 3|e8jVTwx52A5yiSG49aWocTuWvBnrfc4NRL7TQEeL",
        },
      };

      axios
        .request(options)
        .then((response) => {
          console.log(response.data);
          this.products = response.data.data;
          this.user_id = response.data.data.id;
          this.brand = response.data.data.attributes.brand;
          this.model = response.data.data.attributes.model;

          this.description = response.data.data.attributes.description;
        })
        .catch(function (error) {
          console.error(error);
        });
    },
    assignProduct(search) {
      const options = {
        method: "PATCH",
        url: "http://127.0.0.1:8000/api/products/assign/" + search,
        data: {
          user_id: this.user_id,
        },
        headers: {
          Authorization: "Bearer 3|e8jVTwx52A5yiSG49aWocTuWvBnrfc4NRL7TQEeL",
        },
      };

      axios
        .request(options)
        .then((response) => {
          console.log(response.data);
          this.products = response.data;
        })
        .catch(function (error) {
          console.error(error);
        });
    },
  },
};
</script>
