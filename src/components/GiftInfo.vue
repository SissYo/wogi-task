<template>
  <div>
    <ValidationObserver ref="giftForm">
      <div id="gift-form" class="section">
        <h3 class="has-text-weight-semibold gift-title">Gift information</h3>
        <b-field
          id="amount-field"
          label="Select gift amount"
          custom-class="has-text-dark has-text-weight-medium"
          :class="[form.amount == 'custom' ? 'mb-4' : 'parent-field']"
          grouped
          group-multiline
        >
          <b-radio-button
            v-for="(item, index) in amounts"
            :key="index"
            v-model="form.amount"
            :native-value="item.value"
            type="is-info"
            class="mr-3 radio-button has-text-dark has-text-weight-medium"
            >{{ item.label }}</b-radio-button
          >
        </b-field>
        <ValidationProvider
          v-if="form.amount == 'custom'"
          rules="required"
          name="gift amount"
          v-slot="{ errors }"
        >
          <b-field id="custom-amount-field" class="parent-field">
            <p class="control">
              <span class="button is-static has-background-white">$</span>
            </p>
            <b-input
              v-model="form.customAmount"
              placeholder="Enter custom amount"
            ></b-input>
          </b-field>
          <span
            v-for="error in errors"
            :key="error.id"
            class="help has-text-danger custom-amount-error"
            >{{ error }}</span
          >
        </ValidationProvider>
        <b-field
          label="Delivery type"
          class="mt-5 parent-field"
          custom-class="has-text-dark has-text-weight-medium"
        >
          <b-radio
            v-for="(item, index) in deliveryTypes"
            :key="index"
            v-model="form.deliveryType"
            :native-value="item.value"
            type="is-info"
            class="mr-5 has-text-dark has-text-weight-normal"
            >{{ item.label }}</b-radio
          >
        </b-field>
        <b-field
          v-if="form.deliveryType == 'gift'"
          grouped
          group-multiline
          class="is-flex is-justify-content-space-evenly"
        >
          <ValidationProvider
            rules="required"
            name="sender name"
            v-slot="{ errors }"
          >
            <b-field
              label="Sender name"
              class="parent-field"
              custom-class="has-text-dark has-text-weight-medium"
              expanded
            >
              <b-input
                v-model="form.senderName"
                placeholder="Enter sender name"
                expanded
              ></b-input>
            </b-field>
            <span
              v-for="error in errors"
              :key="error.id"
              class="help has-text-danger mb-5"
              >{{ error }}</span
            >
          </ValidationProvider>
          <ValidationProvider
            rules="required"
            name="recipient name"
            v-slot="{ errors }"
          >
            <b-field
              label="Recipient name"
              class="parent-field"
              custom-class="has-text-dark has-text-weight-medium"
              expanded
            >
              <b-input
                v-model="form.recipientName"
                placeholder="Enter recipient name"
                expanded
              ></b-input>
            </b-field>
            <span
              v-for="error in errors"
              :key="error.id"
              class="help has-text-danger mb-5"
              >{{ error }}</span
            >
          </ValidationProvider>
        </b-field>
        <b-field grouped group-multiline>
          <ValidationProvider
            rules="required"
            name="recipient email"
            v-slot="{ errors }"
          >
            <b-field
              label="Recipient email"
              class="parent-field"
              custom-class="has-text-dark has-text-weight-medium"
            >
              <b-input
                v-model="form.recipientEmail"
                placeholder="Enter recipient email"
                expanded
              ></b-input>
            </b-field>
            <span
              v-for="error in errors"
              :key="error.id"
              class="help has-text-danger mb-5"
              >{{ error }}</span
            >
          </ValidationProvider>
          <ValidationProvider
            rules="required"
            name="recipient phone"
            v-slot="{ errors }"
          >
            <b-field
              label="Recipient phone"
              class="parent-field"
              custom-class="has-text-dark has-text-weight-medium"
            >
              <p class="control">
                <span class="button is-static has-background-white">+65</span>
              </p>
              <b-input
                v-model="form.recipientPhone"
                placeholder="Enter recipient phone"
                expanded
              ></b-input>
            </b-field>
            <span
              v-for="error in errors"
              :key="error.id"
              class="help has-text-danger mb-5"
              >{{ error }}</span
            >
          </ValidationProvider>
        </b-field>
        <div v-if="form.deliveryType == 'gift'">
          <b-field
            label="Delivery time"
            custom-class="has-text-dark has-text-weight-medium"
            class="parent-field"
          >
            <b-radio
              v-for="(item, index) in deliveryTimes"
              :key="index"
              v-model="form.deliveryTime"
              :native-value="item.value"
              type="is-info"
              class="mr-5 has-text-dark has-text-weight-normal"
              >{{ item.label }}</b-radio
            >
          </b-field>
          <b-field v-if="form.deliveryTime == 'custom'" grouped group-multiline>
            <ValidationProvider
              rules="required"
              name="delivery date"
              v-slot="{ errors }"
            >
              <b-field
                label="Delivery date"
                class="parent-field"
                custom-class="has-text-dark has-text-weight-medium"
              >
                <b-datepicker
                  placeholder="Select delivery date"
                  icon="calendar-today"
                  :min-date="new Date()"
                  editable
                  class="has-icons-right"
                  v-model="form.deliveryDate"
                >
                </b-datepicker>
              </b-field>
              <span
                v-for="error in errors"
                :key="error.id"
                class="help has-text-danger mb-5"
                >{{ error }}</span
              >
            </ValidationProvider>
            <b-field
              id="period-field"
              label="Period"
              class="parent-field"
              custom-class="has-text-dark has-text-weight-medium"
            >
              <b-radio-button
                v-for="(item, index) in periods"
                :key="index"
                v-model="form.period"
                :native-value="item.value"
                type="is-info"
                class="mr-3 radio-button has-text-dark has-text-weight-medium"
                >{{ item.label }}</b-radio-button
              >
            </b-field>
          </b-field>
          <ValidationProvider
            rules="required"
            name="gift message"
            v-slot="{ errors }"
          >
            <b-field
              label="Gift message"
              custom-class="has-text-dark has-text-weight-medium"
              class="parent-field"
            >
              <b-input
                v-model="form.message"
                type="textarea"
                class="is-info"
                placeholder="Enter gift message"
              ></b-input>
            </b-field>
            <span
              v-for="error in errors"
              :key="error.id"
              class="help has-text-danger"
              >{{ error }}</span
            >
          </ValidationProvider>
        </div>
        <b-field class="is-flex is-justify-content-flex-end parent-field">
          <b-button class="is-info" @click="sendGift">Send</b-button>
        </b-field>
      </div>
    </ValidationObserver>
    <gift-card-submit-info :data="form" ref="cardModal"></gift-card-submit-info>
  </div>
