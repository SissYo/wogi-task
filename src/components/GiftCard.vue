<template>
  <div class="columns">
    <brand-info
      class="column is-6-tablet is-3-desktop pb-0 mx-2 mb-5 pt-5"
      :data="brandInfo"
    ></brand-info>
    <gift-info class="column is-6-tablet mx-2 mb-5 pt-5"></gift-info>
  </div>
</template>

<script>
import BrandInfo from "@/components/BrandInfo";
import GiftInfo from "@/components/GiftInfo";

export default {
  name: "GiftCard",
  data() {
    return {
      brandInfo: null,
    };
  },
  components: {
    BrandInfo,
    GiftInfo,
  },
  mounted() {
    this.axios.get("https://api.mocki.io/v1/5c1d3f35").then((response) => {
      console.log(response);
      this.brandInfo = response.data;
    });
  },
};
</script>

<style scoped>
.column {
  border: 1px solid whitesmoke;
  box-shadow: 0 6px 20px 0 rgba(0, 0, 0, 0.1);
  background-color: white;
}

.columns {
  justify-content: center;
}
</style>
