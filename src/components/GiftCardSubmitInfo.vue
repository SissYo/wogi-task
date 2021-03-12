<template>
  <section>
    <b-modal v-model="isActive">
      <div class="modal-card"></div>
    </b-modal>
  </section>
</template>

<script>
export default {
  name: "GiftCardSubmitInfo",
  data() {
    return {
      isActive: false,
    };
  },
};
</script>
