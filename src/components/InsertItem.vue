<template>
  <div>
      <form  class="task-section" @submit.prevent="addItem">
        <dl>
          <dt>TASK</dt>
          <dd><input type="text" v-model="newTaskName"></dd>
          <dt>MEMO</dt>
          <dd><textarea type="text" v-model="newTaskDs"></textarea></dd>
        </dl>
        <input class="btn" type="submit" value="INSERT">
      </form>
    </div>
</template>

<script>
export default {
  props: ["taskAlls"],
  data() {
    return {
      newTaskName: "",
      newTaskDs: "",
    }
  },
  computed: {
    getInsertTime() {
      const d = new Date(Date.now());
      const date1 = d.getDate();
      const year = d.getUTCFullYear();
      const month = d.getMonth();
      return `${year}/${month + 1}/${date1}`;
    }
  },
  methods: {
    addItem() {
      if (this.newTaskName == "" && this.newTaskDs == "") {
        return;
      }
      let item = {
        taskName: this.newTaskName,
        taskDs: this.newTaskDs,
        insertTime: this.getInsertTime,
      };
      this.taskAlls.push(item);
      this.clearInput();
    },
    clearInput() {
      this.newTaskName = "";
      this.newTaskDs = "";
      this.newTaskLevel = "";
    },
  }
}
</script>

<style scoped>
form {
  background: #ddd;
  margin: 0 auto;
}
form dd {
  width: 100%;
}
form textarea {
  width: 100%;
}
form input {
  width: 100%;
}
</style>