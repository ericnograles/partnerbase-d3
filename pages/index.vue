<template>
  <div class="c-landing">
    <div>
      <visualization :graph="{}" @selected="onSelect"/>
    </div>
    <div v-if="selectedCompany" class="c-landing__sidebar">
      <span class="c-landing__sidebar__header">
        <span class="c-landing__sidebar__header__icon o-rounded-image">
          <!-- <clearbit-logo :domain="selectedCompany.website" class="o-rounded-image__img"/> -->
        </span>
        {{ selectedCompany.name }}
      </span>
      <div class="c-landing__sidebar__details">SIDEBAR!
        <div class="c-landing__sidebar__details__item">
          <span class="c-landing__sidebar__details__item__label">Location:</span>
          <span class="c-landing__sidebar__details__item__value">{{ selectedCompany.location }}</span>
        </div>

        <div class="c-landing__sidebar__details__item">
          <span class="c-landing__sidebar__details__item__label">Employees:</span>
          <span class="c-landing__sidebar__details__item__value">{{ selectedCompany.employees }}</span>
        </div>

        <div class="c-landing__sidebar__details__item">
          <span class="c-landing__sidebar__details__item__label">Founded:</span>
          <span class="c-landing__sidebar__details__item__value">{{ selectedCompany.founded }}</span>
        </div>

        <div class="c-landing__sidebar__details__item">
          <span class="c-landing__sidebar__details__item__label">Website:</span>
          <span class="c-landing__sidebar__details__item__value">
            <a
              :href="`//${selectedCompany.website}?source=partnerbase`"
              target="_blank"
              class="u-details-grid-item"
            >{{ selectedCompany.website }}</a>
          </span>
        </div>

        <div class="c-landing__sidebar__details__item">
          <span class="c-landing__sidebar__details__item__label">Industry:</span>
          <span class="c-landing__sidebar__details__item__value">{{ selectedCompany.industry }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Visualization from "~/components/Visualization";

export default {
  name: "Homepage",
  components: {
    Visualization
  },
  data() {
    return {
      selectedCompany: null
    };
  },
  head() {
    return {
      title: "Partnerbase · B2B Partnerships and Alliances Directory",
      meta: [
        {
          hid: "description",
          name: "description",
          content: `
            Partnerbase is on a mission to catalog and analyze the
            relationships between B2B companies. This includes product
            partnerships, go-to-market alliances, channel sales partnerships,
            and more. Use Partnerbase to find partnership information, study
            partner ecosystems, and add new partnerships to our always-growing
            data set.
          `
        }
      ]
    };
  },
  methods: {
    onSelect(data) {
      this.selectedCompany = data;
      console.log(this.selectedCompany);
    }
  }
};
</script>