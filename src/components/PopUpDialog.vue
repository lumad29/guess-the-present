<script setup>
import { computed } from 'vue';

// Define props: v-model (modelValue), dynamic imageUrl, title, and optional close text
const props = defineProps({
  modelValue: Boolean,
  imageUrl: String,
  title: String,
  closeText: { type: String, default: 'Close' },
});
// Emit event to update the parent dialog visibility
const emit = defineEmits(['update:modelValue']);

// Proxy modelValue prop into an internal reactive for v-dialog v-model binding
const internalModel = computed({
  get: () => props.modelValue,
  set: (val) => emit('update:modelValue', val),
});
</script>

<template>
  <!-- Bind the dialog visibility to internalModel -->
  <v-dialog v-model="internalModel" max-width="500">
    <!-- No internal activator: parent controls opening via v-model -->
    <v-card :title="title">
      <v-card-text>
        <!-- Render the passed-in image dynamically -->
        <v-img
          v-if="imageUrl"
          :src="imageUrl"
          alt="Present"
          max-width="300"
          class="mx-auto"
          cover
        />
      </v-card-text>

      <v-card-actions>
        <v-spacer />
        <!-- Close button uses the passed-in closeText prop -->
        <v-btn text @click="internalModel = false">
          {{ closeText }}
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>
