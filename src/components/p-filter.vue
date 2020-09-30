<template>
  <div class="p-filters">
    <div class="flex flex-col items-center">
      <p class="p-filters-title">Color</p>
      <select @change="onClickButton" v-model="this.selected.selectedcolor">
        <option value="" selected>All</option>
        <option
          :style="`background-color:${filter.color} `"
          v-for="filter in unique(filters, 'color')"
          :key="filter"
          :value="filter.color"
        >
          {{ filter.color }}
        </option>
      </select>
    </div>
    <div class="flex flex-col justify-center items-center">
      <p class="p-filters-title">Order By</p>
      <div class="flex flex-col md:flex-row justify-center items-center">
        <select @change="onClickButton" v-model="this.selected.sortby">
          <option value="id" selected>
            ID Number&nbsp;

            <span> &#xf577;</span>
          </option>
          <option value="price">
            Price&nbsp;

            <span> &#xf02c;</span>
          </option>
          <option value="createdAt">
            Publish Time&nbsp;
            <span> &#xf274;</span>
          </option>
        </select>

        <select @change="onClickButton" v-model="this.selected.orderby">
          <option value="asc" selected>
            Low To High&nbsp;
            <span> &#xf884;</span>
          </option>
          <option value="desc">High To Low&nbsp;<span> &#xf160;</span></option>
        </select>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      filters: "",
      selected: {
        selectedcolor: "",
        sortby: "id",
        orderby: "asc",
      },
    };
  },

  props: ["pcolor"],

  mounted() {
    this.getfilters();
  },

  methods: {
    async getfilters() {
      const filtersres = await axios.get(
        `https://5f7301beb63868001615f226.mockapi.io/api/products`
      );
      this.filters = filtersres.data;
    },

    onClickButton() {
      this.$emit("clicked", this.selected);
    },
  },

  computed: {
    unique () {
      return function (arr, key) {
        var output = []
        var usedKeys = {}
        for (var i = 0; i < arr.length; i++) {
          if (!usedKeys[arr[i][key]]) {
            usedKeys[arr[i][key]] = true
            output.push(arr[i])
          }
        }
        return output
      }
    }
  },
};
</script>

<style lang="scss">
.p-filters {
  display: flex;
  width: 100%;
  min-height: 100px;
  justify-content: center;
  align-items: center;
  background: #3fffca;

  * {
    margin: 5px 2%;
  }

  .p-filters-title {
    font-weight: 600;
    font-size: 18px;

    color: white;
  }

  select {
    border-radius: 10px;
    padding: 3px 15px;
    outline: none !important;
    font-size: 13px;
    text-align: center;
    text-align-last: center;

    font-family: "Rubik", "Font Awesome 5 Free", "Font Awesome 5 Brands";
    font-weight: 700;
    * {
      font-family: "Rubik", "Font Awesome 5 Free", "Font Awesome 5 Brands";
      text-align: center;
      text-align-last: center;
      font-weight: 700;
    }
  }
}
</style>