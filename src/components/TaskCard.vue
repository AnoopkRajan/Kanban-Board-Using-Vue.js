<template>
  <div>
    <div>
      <p>
        {{ task.title }}
      </p>
      <!-- <div class="flex mt-4 justify-around items-center"> -->
      <badge v-if="task.type" :color="badgeColor">{{ task.type }}</badge>
      <!-- </div> -->

      <div class="card-footer">
        <days-indicator
          :dotsNumber="
            Math.floor((Date.now() - Number(task.date)) / (1000 * 60 * 60 * 24))
          "
        ></days-indicator>
        <img
          src="https://pickaface.net/gallery/avatar/unr_sample_161118_2054_ynlrg.png"
          alt="Avatar"
        />
      </div>
    </div>
  </div>
</template>
<script>
import DaysIndicator from "./DaysIndicator.vue";
import Badge from "./StatusComponent.vue";
export default {
  components: {
    Badge,
    DaysIndicator,
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
.card-footer {
  background: white;
  border: none;

  padding: 2%;

  display: flex;
  justify-content: space-between;
  align-items: center;

  img {
    width: 10%;
    height: 10%;
    border-radius: 50%;

    float: right;
    margin: 0;
  }
}
</style>
