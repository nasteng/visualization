<template>
  <div></div>
</template>
<script>
const MAX_SALES_BAR_HEIGHT_PER_PRODUCT = 50

export default {
  props: {
    google: {
      required: true,
      type: Object,
    },
    map: {
      required: true,
      type: Object,
    },
    store: {
      required: true,
      type: Object,
    },
  },

  data() {
    return {
      currentBarHeight: 0,
    }
  },

  methods: {
    makeInfoWindow() {
      let content = `<h1>${this.store.name}</h1>`

      this.store.products.forEach(function(item) {
        content += `<p>${item.name}：¥${item.salesAmount.toLocaleString()}</p>`
      })

      return new this.google.maps.InfoWindow({
        content: content,
      })
    },

    totalSalesBarHeight() {
      const height = this.store.products.reduce((prev, product) => {
        return prev + MAX_SALES_BAR_HEIGHT_PER_PRODUCT * product.salesRatio
      }, 0)

      return height
    },

    makeSalesBarGraph(width, height) {
      console.log(this.currentBarHeight)
      let svg = `<svg xmlns="http://www.w3.org/2000/svg" version="1.1" width="10" height="${this.totalSalesBarHeight()}">`

      this.store.products.forEach((product) => {
        const productHeight =
          MAX_SALES_BAR_HEIGHT_PER_PRODUCT * product.salesRatio
        svg += `<rect x="0" y="${this.currentBarHeight}" width="${width}" height="${productHeight}" fill="${product.rgb}" />`
        this.currentBarHeight += productHeight
      })

      svg += "</svg>"

      return {
        url: `data:image/svg+xml,${encodeURIComponent(svg)}`,
        scaledSize: this.google.maps.Size(width, height),
      }
    },
  },

  mounted() {
    const store = new this.google.maps.Marker({
      position: {
        lat: this.store.lat,
        lng: this.store.lng,
      },
      marker: this.store,
      map: this.map,
      icon: this.makeSalesBarGraph(10, this.totalSalesBarHeight()),
    })

    const infoWindow = this.makeInfoWindow()

    store.addListener("click", () => {
      infoWindow.open(this.map, store)
    })
  },
}
</script>
