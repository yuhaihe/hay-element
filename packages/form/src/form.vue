<template>
  <div>
    <form>
      <slot></slot>
    </form>
  </div>
</template>
<script>
export default {
  name: "LgForm",
  provide() {
    return {
      form: this,
    };
  },
  props: {
    model: {
      type: Object,
    },
    rules: {
      type: Object,
    },
  },
  methods: {
    validate(cb) {
      const tasks = this.$children
        .filter((child) => child.prop)
        .map((child) => child.validate());
      Promise.all(tasks)
        .then(() => cb(true))
        .catch(() => cb(false));
    },
  },
};
</script>
<style scoped>
</style>