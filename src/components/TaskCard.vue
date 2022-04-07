<template>
  <div>
    <div @click="edit()">
      <p>{{ task.title }}</p>
      <!-- <div class="flex mt-4 justify-around items-center"> -->
      <badge v-if="task.type" :color="badgeColor">{{ task.type }}</badge>
      <!-- </div> -->

      <div class="card-footer">
        <div class="days-priority">
          <div class="priority">
            <img
              v-if="task.priority === 'High'"
              class="status"
              src="@/assets/Icons/high-p.png"
              alt="High priority status icon"
            />
            <img
              v-if="task.priority === 'Medium'"
              class="status"
              src="@/assets/Icons/medium-p.png"
              alt="Medium priority status icon"
            />
            <img
              v-if="task.priority === 'Low'"
              class="status"
              src="@/assets/Icons/low-p.png"
              alt="Low priority status icon"
            />
          </div>
          <days-indicator
            class="days"
            :dotsNumber="
              Math.floor(
                (Date.now() - Number(task.date)) / (1000 * 60 * 60 * 24)
              )
            "
          ></days-indicator>
        </div>
        <button
          v-if="column === 'Done'"
          class="delete-btn"
          @click.stop="deleteTask()"
        >
          🗑
        </button>
        <!-- <img class="avatar" :src="getRandomUser()" alt="Avatar" /> -->
        <img class="avatar" :src="task.image" alt="Avatar" />
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
      // image:
      //   "https://pickaface.net/gallery/avatar/unr_sample_161118_2054_ynlrg.png",
      image: "https://randomuser.me/api/portraits/thumb/men/41.jpg",
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

  .days-priority {
    display: flex;
    // justify-content: space-around;
    align-items: center;
    max-width: 80px;

    .priority {
      flex-basis: 20%;

      .status {
        width: 80%;
        height: 80%;
      }
    }
  }

  .delete-btn {
    border: none;
    background: none;
  }

  .avatar {
    width: 10%;
    height: 10%;
    border-radius: 50%;

    float: right;
    margin: 0;
  }
}
</style>
