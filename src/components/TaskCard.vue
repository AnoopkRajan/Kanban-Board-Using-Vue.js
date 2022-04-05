<template>
  <div>
    <div @click="edit()">
      <p>{{ task.title }}</p>
      <!-- <div class="flex mt-4 justify-around items-center"> -->
      <badge v-if="task.type" :color="badgeColor">{{ task.type }}</badge>
      <!-- </div> -->

      <div class="card-footer">
        <days-indicator
          :dotsNumber="
            Math.floor((Date.now() - Number(task.date)) / (1000 * 60 * 60 * 24))
          "
        ></days-indicator>
        <button
          v-if="column === 'Done'"
          class="delete-btn"
          @click.stop="deleteTask()"
        >
          🗑
        </button>
        <img
          src="https://pickaface.net/gallery/avatar/unr_sample_161118_2054_ynlrg.png"
          alt="Avatar"
        />
      </div>
    </div>
    <edit-task
      v-if="editTask"
      :task="task"
      @closeTrigger="closedModal"
      :column="column"
    ></edit-task>
  </div>
</template>
<script>
import DaysIndicator from "./DaysIndicator.vue";
import Badge from "./StatusComponent.vue";
import EditTask from "./EditTask.vue";

export default {
  components: {
    Badge,
    DaysIndicator,
    EditTask,
  },
  emits: ["delete-task", "change-column"],
  props: {
    task: {
      type: Object,
      default: () => ({}),
    },
    column: String,
  },
  data() {
    return {
      editTask: false,
    };
  },
  methods: {
    edit() {
      this.editTask = true;
    },
    deleteTask() {
      this.$emit("delete-task", this.task.id);
    },
    closedModal($newColumn) {
      this.editTask = false;

      if ($newColumn !== this.column) {
        this.$emit("change-column", [this.column, $newColumn, this.task.id]);
      }
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

  .delete-btn {
    border: none;
    background: none;
  }

  img {
    width: 10%;
    height: 10%;
    border-radius: 50%;

    float: right;
    margin: 0;
  }
}
</style>
