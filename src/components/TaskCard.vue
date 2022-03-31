<template>
  <div class="bg-white shadow rounded px-3 pt-3 pb-5 border border-white">
    <div class="flex justify-between">
      <p class="text-gray-700 font-semibold font-sans tracking-wide text-sm">
        {{ task.title }}
      </p>
      <div class="flex mt-4 justify-around items-center">
        <badge v-if="task.type" :color="badgeColor">{{ task.type }}</badge>
      </div>

      <img
        class="w-6 h-6 rounded-full ml-3"
        src="https://pickaface.net/gallery/avatar/unr_sample_161118_2054_ynlrg.png"
        alt="Avatar"
      />
    </div>
  </div>
</template>
<script>
import Badge from "./StatusComponent.vue";
export default {
  components: {
    Badge,
  },
  props: {
    task: {
      type: Object,
      default: () => ({}),
    },
  },
  computed: {
    badgeColor() {
      const mappings = {
        Design: "#acddde",
        "Feature Request": "#f7d8ba",
        Backend: "#e1f8dc",
        QA: "#fef8dd",
        default: "#fef",
      };
      return mappings[this.task.type] || mappings.default;
    },
  },
};
</script>

<style lang="scss" scoped>
img {
  width: 10%;
  height: 10%;
  border-radius: 50%;
}
</style>
