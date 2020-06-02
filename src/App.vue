<template>
  <div>
    <Header></Header>
    <MainContent></MainContent>
  </div>
</template>

<script>
import Header from './components/Header.vue';
import MainContent from './components/MainContent.vue';
import './bootstrap-reboot.css';

export default {
  components: {
    Header,
    MainContent,
  }
}
</script>

<style lang="scss">
* {
  font-family: 'Crimson Text', 'Noto Serif JP', serif;
  overflow-wrap: break-word;
}
input {
  outline: 0;
}
textarea {
  outline: 0;
}
.big {
  font-weight: 700;
  color: rgb(235, 8, 8);
}
.btn {
  border: 1px solid #fff;
  font-size: 15px;
  padding: 5px 5px;
  margin-right: 10px;
  box-shadow: 0 0 0 0 rgb(199, 198, 198);

  &:hover {
    background: #ddd;
  }
}
.task-section {
  width: 22%;
  margin: 10px;
  padding: 20px;
  box-sizing: border-box;
  background: rgb(210, 234, 238);
  & dt {
    font-size: 14px;
    margin-bottom: 5px;
  }
}
</style>