<template>
  <div class="main-wrapper">
    <div v-for="column in columns" :key="column.title" class="sections">
      <h6>{{ column.title }}</h6>
      <div class="scrollable-area">
        <draggable
          id="first"
          data-source="juju"
          :list="column.tasks"
          class="list-group"
          group="a"
          item-key="id"
        >
          <template #item="{ element }">
            <task-card :task="element" class="list-group-item"></task-card>
          </template>

          <template v-if="column.title === 'Backlog'" #footer>
            <div class="btn-group add-btn" role="group">
              <button class="btn btn-secondary" @click="add">Add</button>
            </div>
          </template>
        </draggable>
      </div>
    </div>
  </div>
  <add-task v-if="addTask" @closeTrigger="addTask = false"></add-task>
</template>

<script>
import { columns } from "./columns";
import draggable from "vuedraggable";
import TaskCard from "./components/TaskCard.vue";
import AddTask from "./components/AddTask.vue";

export default {
  order: 14,
  components: {
    draggable,
    TaskCard,
    AddTask,
  },
  data() {
    return {
      addTask: false,
      columns,
      badgeColors: {
        Design: "green",
        "Feature Request": "blue",
        QA: "yellow",
        Backend: "red",
      },
      list: columns[0].tasks,
      list1: columns[1].tasks,
      list2: columns[2].tasks,
      list3: columns[3].tasks,
      list4: columns[4].tasks,
    };
  },
  methods: {
    add: function () {
      this.addTask = true;
    },
  },
};
</script>

<style lang="scss" scoped>
.main-wrapper {
  display: flex;
  z-index: 2;
  // margin: 5px auto;

  .sections {
    flex-basis: 50%;
    margin: 5px;
    padding-bottom: 15px;

    background: rgb(245, 245, 247);

    h6 {
      margin: 5px 0;
      text-align: center;
      color: rgb(85, 95, 114);
    }

    .scrollable-area {
      height: 92vh;
      overflow-y: auto;
    }
  }
}

.list-group {
  .list-group-item {
    border-radius: 10px;

    width: 95%;
    margin: 5px auto;
    padding: 10px;

    min-height: 80px;
    max-height: 180px;
  }
  .add-btn {
    margin-left: 10px;
  }
}
</style>
