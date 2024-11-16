<template>
  <div class="navigation-container">
    <NuxtLink
      v-if="prev"
      :to="`/${basePath}/${prev.name}`"
      class="button-nav"
    >
      ← {{ prev.name }}
    </NuxtLink>
    <span v-else class="spacer">&nbsp;</span>

    <NuxtLink
      v-if="next"
      :to="`/${basePath}/${next.name}`"
      class="button-nav"
    >
      {{ next.name }} →
    </NuxtLink>
    <span v-else class="spacer">&nbsp;</span>
  </div>
</template>

<script>
export default {
  props: {
      prev: {
          type: Object,
          default: () => null
      },
      next: {
          type: Object,
          default: () => null
      },
      name: {
          type: String,
          default: () => null
      },
      basePath: {
          type: String,
          required: true 
      }
  }
}
</script>

<style scoped>
.navigation-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 20px 0;
  padding: 10px;
  background-color: #f7f7f7;
  border-radius: 8px;
}

.button-nav {
  display: inline-block;
  padding: 10px 20px;
  background-color: #427dbb;
  color: white;
  text-decoration: none;
  border-radius: 5px;
  font-weight: bold;
  transition: background-color 0.3s;
}

.button-nav:hover {
  background-color: #356a9a;
}

.spacer {
  flex: 1;
}
</style>