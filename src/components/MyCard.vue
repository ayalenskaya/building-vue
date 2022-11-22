<script>
import { reactive } from "vue";

export default {
  props: [
    "code",
    "productId",
    "priceGoldAlt",
    "priceRetailAlt",
    "priceRetail",
    "primaryImageUrl",
    "assocProducts",
    "product",
  ],
  setup() {
    const state = reactive({ amount: 1 });
    const active = reactive({ activeEl: 1 });

    const decrement = () => {
      if (state.amount > 1) {
        state.amount -= 1;
      }
    };

    const increment = () => {
      state.amount += 1;
    };

    const computedUrl = (url) => {
      return `${url.slice(0, -4)}_220x220_1${url.slice(-4)}`;
    }; //косяк сервера, не работает

    return {
      active,
      state,
      decrement,
      increment,
      computedUrl,
    };
  },
};
</script>
<template>
  <!--  <div >-->
  <li class="products_page pg_0">
    <div class="product product_horizontal">
      <span class="product_code">Код: {{ product.code.substr(5, 11) }}</span>
      <div class="product_status_tooltip_container">
        <span class="product_status">Наличие</span>
      </div>
      <div class="product_photo">
        <a class="url--link product__link" href="#">
          <img :src="product.primaryImageUrl" />
        </a>
      </div>
      <div class="product_description">
        <a class="product__link" href="#">{{ product.title }}</a>
      </div>
      <div class="product_tags hidden-sm">
        <p>Могут понадобиться:</p>
        <!--          {{ product.assocProducts.split(";\n") }} -->
        {{ product.assocProducts }}
      </div>

      <div class="product_units">
        <div class="unit--wrapper">
          <div
            :class="{ 'unit--active': active.activeEl === 1 }"
            @click="active.activeEl = 1"
            class="unit--select"
          >
            <p class="ng-binding">За м. кв.</p>
          </div>
          <div
            :class="{ 'unit--active': active.activeEl === 2 }"
            @click="active.activeEl = 2"
            class="unit--select"
          >
            <p class="ng-binding">За упаковку</p>
          </div>
        </div>
      </div>
      <div v-if="active.activeEl === 1">
        <p class="product_price_club_card">
          <span class="product_price_club_card_text">По карте<br />клуба</span>
          <span class="goldPrice">{{ Math.floor(product.priceGoldAlt) }}</span>

          <span class="rouble__i black__i"> ₽ </span>
        </p>
        <p class="product_price_default">
          <span class="retailPrice">{{
            // Math.floor(product.priceRetailAlt)
            Math.floor(product.priceRetailAlt)
          }}</span>
          <span class="rouble__i black__i"> ₽ </span>
        </p>
        <div class="product_price_points">
          <p class="ng-binding">
            Можно купить за
            {{ Math.floor(product.priceRetailAlt) }} балла
          </p>
        </div>
        <div class="list--unit-padd"></div>
        <div class="list--unit-desc">
          <div class="unit--info">
            <div class="unit--desc-i"></div>
            <div class="unit--desc-t">
              <p>
                <span class="ng-binding">Продается упаковками:</span>
                <span class="unit--infoInn"
                  >1 упак. = {{ Math.floor(product.priceRetailAlt) }} м. кв.
                </span>
              </p>
            </div>
          </div>
        </div>
      </div>
      <div v-else>
        <p class="product_price_club_card">
          <span class="product_price_club_card_text">По карте<br />клуба</span>
          <span class="goldPrice">{{ Math.floor(product.priceGold) }}</span>
          <span class="rouble__i black__i"> ₽ </span>
        </p>
        <p class="product_price_default">
          <span class="retailPrice">{{ Math.floor(product.priceRetail) }}</span>
          <span class="rouble__i black__i"> ₽ </span>
        </p>
        <div class="product_price_points">
          <p class="ng-binding">
            Можно купить за
            {{ Math.floor(product.priceRetail) }} балла
          </p>
        </div>
        <div class="list--unit-padd"></div>
        <div class="list--unit-desc">
          <div class="unit--info">
            <div class="unit--desc-i"></div>
            <div class="unit--desc-t">
              <p>
                <span class="ng-binding">Продается упаковками:</span>
                <span class="unit--infoInn"
                  >1 упак. = {{ Math.floor(product.priceRetail) }} м. кв.
                </span>
              </p>
            </div>
          </div>
        </div>
      </div>
      <div class="product__wrapper"></div>

      <div class="product_count_wrapper">
        <div class="stepper">
          <input
            :value="state.amount"
            class="product__count stepper-input"
            type="text"
            readonly
          />
          <span @click="increment" class="stepper-arrow up"></span>
          <span
            v-if="state.amount > 0"
            @click="decrement"
            class="stepper-arrow down"
          ></span>
        </div>
      </div>
      <span
        class="btn btn_cart"
        :data-product-id="product.productId"
        data-url="/cart/"
      >
        <span class="ng-binding">В корзину</span>
      </span>
    </div>
  </li>
</template>
<style scoped></style>
