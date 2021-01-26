<template>
  <google-map-loader :mapConfig="mapConfig" :apiKey="apiKey">
    <template slot-scope="{ google, map }">
      <google-map-marker
        v-for="store in stores"
        :key="store.id"
        :map="map"
        :google="google"
        :store="store"
      />
    </template>
  </google-map-loader>
</template>

<script>
import GoogleMapLoader from "./GoogleMapLoader.vue"
import GoogleMapMarker from "./GoogleMapMarker.vue"

export default {
  components: { GoogleMapLoader, GoogleMapMarker },
  data() {
    return {
      apiKey: process.env.VUE_APP_GOOGLE_MAP_API_KEY,
      stores: [
        {
          id: 1,
          name: "ほげほげ店",
          lat: 35.69,
          lng: 139.765,
          products: [
            {
              name: "A商品",
              salesAmount: 100000,
              rgb: "#f00",
              salesRatio: 1.0,
            },
            {
              name: "B商品",
              salesAmount: 150000,
              rgb: "#0f0",
              salesRatio: 1.0,
            },
            {
              name: "C商品",
              salesAmount: 200000,
              rgb: "#00f",
              salesRatio: 1.0,
            },
          ],
        },
        {
          id: 2,
          name: "ふがふが店",
          lat: 35.690015,
          lng: 139.761897,
          products: [
            {
              name: "A商品",
              salesAmount: 50000,
              rgb: "#f00",
              salesRatio: 0.5,
            },
            {
              name: "B商品",
              salesAmount: 75000,
              rgb: "#0f0",
              salesRatio: 0.5,
            },
            {
              name: "C商品",
              salesAmount: 100000,
              rgb: "#00f",
              salesRatio: 0.5,
            },
          ],
        },
        {
          id: 3,
          name: "ぴよぴよ店",
          lat: 35.6946,
          lng: 139.76112,
          products: [
            {
              name: "A商品",
              salesAmount: 10000,
              rgb: "#f00",
              salesRatio: 0.1,
            },
            {
              name: "B商品",
              salesAmount: 15000,
              rgb: "#0f0",
              salesRatio: 0.1,
            },
            {
              name: "C商品",
              salesAmount: 20000,
              rgb: "#00f",
              salesRatio: 0.1,
            },
          ],
        },
        {
          id: 4,
          name: "すごすご店",
          lat: 35.684599,
          lng: 139.76551,
          products: [
            {
              name: "A商品",
              salesAmount: 30000,
              rgb: "#f00",
              salesRatio: 0.333,
            },
            {
              name: "B商品",
              salesAmount: 50000,
              rgb: "#0f0",
              salesRatio: 0.333,
            },
            {
              name: "C商品",
              salesAmount: 66666,
              rgb: "#00f",
              salesRatio: 0.333,
            },
          ],
        },
        {
          id: 5,
          name: "やばやば店",
          lat: 35.680997,
          lng: 139.7670936,
          products: [
            {
              name: "A商品",
              salesAmount: 200000,
              rgb: "#f00",
              salesRatio: 2,
            },
            {
              name: "B商品",
              salesAmount: 300000,
              rgb: "#0f0",
              salesRatio: 2,
            },
            {
              name: "C商品",
              salesAmount: 400000,
              rgb: "#00f",
              salesRatio: 2,
            },
          ],
        },
      ],
    }
  },
  computed: {
    mapConfig() {
      return {
        center: {
          // マップの中心は東京駅
          lat: 35.6800156,
          lng: 139.7642828,
        },
        zoom: 14,
      }
    },
  },
}
</script>
