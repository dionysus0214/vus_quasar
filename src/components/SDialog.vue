<template>
  <q-dialog>
    <q-card class="s-confirm">
      <q-card-actions class="modal-close-button">
        <q-btn
          :icon="closeIcon"
          flat
          round
          dense
          v-close-popup
          color="grey-6"
          :ripple="false"
          @click="$emit('handleClose')"
        />
      </q-card-actions>
      <q-card-section class="modal-title">
        <div
          v-if="withHeaderIcon"
          class="flex items-center justify-center modal-icon"
        >
          <q-icon
            v-if="type === 'info'"
            :name="infoOutlineIcon"
            size="32px"
            color="positive"
          />
          <q-icon
            v-else
            :name="warningOutlineIcon"
            size="32px"
            color="negative"
          />
        </div>
        {{ title }}
      </q-card-section>
      <q-card-section class="modal-content">
        <slot name="content"></slot>
      </q-card-section>
      <q-card-actions
        class="modal-buttons"
        align="center"
        :vertical="btnVertical"
        :class="btnVertical ? 'btn-vertical' : 'no-vertical'"
      >
        <q-btn
          class="modal-button first"
          no-caps
          no-wrap
          dense
          unelevated
          :ripple="false"
          :color="firstBtnColor"
          :outline="firstBtnOutLine"
          @click="$emit('handleFirst')"
        >
          {{ buttonLabel }}
        </q-btn>
        <q-btn
          v-if="twoButtons"
          class="modal-button second"
          no-caps
          no-wrap
          dense
          unelevated
          :ripple="false"
          :color="secondBtnColor"
          :outline="secondBtnOutLine"
          @click="$emit('handleSecond')"
        >
          {{ secondButtonLabel }}
        </q-btn>
      </q-card-actions>
    </q-card>
  </q-dialog>
</template>

<script>
import { infoOutlineIcon, warningOutlineIcon, closeIcon } from '../assets/icons.js';

export default {
  props: {
    withHeaderIcon: {
      type: Boolean,
      default: false,
    },
    title: {
      type: String,
      default: '',
    },
    content: {
      type: String,
      default: '',
    },
    type: {
      type: String,
      default: 'info',
    },
    buttonLabel: {
      type: String,
      default: '',
    },
    twoButtons: {
      type: Boolean,
      default: false,
    },
    secondButtonLabel: {
      type: String,
      default: '',
    },
    firstBtnColor: {
      type: String,
      default: '',
    },
    secondBtnColor: {
      type: String,
      default: '',
    },
    firstBtnOutLine: {
      type: Boolean,
      default: false,
    },
    secondBtnOutLine: {
      type: Boolean,
      default: false,
    },
    btnVertical: {
      type: Boolean,
      default: false,
    },
  },
  setup() {
    return {
      infoOutlineIcon,
      warningOutlineIcon,
      closeIcon,
    };
  },
};
</script>

<style lang="scss">
.s-confirm {
  border-radius: 8px;
  padding: 40px 24px;
  width: 504px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  .modal-close-button {
    position: absolute;
    top: 12px;
    right: 12px;
    width: 24px;
    height: 24px;
    padding: 0;
    .q-btn {
      color: $grey-4;
      padding: 0;
      width: 100%;
      height: 100%;
      align-items: center;
      justify-content: center;
      min: {
        height: 0;
        width: 0;
      }
      .q-focusable:focus .q-focus-helper,
      .q-hoverable:hover .q-focus-helper {
        background: inherit !important;
        opacity: 0;
      }
      .q-icon {
        width: 100%;
        height: 100%;
      }
    }
  }
  .modal-title {
    padding: 0 0 16px;
    text-align: center;
    color: $grey-1;
    font: {
      size: 20px;
      weight: 700;
    }
    .modal-icon {
      text-align: center;
      width: 32px;
      height: 32px;
      margin: 0 auto 16px;
    }
  }
  .modal-content {
    padding: 0 0 32px;
    text-align: center;
    font: {
      size: 14px;
      weight: 400;
    }
  }
  .modal-buttons {
    text-align: center;
    padding: 0;
    width: 100%;
    height: 42px;
    display: flex;
    flex-flow: row nowrap;
    justify-content: center;
    .q-btn {
      min-width: 76px;
      padding: 8px 24px;
      margin: 0 4px;
      height: 42px;
      font: {
        weight: 500;
        size: 18px;
      }
      &__content {
        height: 100%;
      }
    }
  }
}
</style>
