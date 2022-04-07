<template>
  <div class="task-window">
    <div class="task">
      <div class="top-section">
        <button class="close-btn" @click="closeModal()">❌</button>
      </div>
      <div class="task-title">
        <h3>{{ newTask.title }}</h3>
      </div>

      <div class="task-info">
        <h6>Title:</h6>
        <textarea class="textarea title" v-model="newTask.title"></textarea>
      </div>
      <div class="task-info">
        <div class="type-priority">
          <div class="type">
            <h6>Type:</h6>
            <select id="types">
              <option value="Design">Design</option>
              <option value="Feature Request">Feature Request</option>
              <option value="QA">QA</option>
              <option value="Backend">Backend</option>
              <option value="default">Other</option>
            </select>
          </div>
          <div class="priority">
            <h6>Priority:</h6>
            <select id="priority">
              <option value="Low">Select</option>
              <option value="High">High</option>
              <option value="Medium">Medium</option>
              <option value="Low">Low</option>
            </select>
          </div>
        </div>
      </div>
      <div class="task-info">
        <h6>Description:</h6>
        <textarea
          class="textarea description"
          v-model="newTask.desc"
        ></textarea>
      </div>

      <div class="add-or-cancel">
        <button class="cancel" @click="closeModal()">Cancel</button>
        <button class="add" @click="addNewTask()">Add</button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  emits: ["closeTrigger", "newTaskInfo"],
  data() {
    return {
      newTask: {
        id: "",
        title: "Title",
        date: "",
        type: "",
        desc: "blah blah blah",
        priority: "",
        image: "",
        name: "",
      },
    };
  },
  methods: {
    closeModal() {
      this.$emit("closeTrigger");
    },
    addNewTask() {
      this.newTask.type = document.getElementById("types").value;
      this.newTask.priority = document.getElementById("priority").value;
      this.newTask.date = Date.now();
      this.getRandomUser();

      this.$emit("newTaskInfo", this.newTask);
      this.closeModal();
    },
    getRandomUser: async function () {
      try {
        const response = await axios.get("https://randomuser.me/api/");
        this.newTask.image = response.data.results[0].picture.thumbnail;
        this.newTask.name = `${response.data.results[0].name.first} ${response.data.results[0].name.last}`;
      } catch (err) {
        console.log("error: ", err);
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.task-window {
  z-index: 500;
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.3);

  .task {
    background: #ffffff;
    box-shadow: 2px 2px 20px 1px;
    overflow-x: auto;
    display: flex;
    flex-direction: column;

    margin: 50px auto;

    width: 80vw;
    height: 80vh;

    .top-section {
      button {
        float: right;
        margin-top: 5px;
        margin-right: 40px;
        background: none;
      }
    }

    .task-title {
      height: 50px;
      margin-bottom: 40px;
      margin-left: 10%;
      margin-right: 10%;
      padding: 20px;

      background: rgb(230, 230, 230);

      h3 {
        transform: translateY(-10px);
        text-align: center;
      }
    }

    .task-info {
      margin: 20px 0 20px 10%;
      //   width: 70%;
      display: flex;
      flex-direction: column;
      justify-content: left;
      // align-items: center;

      .type-priority {
        display: flex;

        .type {
          margin-right: 50px;
        }
      }

      .textarea {
        width: 90%;

        // height: 100px;
        padding: 12px 20px;
        border-radius: 4px;

        resize: none;
      }

      .title {
        height: 60px;
      }

      .description {
        height: 200px;
      }
    }

    .add-or-cancel {
      display: flex;
      justify-content: flex-end;

      button {
        margin-right: 40px;
        width: 80px;
        height: 40px;
        border-radius: 10px;
      }
    }
  }
}
</style>
