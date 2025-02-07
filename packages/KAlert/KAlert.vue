<template>
  <div
    v-if="isShowing"
    :class="[appearance, size, {'isBordered':isBordered}, {'hasLeftBorder':hasLeftBorder}, {'isCentered': isCentered}, {'isFixed': isFixed}]"
    class="k-alert"
    role="alert">
    <button
      v-if="isDismissible"
      type="button"
      aria-label="Close"
      class="close"
      @click="dismissAlert()">
      <KIcon
        icon="close"
        color="#000"
        size="12"
        view-box="0 0 12 12" />
    </button>
    <span
      v-if="hasIcon"
      class="alert-icon">
      <slot name="alertIcon" />
    </span>
    <span>
      <slot name="alertMessage">{{ alertMessage }}</slot>
    </span>
  </div>
</template>

<script>
import KIcon from '@kongponents/kicon/KIcon.vue'

export const appearances = {
  info: 'info',
  success: 'success',
  danger: 'danger',
  warning: 'warning'
}

export default {
  name: 'KAlert',
  components: { KIcon },
  props: {
    /**
    * Message to show in alert
    */
    alertMessage: {
      type: String,
      default: ''
    },
    /**
     * Set if close button is visible
     */
    isDismissible: {
      type: Boolean,
      default: false
    },
    /**
     * Set whether or not the alert box is shown.
     */
    isShowing: {
      type: Boolean,
      default: true
    },
    /**
     * Fixes alert to top
     */
    isFixed: {
      type: Boolean,
      default: false
    },
    /**
     * Set whether or not alert has full border is visible
     */
    isBordered: {
      type: Boolean,
      default: false
    },
    /**
     * Sets whether or not alert has left border
     */
    hasLeftBorder: {
      type: Boolean,
      default: false
    },
    /**
     * Center text inside alert
     */
    isCentered: {
      type: Boolean,
      default: false
    },
    /**
      * Base styling of the button<br>
      * One of ['primary, danger, warning, success ]
      */
    appearance: {
      type: String,
      default: 'info',
      validator: function (value) {
        return Object.values(appearances).indexOf(value) !== -1
      }
    },
    /**
     * Set whether alert box is the default size or small for context (under form fields, etc),
     */
    size: {
      type: String,
      default: '',
      validator: (value) => {
        return [
          '',
          'small'
        ].indexOf(value) !== -1
      }
    }
  },

  computed: {
    hasIcon () {
      return !!this.$slots.alertIcon
    }
  },

  methods: {
    dismissAlert () {
      this.$emit('closed')
    }
  }
}
</script>

<style scoped lang="scss">
@import '~@kongponents/styles/_variables.scss';

.k-alert {
  position: relative;
  display: flex;
  align-items: center;
  padding: var(--spacing-sm, spacing(sm)) var(--spacing-md, spacing(md));
  font-family: inherit;
  font-size: 1rem;
  border-radius: 3px;
  overflow-wrap: anywhere;
  a {
    text-decoration: underline;
    color: var(--blue-600, color(blue-600));
  }

  .alert-icon {
    margin-right: var(--spacing-xs, spacing(xs));
    max-height: 1rem;
    svg,
    img {
      max-height: 1rem;
    }
  }

  .close {
    position: absolute;
    top: 0;
    right: 18px;
    bottom: 0;
    border: 0;
    background-color: transparent;
    transition: all 200ms ease;
    cursor: pointer;
    opacity: .5;
    &:hover,
    &:active {
      text-decoration: none;
      opacity: 1;
    }
  }

  // Variants
  &.isFixed {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
  }
  &.isBordered {
    border: 1px solid;
  }
  &.isCentered {
    justify-content: center;
  }
  &.hasLeftBorder {
   border-left: 3px solid;
   border-radius: 0;
  }
  &.small {
    font-size: var(--type-sm, type(sm));
    padding: var(--spacing-sm, spacing(sm)) var(--spacing-xs, spacing(xs));
  }

  // Appearances
  &.info {
    color: var(--KAlertInfoColor, var(--blue-700, color(blue-700)));
    border-color: var(--KAlertInfoBorder, var(--blue-300, color(blue-300)));
    background-color: var(--KAlertInfoBackground, var(--blue-200, color(blue-200)));
  }
  &.success {
    color: var(--KAlertSuccessColor, var(--green-500, color(green-500)));
    border-color: var(--KAlertSuccessBorder, var(--green-200, color(green-200)));
    background-color: var(--KAlertSuccessBackground, var(--green-100, color(green-100)));
  }
  &.danger {
    color: var(--KAlertDangerColor, var(--red-700, color(red-700)));
    border-color: var(--KAlertDangerBorder, var(--red-300, color(red-300)));
    background-color: var(--KAlertDangerBackground, var(--red-200, color(red-200)));
  }
  &.warning {
    color: var(--KAlertWarningColor, var(--yellow-400, color(yellow-400)));
    border-color: var(--KAlertWarningBorder, var(--yellow-200, color(yellow-200)));
    background-color: var(--KAlertWarningBackground, var(--yellow-100, color(yellow-100)));
  }
}
</style>
