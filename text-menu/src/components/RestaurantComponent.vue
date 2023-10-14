<template>
  <v-text-field
    type="text"
    :value="restaurantName"
    @input="$emit('update:restaurantName', $event.target.value)"
  ></v-text-field>
</template>

<script>
export default {
  props: {
    restaurantName: String,
  },
  emits: ['update:restaurantName']
}
</script>
