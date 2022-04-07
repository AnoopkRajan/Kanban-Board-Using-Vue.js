<template>
  <div class="task-window">
    <div class="all-contents">
      <div class="top-section">
        <button class="close-btn" @click="closeModal()">❌</button>
      </div>
      <div class="contents-section">
        <div class="description-section">
          <div class="task">
            <textarea class="task-title" v-model="editingTask.title"></textarea>

            <div class="task-info">
              <h6>Description:</h6>
              <textarea
                class="textarea description"
                v-model="editingTask.desc"
              ></textarea>
            </div>
          </div>
        </div>
        <div class="info-section">
          <h5 class="info-title">Info</h5>

          <div class="info-content">
            <h6>Created On:</h6>
            <p>{{ String(Date(task.date)).slice(4, 15) }}</p>
          </div>

          <div class="info-content">
            <h6>Type:</h6>
            <select id="types" :value="editingTask.type">
              <option value="Design">Design</option>
              <option value="Feature Request">Feature Request</option>
              <option value="QA">QA</option>
              <option value="Backend">Backend</option>
              <option value="default">Other</option>
            </select>
          </div>
          <div class="info-content">
            <h6>Current status:</h6>
            <select id="status" :value="column">
              <option value="Backlog">Backlog</option>
              <option value="In Progress">In Progress</option>
              <option value="Blocked">Blocked</option>
              <option value="Review">Review</option>
              <option value="Done">Done</option>
            </select>
          </div>
          <div class="info-content">
            <h6>Priority:</h6>
            <select id="priority" :value="editingTask.priority">
              <option value="High">High</option>
              <option value="Medium">Medium</option>
              <option value="Low">Low</option>
            </select>
          </div>
          <div class="info-content opened">
            <h6>Opened by:</h6>
            <div class="user-details">
              <img style="border-radius: 50%" :src="task.image" alt="Avatar" />
              <p>{{ task.name }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  emits: ["closeTrigger", "columnChange"],
  props: {
    task: {
      type: Object,
      default: () => ({}),
    },
    column: String,
  },
  data() {
    return {
      editingTask: this.task,
    };
  },
  methods: {
    closeModal() {
      this.editingTask.type = document.getElementById("types").value;
      this.editingTask.priority = document.getElementById("priority").value;
      let newColumn = document.getElementById("status").value;
      this.$emit("closeTrigger", newColumn);
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
}
.all-contents {
  display: flex;
  flex-direction: column;

  background: #ffffff;
  box-shadow: 2px 2px 20px 1px;
  width: 80vw;
  height: 85vh;
  margin: 4% auto;

  .top-section {
    flex-basis: 5%;
    button {
      float: right;
      margin-top: 5px;
      margin-right: 40px;
      // border: none;
      background: none;
    }
  }

  .contents-section {
    flex-basis: 95%;

    display: flex;

    .description-section {
      flex-basis: 70%;
      .task {
        overflow-x: auto;
        display: flex;
        flex-direction: column;

        margin: 50px auto;

        // width: 80vw;
        // height: 80vh;

        .task-title {
          height: 50px;
          margin-bottom: 40px;
          margin-left: 10%;
          margin-right: 10%;
          padding: 20px;

          background: rgb(230, 230, 230);
          border: none;
          resize: none;

          font-size: 20px;
          font-weight: 600;
          text-align: center;

          &:focus {
            outline: none;
          }
        }

        .task-info {
          margin: 20px 0 20px 10%;
          //   width: 70%;
          display: flex;
          flex-direction: column;
          justify-content: left;
          // align-items: center;

          .textarea {
            width: 90%;
            padding: 12px 20px;
            border-radius: 4px;

            resize: none;
          }

          .description {
            height: 420px;
          }
        }
      }
    }

    .info-section {
      flex-basis: 30%;
      border: 1px solid #888;
      margin: 5px 10px 20px 0;

      .info-title {
        padding: 10px 0 10px 10px;
        border-bottom: 1px solid #888;
      }

      .info-content {
        margin: 15px 10px 0 10px;
        display: flex;
        justify-content: space-between;

        select {
          width: 45%;
        }
      }

      .opened {
        margin-top: 30px;
        align-items: center;

        .user-details {
          display: flex;
          flex-direction: column;
          align-items: center;

          img {
            width: 40px;
            height: 40px;
          }
        }
      }
    }
  }
}
</style>
