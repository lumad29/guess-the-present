<script setup>
import { ref } from 'vue';
import toto from '@/assets/toto.png';
import PopUpDialog from './PopUpDialog.vue';
import SnackBar from './SnackBar.vue';

const dialog = ref(false); // This controls the dialog visibility
const selectedImage = ref(''); // This holds the image to show


const presents = [
    {
      title: 'Shoe horn',
      imageUrl: new URL('@/assets/shoeHorn.png', import.meta.url).href,
      icon: 'mdi-shoe-formal',
      subtitle: 'For putting shoes on like a lazy ass',
    },
    {
      title: 'Drone',
      imageUrl: new URL('@/assets/drone.png', import.meta.url).href,
      icon: 'mdi-quadcopter',
      subtitle: `Don't crash it into a waterfall`,
    },
    {
      title: 'Shirt',
      imageUrl: new URL('@/assets/shirt.png', import.meta.url).href,
      icon: 'mdi-tshirt-crew-outline',
      subtitle: `I’d steal this from you and sleep in it`,
    },
    {
      title: 'Coffee Beans',
      imageUrl: new URL('@/assets/coffee.png', import.meta.url).href,
      icon: 'mdi-coffee-outline',
      subtitle: `I'm sure this coffee tastes better than yours`,
    },
  ];

  const guess = ref(''); // User's guess
  const snackbarMessage = ref('');
  const showSnackbar = ref(false);
  const snackbarColor = ref('');


  function openDialog(imageUrl) {
  selectedImage.value = imageUrl;
  dialog.value = true;
}

// Function to check the guess
function checkGuess() {
  const g = guess.value.trim().toLowerCase(); // Normalize guess (case-insensitive)
  const correctAnswer = 'shirt'; // Correct answer (case insensitive)
  if (!g) return;

  // Check if the guess matches the correct answer
  if (g === correctAnswer) {
    snackbarMessage.value = `🎉 YAaaay! You guessed! It's a "${correctAnswer}"!`;
    snackbarColor.value = 'success';
  } else {
    snackbarMessage.value = '❌ Nope, try again.';
    snackbarColor.value = 'error';
  }
  showSnackbar.value = true;
  guess.value = '';
}

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
                <v-text-field v-model="guess" label="Your guess" @keyup.enter="checkGuess()"/>
                <v-btn @click="checkGuess()">check</v-btn>
              </div>
            </template>

          </v-card>
        </v-col>

        <v-col v-for="present in presents" :key="present.href" cols="12" sm="6" >
          <v-card
       
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
          <v-btn @click="openDialog(present.imageUrl)" color="primary" size="small" variant="text" class="ml-8">See Image</v-btn>
        </v-card>
        </v-col>
      </v-row>
    </div>
    <PopUpDialog v-model="dialog" :image-url="selectedImage" title="Is it this?">
  <!-- <template #content>
    This is some content for the dialog.
  </template> -->
</PopUpDialog>

<v-snackbar v-model="showSnackbar" :color="snackbarColor">
  {{ snackbarMessage }}
  <template #actions>
    <v-btn variant="text" @click="showSnackbar = false">Close</v-btn>
  </template>
</v-snackbar>

  </v-container>
   
</template>

