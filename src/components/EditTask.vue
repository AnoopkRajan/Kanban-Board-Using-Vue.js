<template>
  <div class="task-window">
    <div class="task">
      <div class="top-section">
        <button class="close-btn" @click="closeModal()">❌</button>
      </div>
      <div class="task-title">
        <h3>{{ task.title }}</h3>
      </div>

      <div class="task-info">
        <h6>Title:</h6>
        <textarea class="textarea title" v-model="editingTask.title"></textarea>
      </div>
      <div class="task-info">
        <h6>Type:</h6>
        <select id="types" :value="editingTask.type">
          <option value="Design">Design</option>
          <option value="Feature Request">Feature Request</option>
          <option value="QA">QA</option>
          <option value="Backend">Backend</option>
          <option value="default">Other</option>
        </select>
      </div>
      <div class="task-info">
        <h6>Description:</h6>
        <textarea
          class="textarea description"
          v-model="editingTask.desc"
        ></textarea>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  emits: ["closeTrigger"],
  props: {
    task: {
      type: Object,
      default: () => ({}),
    },
  },
  data() {
    return {
      editingTask: this.task,
    };
  },
  methods: {
    closeModal() {
      this.editingTask.type = document.getElementById("types").value;
      this.$emit("closeTrigger");
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
        // border: none;
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

      select {
        width: 15%;
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
  }
}
</style>
