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
          @change="changeDate"
        >
          <template v-if="column.title === 'Backlog'" #header>
            <div class="add-btn" role="group">
              <button @click="add">﹢</button>
            </div>
          </template>
          <template #item="{ element }">
            <task-card
              :task="element"
              class="list-group-item"
              :column="column.title"
              @delete-task="deleteFromL4"
              @change-column="changeColumn"
            ></task-card>
          </template>
        </draggable>
      </div>
    </div>
  </div>
  <add-task
    v-if="addTask"
    @closeTrigger="addTask = false"
    @newTaskInfo="addNewTask"
  ></add-task>
</template>

<script>
import { columns } from "./columns";
import draggable from "vuedraggable";
import TaskCard from "./components/TaskCard.vue";
import AddTask from "./components/AddTask.vue";

var id = 100;

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
      columnToIndex: {
        Backlog: 0,
        "In Progress": 1,
        Blocked: 2,
        Review: 3,
        Done: 4,
      },
    };
  },
  methods: {
    add: function () {
      this.addTask = true;
    },

    addNewTask($newTask) {
      $newTask.id = id++;
      this.list.push($newTask);
    },
    deleteFromL4($id) {
      for (let i = 0; i < this.list4.length; i++) {
        if (this.list4[i].id === Number($id)) {
          this.list4.splice(i, 1);
          break;
        }
      }
    },
    changeColumn($passedInfo) {
      let previousColumn = $passedInfo[0];
      let newColumn = $passedInfo[1];
      let taskId = $passedInfo[2];
      let taskData = {};

      for (
        let i = 0;
        i < this.columns[this.columnToIndex[previousColumn]].tasks.length;
        i++
      ) {
        if (
          this.columns[this.columnToIndex[previousColumn]].tasks[i].id ===
          taskId
        ) {
          taskData = this.columns[this.columnToIndex[previousColumn]].tasks[i];
          this.columns[this.columnToIndex[previousColumn]].tasks.splice(i, 1);
          break;
        }
      }

      this.columns[this.columnToIndex[newColumn]].tasks.push(taskData);
    },
    changeDate({ added }) {
      let newOne = added;
      if (added) newOne.element.date = Date.now();
    },
  },
};
</script>

<style lang="scss" scoped>
.main-wrapper {
  display: flex;
  z-index: 2;

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
    transform: translate(4%, -25px);
    position: absolute;
    z-index: 10;

    button {
      border: none;
      background: #888;
      border-radius: 5px;
    }
  }
}
</style>
