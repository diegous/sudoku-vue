<template>
  <div class="cell"
    v-on:click="clicked"
    v-bind:class="classObject">
    {{ cell.value === "." ? "" : cell.value }}
  </div>
</template>

<script>
export default {
  name: 'Cell',
  props: {
    x: Number,
    y: Number,
    cell: {
      value: String,
      original: Boolean,
      selected: Boolean,
    },
  },
  computed: {
    classObject: function() {
      return {
        error: this.cell.error,
        original: this.cell.original,
        selected: !this.cell.original && this.cell.selected,
      }
    }
  },
  methods: {
    clicked: function() {
      this.$emit("update:selected", { x: this.x, y: this.y })
    }
  }
}
</script>

<style scoped>
.cell {
  width: 60px;
  height: 60px;
  line-height: 60px;

  border-color: grey;
  border-style: solid;
  border-width: 1px;

  font-size: 2rem;
}

.original {
  font-weight: bold;
  background-color: gainsboro;
}

.selected {
  background-color: lightblue;
}

.error {
  color: crimson;
}
</style>
