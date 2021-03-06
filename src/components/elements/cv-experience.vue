<template>
  <article class="al-cv-experience">
    <header>
      <div>
        <h2 class="exp-title">
          <b>{{ experience.title | i18n }}</b>
        </h2>
        <span class="exp-org">
          <cv-link
            v-if="experience.organisation.url"
            :url="experience.organisation.url"
          >{{ experience.organisation.name }}</cv-link>
          <span v-else>{{ experience.organisation.name }}</span>
        </span>
      </div>

      <div>
        <span class="exp-location">{{ experience.location | i18n }}</span>
        <span class="exp-date">{{ experience.date.start | i18n }} – {{ experience.date.end | i18n }}</span>
      </div>
    </header>

    <main>
      <p class="experience-description">{{ experience.description | i18n }}</p>
    </main>

    <footer>
      <template v-if="experience.roles">
        <span class="footer-key">Roles</span>
        <span class="footer-value">{{ experience.roles | i18n }}</span>
      </template>
      <template v-if="experience.skills">
        <span class="footer-key">Tech</span>
        <span class="footer-value">{{ experience.skills | i18n }}</span>
      </template>
    </footer>
  </article>
</template>

<script lang="ts">
import { defineComponent } from "@vue/composition-api";

import { CvExperience } from "@/models";
import CvLink from "./cv-link.vue";

interface Props {
  experience: CvExperience;
}

export default defineComponent({
  name: "cv-experience",
  components: { CvLink },
  props: {
    experience: { type: Object, required: true },
  },

  setup() {
    return {};
  },
});
</script>

<style lang="scss">
.al-cv-experience {
  header {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: space-between;
    margin-bottom: multiply(al-cv-base-size, 0.25);

    & > :last-child {
      width: 100%;
    }
  }

  .exp-title {
    display: inline-block;
    color: var(--al-cv-color-primary);
    font-weight: bold;
    transition: color 0.2s;
  }

  h3 {
    margin-bottom: multiply(al-cv-base-size, 0.5);
  }

  .exp-org {
    display: inline-block;
    width: 100%;

    &::before {
      margin-right: multiply(al-cv-base-size, 0.25);
      content: "@";
    }

    @include print-and-tablet {
      width: auto;
      margin-left: multiply(al-cv-base-size, 0.5);
    }
  }

  .exp-location {
    border-right: 1px solid var(--al-cv-color-primary);
    padding-right: multiply(al-cv-base-size, 0.5);
    margin-right: multiply(al-cv-base-size, 0.5);
  }

  .exp-date {
    transition: color 0.2s;
  }

  main {
    margin: multiply(al-cv-base-size, 0.25) 0;
    color: var(--al-cv-color-on-surface-disabled);
  }

  footer {
    display: grid;
    gap: 0 multiply(al-cv-base-size, 0.5);
    grid-template-columns: max-content auto;
    margin-top: multiply(al-cv-base-size, 0.5);
    border-left: 3px solid var(--al-cv-color-secondary);
    padding-left: multiply(al-cv-base-size, 0.75);
    font-style: italic;
    transition: border-left 0.2s;

    @include print-and-tablet {
      padding-left: multiply(al-cv-base-size, 1.5);
    }

    .footer-key {
      &::after {
        color: var(--al-cv-color-on-surface);
        content: ": ";
      }
    }
  }

  &:hover,
  &:focus {
    .exp-title {
      color: var(--al-cv-color-primary-dark);
    }

    .exp-date {
      color: var(--al-cv-color-secondary-dark);
    }

    footer {
      border-left: 3px solid var(--al-cv-color-secondary-dark);
    }
  }
}

.al-cv-experience + .al-cv-experience {
  margin-top: multiply(al-cv-base-size, 2);
}

@include print-and-tablet {
  .al-cv-experience {
    header {
      & > :last-child {
        width: auto;
      }
    }
  }
}

@media print {
  .al-cv-experience {
    // .exp-date {
    //   color: var(--al-cv-color-secondary);
    // }

    main {
      // margin: multiply(al-cv-base-size, 0.25) 0;
      margin: 0;
    }

    footer {
      border-left: 2px solid var(--al-cv-color-secondary);
      line-height: multiply(al-cv-font-size-m, 1.5);
    }

    &:hover,
    &:focus {
      .exp-title {
        color: var(--al-cv-color-primary);
      }

      footer {
        border-left: 3px solid var(--al-cv-color-secondary);
      }
    }
  }

  .al-cv-experience + .al-cv-experience {
    margin-top: multiply(al-cv-base-size, 0.75);
  }
}
</style>
