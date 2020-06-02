<template>
  <div class="main">
    <div class="today-task">

      <transition name="fade">
        <div v-show="isShown" class="mask" @click="isShown = !isShown"></div>
      </transition>
      <transition name="fade">
        <section class="modal" v-show="isShown">
          <dl>
            <p>TASK</p>
            <input type="text" v-model="text">
            <p>MEMO</p>
            <textarea type="text" v-model="description"></textarea>
          </dl>
          <button class="btn" @click="editComp()">COMPLETE</button>
        </section>
      </transition>
    
      <section class="task-section" v-for="(taskAll, index) in taskAlls" :key="index">
        <p class="time">{{ taskAll.insertTime }}</p>
        <dl>
          <dt>TASK</dt>
          <dd class="big">{{ taskAll.taskName }}</dd>
          <dt>MEMO</dt>
          <dd>{{ taskAll.taskDs }}</dd>
        </dl>
        <div class="btns">
        <button class="btn" @click="deleteItem(index)">DELETE</button>
        <button class="btn" @click="edit(index)">EDIT</button>

        </div>
      </section>

    </div>
    <insert-item :taskAlls="taskAlls"></insert-item>
  </div>
</template>

<script scoped>
import InsertItem from './InsertItem.vue';
export default {
  components: {
    InsertItem,
  },
  data() {
    return {
      isShown: false,
      taskAlls: [],
      isactive: true,
      editName: "",
      editIndex: -1,
      text: "",
      description: "",
    }
  },
  computed: {
    returnTask() {
      return this.taskAlls[this.currentIndex];
    }
  },
  methods: {
    edit(index) {
      this.isShown = !this.isShown;
      this.editIndex = index;
      this.text = this.taskAlls[index].taskName;
      this.description = this.taskAlls[index].taskDs;
      // this.$refs.editor1.focus();
      // this.$refs.editor2.focus();
    },
    editComp() {
      let editItem = {
        taskName: this.text,
        taskDs: this.description,
      }
      this.taskAlls.splice(this.editIndex, 1, editItem);
      this.isShown = !this.isShown;
    },
    deleteItem(index) {
      if (confirm('本当に削除しますか？')) {
        this.taskAlls.splice(index, 1);
        this.currentIndex = index;
      }
    },
  },
  watch: {
    taskAlls: {
      handler() {
        localStorage.setItem('taskAlls', JSON.stringify(this.taskAlls));
      },
      deep: true
    }
  },
  mounted() {
    this.taskAlls = JSON.parse(localStorage.getItem('taskAlls')) || [];
  },
}
</script>

<style lang="scss" scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity .4s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
.main {
  padding: 20px 0;
  .today-task {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    margin-bottom: 20px;
  }
}
.mask {
  background: rgba(0,0,0,0.4);
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
}
.modal {
  background: rgb(210, 234, 238);
  width: 25%;
  padding: 20px;
  box-sizing: border-box;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  & input {
    padding: 4px;
    width: 100%;
  }
  & textarea {
    width: 100%;
  }
}
.today-task {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  margin-bottom: 20px;
}
.time {
  float: right;
}
.task-section dd {
  background: #fff;
  padding: 4px;
}
.task-section dt {
  font-size: 14px;
  margin-bottom: 5px;
}
</style>