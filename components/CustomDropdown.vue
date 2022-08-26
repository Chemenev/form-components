<template>
  <div class="like-select__menu">
    <div
      class="like-select__menu-item"
      v-for="(item, index) in inputArr"
      :key="index"
      @click="currenItem(item)"
    >
      {{ item }}
    </div>
  </div>
</template>

<script>
export default {
  props: {
    inputArr: {
      type: Array,
    },
  },
  methods: {
    currenItem(value) {
      this.$emit('current-item', value);
    },
  },
};
</script>

<style>
.like-select__menu {
  /*  position: absolute; */
  left: -2px;
  top: 100%;
  width: calc(100% + 4px);
  text-align: left;
  border: 2px solid #000;
  background: #fff;
}

.like-select__menu-item {
  text-transform: capitalize;
  padding: 7px 15px;
}

.like-select__menu-item:hover {
  background: rgba(0, 0, 0, 0.1);
  cursor: pointer;
}
</style>
