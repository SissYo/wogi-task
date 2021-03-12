<template>
  <div id="brand-info" v-if="data">
    <div class="logo"><img :src="data.logo" alt="Logo" /></div>
    <hr />
    <div id="name" class="has-text-centered title has-text-weight-semibold">
      {{ data.name }}
    </div>
    <div id="state" class="is-flex is-justify-content-center">
      <b-taglist>
        <b-tag type="is-success is-light has-text-success">{{
          data.state
        }}</b-tag>
      </b-taglist>
    </div>
    <hr />
    <div id="featured-details" class="columns has-text-centered mb-0">
      <div class="country column is-6">
        <div class="subtitle">Country</div>
        <div class="value">{{ data.featuredDetails.country }}</div>
      </div>
      <div class="products column is-6">
        <div class="subtitle">Products</div>
        <div class="value">{{ data.featuredDetails.products }}</div>
      </div>
    </div>
    <hr class="mt-0" />
    <div class="details ml-4">
      <div class="id my-3">
        <div class="subtitle">Id</div>
        <div class="value">{{ data.details.id }}</div>
      </div>
      <div class="company my-3">
        <div class="subtitle">Company</div>
        <div class="value">{{ data.details.company }}</div>
      </div>
      <div class="category my-3">
        <div class="subtitle">Category</div>
        <div class="value">{{ data.details.category }}</div>
      </div>
      <div class="phone my-3">
        <div class="subtitle">Phone</div>
        <div class="value">{{ data.details.phone }}</div>
      </div>
    </div>
    <hr />
    <div class="keywords ml-4 mt-3">
      <div class="subtitle">Keywords</div>
      <b-taglist class="is-align-items-flex-start my-3">
        <b-tag
          class="custom-tabs has-text-weight-medium"
          v-for="(tag, index) in data.keywords.slice(0, 4)"
          :key="index"
          >{{ tag }}</b-tag
        >
        <b-collapse
          v-if="data.keywords.length > 4"
          :open="false"
          position="is-bottom"
          aria-id="keywords"
          class=""
        >
          <template #trigger="props">
            <b-tag type="is-info is-light" aria-controls="keywords">
              <span>+{{ data.keywords.length - 4 }}</span>
              <b-icon
                :icon="!props.open ? 'chevron-down' : 'chevron-up'"
                size="is-small"
              ></b-icon>
            </b-tag>
          </template>
          <b-tag v-for="(tag, index) in data.keywords.slice(4)" :key="index">{{
            tag
          }}</b-tag>
        </b-collapse>
      </b-taglist>
    </div>
    <div id="social-icons" class="is-fixed-bottom">
      <hr />
      <div class="socials is-flex is-justify-content-space-evenly my-3">
        <a class="has-text-grey" :href="data.socials.website"
          ><b-icon icon="web"></b-icon
        ></a>
        <a class="has-text-grey" :href="data.socials.facebook"
          ><b-icon icon="facebook"></b-icon
        ></a>
        <a class="has-text-grey" :href="data.socials.instagram"
          ><b-icon icon="instagram"></b-icon
        ></a>
        <a class="has-text-grey" :href="data.socials.twitter"
          ><b-icon icon="twitter"></b-icon
        ></a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "BrandInfo",
  props: ["data"],
};
</script>

<style scoped>
.custom-tabs {
  margin-bottom: 0 !important;
}

hr {
  margin: 0.7rem 0;
}

.country {
  border-right: 1px solid whitesmoke;
}

.subtitle {
  font-size: 12px;
  margin-bottom: 0 !important;
  color: #898d90;
}

.tag {
  margin-bottom: 0.5rem !important;
}

#featured-details {
  padding-top: 0.25rem;
}
</style>
