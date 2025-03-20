<template>
  <v-app>
    <v-container>
      <h3 class="mb-4 text-center">Composant visuel pour du son</h3>

      <v-row class="d-flex align-center justify-center flex-nowrap">
        <!-- Bouton Volume (Mute/Unmute) -->
        <v-col cols="auto" class="d-flex align-center">
          <v-btn @click="toggleMute" variant="plain" icon>
            <v-icon
              >{{ isMuted ? 'mdi-volume-mute' : 'mdi-volume-high' }}</v-icon
            >
          </v-btn>
        </v-col>

        <!-- Bouton pour réduire -->
        <v-col cols="auto" class="d-flex align-center">
          <v-btn
            color="blue"
            size="small"
            variant="plain"
            @click="decreaseProgress"
          >
            <v-icon>mdi-minus</v-icon>
          </v-btn>
        </v-col>

        <!-- Slider qui prend 70% de l'espace -->
        <v-col
          class="d-flex align-center"
          style="flex-grow: 1; flex-basis: 70%"
        >
          <v-slider
            class="mt-4"
            v-model="progressValue"
            :min="0"
            :max="100"
            :color="sliderColor"
            track-color="grey-lighten"
            thumb-color="primary"
            :step="10"
            :thumb-label="'always'"
          ></v-slider>
        </v-col>

        <!-- Bouton pour augmenter -->
        <v-col cols="auto" class="d-flex align-center">
          <v-btn
            color="green"
            size="small"
            variant="plain"
            @click="increaseProgress"
          >
            <v-icon>mdi-plus</v-icon>
          </v-btn>
        </v-col>
      </v-row>
    </v-container>
  </v-app>
</template>

<script setup>
  import { ref, computed } from 'vue'

  const progressValue = ref(20)
  const isMuted = ref(false)

  const sliderColor = computed(() => {
    if (progressValue.value < 30) {
      return 'red'
    } else if (progressValue.value < 70) {
      return 'orange'
    } else {
      return 'green'
    }
  })

  const decreaseProgress = () => {
    if (progressValue.value > 0) {
      progressValue.value -= 10
    }
  }

  const increaseProgress = () => {
    if (progressValue.value < 100) {
      progressValue.value += 10
    }
  }

  const toggleMute = () => {
    isMuted.value = !isMuted.value
    progressValue.value = isMuted.value ? 0 : 20
  }
</script>
