<template>
  <ul class="sizes sizes--primery" v-if="currentPropId != 7">
    <li class="sizes__item" v-for="(item, index) in products" :key="item.id">
      <label class="sizes__label ">
        <input
          class="sizes__radio sr-only"
          type="radio"
          :name="item.id"
          :checked="index === 0"
          :value="item.price"
          @change.prevent="updatePrice(item.id, item.price)"
        />
        <span class="sizes__value">
          {{ item.propValues[0].value }}
        </span>
      </label>
    </li>
  </ul>
  <ul class="colors colors--black" v-else-if="currentPropId == 7">
    <li class="colors__item" v-for="(item, index) in products" :key="item.id">
      <label class="colors__label">
        <input
          class="colors__radio sr-only"
          type="radio"
          :name="item.id"
          :value="index"
          v-model="pickedColor"
          @change.prevent="updatePrice(item.id, item.price)"
        />
        <span
          class="colors__value"
          :style="{ 'background-color': getColorCode(item.propValues[0].value) }"
        >
        </span>
      </label>
    </li>
  </ul>
</template>

<script>
import getColorCode from "@/helpers/getColorCode";

export default {
  name: "MainPropPicker",
  data() {
    return {
      currentPrice: "",
      pickedColor: null
    };
  },
  props: ["products", "priceUpdate", "currentProp", "currentPropId"],
  methods: {
    getColorCode,
    updatePrice(id, price) {
      this.$emit("update:currentProp", id);
      this.$emit("update:priceUpdate", price);
    }
  },
  created() {
    this.currentPrice = this.products[0].price;
  },
  mounted() {
    this.pickedColor = 0;
  }
};
</script>
