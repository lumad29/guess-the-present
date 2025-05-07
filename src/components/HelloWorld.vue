<script>
import { ref } from 'vue';
import toto from '@/assets/toto.png';
import PopUpDialog from './PopUpDialog.vue';

const dialog = ref(false); // This controls the dialog visibility
const selectedImage = ref(''); // This holds the image to show

</script>

<template>
  <v-container class="fill-height" max-width="900">
    <div>
      <v-img
        class="mb-4"
        height="150"
        src="@/assets/present.png"
      />

      <div class="mb-8 text-center">
        <div class="text-h2 font-weight-light mb-n1">Guess the</div>
        <h1 class="text-h2 font-weight-bold">Present Dude!</h1>
      </div>

      <v-row>
        <v-col cols="12">
          <v-card
            class="py-4"
            color="surface-variant"
            :image="toto"
            prepend-icon="mdi-thought-bubble"
            rounded="lg"
            variant="tonal"
          >
            <template #image>
              <v-img position="top right" />
            </template>

            <template #title>
              <h2 class="text-h5 font-weight-bold">
                Type here bitch
              </h2>
            </template>

            <template #subtitle>
              <div class="text-subtitle-1">
                <v-text-field label="Your guess" />
              </div>
            </template>

          </v-card>
        </v-col>

        <v-col v-for="present in presents" :key="present.href" cols="12" sm="6" >
          <v-card
            append-icon="mdi-open-in-new"
            class="py-4"
            color="surface-variant"
            :href="present.href"
            :prepend-icon="present.icon"
            rel="noopener noreferrer"
            rounded="lg"
            :subtitle="present.subtitle"
            target="_blank"
            :title="present.title"
            variant="tonal"
          >
          <v-btn @click="dialog = true" color="primary">Open Dialog</v-btn>

        </v-card>
        </v-col>
      </v-row>
    </div>
    <PopUpDialog v-model="dialog" title="My Dialog">
  <!-- <template #content>
    This is some content for the dialog.
  </template> -->
</PopUpDialog>
  </v-container>
   
</template>


<script setup>
  const presents = [
    {
      title: 'Shoe horn',
      // href: 'https://boardroomsocks.com/cdn/shop/products/man-using-metal-shoe-horn-to-slide-on-brown-dress-shoes_1200x.jpg?v=1638314398',
      icon: 'mdi-shoe-formal',
      subtitle: 'For putting shoes on like a lazy ass',
    },
    {
      title: 'Drone',
      // href: 'https://i5.walmartimages.com/seo/Holy-Stone-Drone-HS175D-4K-Camera-Adults-Beginners-Foldable-GPS-Auto-Return-Home-Follow-Me-Mode-2-Batteries-Double-Flight-Time-Black_5ec35928-1082-4505-9e86-c447a1ae1ec8.c50821396b551ec2f0ce01a79149fae3.jpeg',
      icon: 'mdi-quadcopter',
      subtitle: `Don't crash it into a waterfall`,
    },
    {
      title: 'T-Shirt',
      // href: 'https://http2.mlstatic.com/D_NQ_NP_2X_620266-MLA83881932863_042025-F.webp',
      icon: 'mdi-tshirt-crew-outline',
      subtitle: `I’d steal this from you and sleep in it`,
    },
    {
      title: 'Coffee Beans',
      // href: 'https://acdn-us.mitiendanube.com/stores/005/741/718/products/duna250gr-b3d11f95de4a3fe4ed17434437598325-1024-1024.webp',
      icon: 'mdi-coffee-outline',
      subtitle: `I'm sure this coffee tastes better than yours`,
    },
  ]
</script>
