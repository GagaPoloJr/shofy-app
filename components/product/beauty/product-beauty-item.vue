<template>
  <div
    :class="`tp-product-item-3 ${
      primary_style ? 'tp-product-style-primary' : ''
    } mb-50 ${isCenter ? 'text-center' : ''}`"
  >
    <div
      class="tp-product-thumb-3 mb-15 fix p-relative z-index-1"
      :style="`background-color: ${style_2 ? '#f6f6f6' : '#fff'};`"
    >
      <nuxt-link :href="`/product-details/${item.id}`">
        <img :src="item.img" alt="product-img" />
      </nuxt-link>

      <!-- product action -->
      <div class="tp-product-action-3 tp-product-action-blackStyle">
        <div class="tp-product-action-item-3 d-flex flex-column">
          <button
            v-if="!cartStore.cart_products.some((prd) => prd.id === item.id)"
            @click="cartStore.addCartProduct(item)"
            type="button"
            :class="`tp-product-action-btn-3 tp-product-add-cart-btn ${
              cartStore.cart_products.some((prd) => prd.id === item.id)
                ? 'active'
                : ''
            }`"
          >
            <svg-cart-bag-2 />
            <span class="tp-product-tooltip">Add to Cart</span>
          </button>
          <nuxt-link
            v-if="cartStore.cart_products.some((prd) => prd.id === item.id)"
            @click="cartStore.addCartProduct(item)"
            href="/cart"
            :class="`tp-product-action-btn-3 tp-product-add-cart-btn ${
              cartStore.cart_products.some((prd) => prd.id === item.id)
                ? 'active'
                : ''
            }`"
          >
            <svg-cart-bag-2 />
            <span class="tp-product-tooltip">View Cart</span>
          </nuxt-link>

          <button
            type="button"
            class="tp-product-action-btn-3 tp-product-quick-view-btn"
            data-bs-toggle="modal"
            :data-bs-target="`#${utilityStore.modalId}`"
            @click="
              utilityStore.handleOpenModal(`product-modal-${item.id}`, item)
            "
          >
            <svg-quick-view />
            <span class="tp-product-tooltip">Quick View</span>
          </button>
          <button
            @click="wishlistStore.add_wishlist_product(item)"
            type="button"
            :class="`tp-product-action-btn-3 tp-product-add-to-wishlist-btn ${
              wishlistStore.wishlists.some((prd) => prd.id === item.id)
                ? 'active'
                : ''
            }`"
          >
            <svg-wishlist />
            <span class="tp-product-tooltip">Add To Wishlist</span>
          </button>
          <a
            :href="item.shopeeLink"
            target="_blank"
            type="button"
            class="tp-product-action-btn tp-product-quick-view-btn"
          >
            <img class="icon" width="20" src="/img/icon/sp.png" alt="" />
            <!-- <svg-wishlist /> -->
            <span class="tp-product-tooltip">View Product</span>
          </a>
        </div>
      </div>

      <div class="tp-product-add-cart-btn-large-wrapper">
        <button
          @click="cartStore.addCartProduct(item)"
          type="button"
          class="tp-product-add-cart-btn-large"
        >
          Add To Cart
        </button>
      </div>
    </div>
    <div class="tp-product-content-3">
      <div class="tp-product-tag-3">
        <span>{{ item.category.name }}</span>
      </div>
      <h3 class="tp-product-title-3">
        <nuxt-link :href="`/product-details/${item.id}`">{{
          item.title
        }}</nuxt-link>
      </h3>
      <div class="tp-product-price-wrapper-3">
        <span class="tp-product-price-3">${{ item.price.toFixed(2) }}</span>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { useCompareStore } from "@/pinia/useCompareStore";
import { useCartStore } from "@/pinia/useCartStore";
import { useWishlistStore } from "@/pinia/useWishlistStore";
import { useUtilityStore } from "@/pinia/useUtilityStore";
import { IProduct } from "@/types/product-type";
// props
defineProps<{
  item: IProduct;
  style_2?: boolean;
  isCenter?: boolean;
  primary_style?: boolean;
}>();

const compareStore = useCompareStore();
const cartStore = useCartStore();
const wishlistStore = useWishlistStore();
const utilityStore = useUtilityStore();
</script>

<style scoped>
.tp-product-action-btn .icon {
  width: 20px !important;
}
</style>
