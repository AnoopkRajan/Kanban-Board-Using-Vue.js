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
        <textarea v-model="newTask.title"></textarea>
      </div>
      <div class="task-info">
        <h6>Type:</h6>
        <select id="cars">
          <option value="Design">Design</option>
          <option value="Feature Request">Feature Request</option>
          <option value="QA">QA</option>
          <option value="Backend">Backend</option>
          <option value="default">Other</option>
        </select>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  emits: ["closeTrigger"],
  data() {
    return {
      newTask: {
        title: "Title",
        type: "",
      },
    };
  },
  methods: {
    closeModal() {
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
        padding-right: 50px;
        border: none;
        background: none;
      }
    }

    .task-title {
      height: 50px;
      margin-bottom: 40px;
      margin-left: 10%;
      padding: 20px;
    }

    .task-info {
      margin: 20px 0 20px 10%;
      //   width: 70%;
      display: flex;
      justify-content: left;
    }
  }
}
</style>
