<template>
  <custom-input
    @submit-value="submitValue"
    v-model="pressedCity"
    inputPlaceholder="Enter your city"
    @click="
      {
        isVisible = true;
      }
    "
  >
    <div
      class="like-select__append"
      v-bind:class="{ active: isVisible }"
      @click="
        {
          isVisible = true;
        }
      "
    >
      +
    </div>
  </custom-input>
  <custom-dropdown
    v-if="this.cityList.length > 0 && isVisible"
    :inputData="this.enterCity"
    :inputArr="filteredCity()"
    @current-item="submitValue"
    v-click-outside="hide"
  />
</template>
<script>
import { mapActions, mapGetters } from 'vuex';
import CustomInput from '@/components/CustomInput.vue';
import CustomDropdown from './CustomDropdown.vue';

export default {
  components: { CustomInput, CustomDropdown },
  data() {
    return {
      pressedCity: '',
      isVisible: false,
    };
  },
  computed: {
    ...mapGetters('weather', ['cityList', 'enterCity']),
  },
  methods: {
    ...mapActions('weather', ['fetchWeather']),
    submitValue(value) {
      this.pressedCity = value;
      this.fetchWeather(value);
      this.hide();
    },
    filteredCity() {
      const filteredCity = this.cityList.filter((item) =>
        item.includes(this.pressedCity)
      );
      return filteredCity.slice(0, 4);
    },
    hide() {
      this.isVisible = false;
      console.log('hide');
    },
  },
};
</script>

<style>
.like-select__append {
  padding: 15px;
  font-size: 25px;
  font-weight: 600;
  transition: transform 0.4s, color 0.4s;
  cursor: pointer;
}

.like-select__append.active {
  transform: rotate(45deg);
  color: #ec6e4c;
}
</style>
