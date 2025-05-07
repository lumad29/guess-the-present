<template>
    <v-dialog max-width="500">
      <template #activator="{ props: activatorProps }">
        <!-- <v-btn
          v-bind="activatorProps"
          :color="activatorColor"
          :text="activatorText"
          :variant="activatorVariant"
        /> -->
      </template>
  
      <template #default="{ isActive }">
       
        <v-card :title="title">

             
          <v-card-text>
            <!-- <slot name="content">Default content goes here.</slot> -->
            <v-img
      src="@/assets/present.png"
      alt="Present"
      max-width="300"
      class="mx-auto"
    />
          </v-card-text>
          
  
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn :text="closeText" @click="isActive.value = false" />
          </v-card-actions>
        </v-card>
      </template>
    </v-dialog>
  </template>
  
  <script setup>
  defineProps({
    title: String,
    activatorText: {
      type: String,
      default: 'Open Dialog',
    },
    closeText: {
      type: String,
      default: 'Close Dialog',
    },
    activatorColor: {
      type: String,
      default: 'surface-variant',
    },
    activatorVariant: {
      type: String,
      default: 'flat',
    },
  });
  </script>
  