<template>
  <div class="card brew-list">
    <ul class="list-group list-group-flush">
      <li
        @mouseover="mouseOver(index)"
        @mouseleave="mouseLeave(index)"
        v-bind:key="index"
        v-for="(brew, index) in brews"
        class="list-group-item">
        {{index}} || {{brew.id}} - {{brew.name}}, {{brew.state}}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "BrewList",
  // props: ["brews"]
  props: {
    brews: Array
  },
  methods: {
    mouseOver(index) {
      this.$emit('mouse-over-brew', index);
    },
    mouseLeave(index) {
      this.$emit('mouse-left-brew', index);
    }
  }
}
</script>

<style lang="scss" scoped>
  .brew-list {
    //overflow-y: scroll;
    height: 95vh; // 95% of the screen's full height, which is 100vh
    li {
      &:hover {
        background-color: darkgrey;
      }
    }
  }
</style>