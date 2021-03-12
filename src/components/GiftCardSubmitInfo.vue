<template>
  <section>
    <b-modal :active.sync="isActive" has-modal-card :on-cancel="closeModal">
      <div class="modal-card">
        <header class="modal-card-head">
          <p class="modal-card-title">Gift card information</p>
        </header>
        <section class="modal-card-body">
          <div>
            Gift amount:
            {{ data.amount == "custom" ? data.customAmount : data.amount }}
          </div>
          <div>Delivery type: {{ data.deliveryType }}</div>
          <div v-if="data.deliveryType == 'gift'">
            <div>Sender name: {{ data.senderName }}</div>
            <div>Recipient name: {{ data.recipientName }}</div>
          </div>
          <div>Recipient email: {{ data.recipientEmail }}</div>
          <div>Recipient phone: {{ data.recipientPhone }}</div>
          <div>
            Delivery date:
            {{
              data.deliveryTime == "custom" && data.deliveryDate
                ? `${data.deliveryDate.toDateString()}, ${data.period}`
                : data.deliveryTime
            }}
          </div>
          <div v-if="data.deliveryType == 'gift'">
            Gift message: {{ data.message }}
          </div>
        </section>
      </div>
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
  props: ["data"],
  methods: {
    openModal() {
      this.isActive = true;
    },
    closeModal() {
      this.isActive = false;
    },
  },
};
</script>
