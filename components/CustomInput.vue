<template>
  <form novalidate @submit="submitValue">
    <div class="like-select">
      <input
        type="text"
        :value="modelValue"
        :placeholder="inputPlaceholder"
        @input="input"
      />
      <slot></slot>
    </div>

    <button type="submit">Submit</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      enterData: '',
    };
  },
  props: {
    modelValue: {
      type: String,
      required: true,
    },
    inputPlaceholder: {
      type: String,
      default: '',
    },
  },
  methods: {
    submitValue() {
      this.$emit('submit-value', this.modelValue);
    },
    input(event) {
      this.$emit('update:modelValue', event.target.value);
    },
  },
};
</script>

<style>
.like-select {
  width: 84%;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  align-items: center;
  border: 2px solid #000;
  position: relative;
}

form {
  display: flex;
  flex-wrap: wrap;
  gap: 15px;
  position: relative;
  margin: 2vh 0 0;
}

input[type='text'] {
  flex-basis: 84%;
  font-size: 18px;
  color: #000;
  border: none;
  padding: 20px;
  transition: border-color 0.4s;
}

input[type='text']::placeholder {
  text-transform: uppercase;
  font-size: 18px;
  color: #000;
}

input[type='text']:focus {
  border-color: #ec6e4c;
  outline: none;
}

button {
  flex-basis: 14%;
  cursor: pointer;
  background: #ec6e4c;
  color: #fff;
  font-size: 18px;
  text-transform: uppercase;
  border: none;
  transition: background 0.4s, color 0.4s;
}

button:hover {
  background: #fafafa;
  color: #000;
}

button:active {
  background: #000;
  color: #fafafa;
}
</style>