</template>
<script>
import GiftCardSubmitInfo from "@/components/GiftCardSubmitInfo";
export default {
  name: "GitInfo",
  data() {
    return {
      form: {
        amount: "30",
        customAmount: "",
        deliveryType: "personal",
        deliveryTime: "immediately",
        period: "afternoon",
        senderName: "",
        recipientName: "",
        recipientEmail: "",
        message: "",
        deliveryDate: null,
        recipientPhone: null,
      },
      amounts: [
        {
          label: "$10",
          value: "10",
        },
        {
          label: "$20",
          value: "20",
        },
        {
          label: "$30",
          value: "30",
        },
        {
          label: "$40",
          value: "40",
        },
        {
          label: "Custom",
          value: "custom",
        },
      ],
      deliveryTypes: [
        {
          label: "Personal",
          value: "personal",
        },
        {
          label: "Send as gift",
          value: "gift",
        },
      ],
      deliveryTimes: [
        {
          label: "Immediately",
          value: "immediately",
        },
        {
          label: "Custom",
          value: "custom",
        },
      ],
      periods: [
        {
          label: "Morning",
          value: "morning",
        },
        {
          label: "Afternoon",
          value: "afternoon",
        },
        {
          label: "Evening",
          value: "evening",
        },
      ],
    };
  },
  components: { GiftCardSubmitInfo },
  methods: {
    sendGift() {
      this.$refs.giftForm.validate().then((valid) => {
        if (!valid) {
          return this.$buefy.toast.open({
            message: "Please fill in all fields",
            type: "is-danger",
          });
        }

        this.$refs.cardModal.openModal();
      });
    },
  },
};
</script>

<style scoped>
.section {
  padding: 0 !important;
}

.help {
  margin-top: -2rem;
}
</style>

<style>
#amount-field,
#period-field label {
  border-radius: 4px !important;
}
</style>
