<script>
import MyCard from "@/components/MyCard";
import products from "@/products.json";
export default {
  name: "MyList",
  components: { MyCard },

  setup() {
    return {
      products,
    };
  },
};
</script>
<template>
  <div class="sub_category_page">
    <div class="column_right column_right_products_container">
      <div class="product__area">
        <ul>
          <my-card
            v-for="product in products"
            :product="product"
            :key="product.productId"
          />
        </ul>
      </div>
    </div>
  </div>
</template>
