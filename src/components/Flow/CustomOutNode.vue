<script setup lang="ts">
import { Handle, Position } from "@vue-flow/core"

const props = defineProps({
  data: {
    type: Object,
    required: true
  },
  status: {
    type: String,
    required: false
  }
})

const emits = defineEmits(["freeze", "defreeze"])
</script>

<template>
  <div class="indicator">
    <span
      v-if="status"
      :class="[
        'indicator-item',
        'badge',
        status == 'running'
          ? 'badge-primary'
          : status == 'finished'
          ? 'badge-success'
          : status == 'error'
          ? 'badge-error'
          :'badge-warning'
      ]"
    ></span>

    <div class="card bg-neutral">
      <div class="card-body">
        <h2 class="card-title">Output</h2>
        <input
          @focus="emits('freeze')"
          @blur="emits('defreeze')"
          v-model="data.data.label"
          type="text"
          placeholder="Label"
          class="input input-sm w-full max-w-xs"
        />
      </div>
    </div>
  </div>
  <Handle
    id="in"
    :connectable="true"
    :connectable-start="false"
    type="target"
    :position="Position.Left"
  />
</template>
