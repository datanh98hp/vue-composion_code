<template>
  <div class="myapp">
    <header>
      <div class="title">
        <img src="./assets/logo.png" />
        <h1>MY JOB LIST</h1>
      </div>
      <div class="order">
        <button @click="handleClick('title')">Order by Title</button>
        <button @click="handleClick('salary')">Order by Salary</button>
        <button @click="handleClick('location')">Order by Location</button>
      </div>
    </header>

    <JobList :jobs="jobs" :order="order" />
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, ref, toRef } from 'vue';
import Job from '@/Type/Job';
import JobList from './components/JobList.vue';
import OrderTerm from './Type/OrderTerm';
export default defineComponent({
  name: 'App',
  components: {
    JobList
    // HelloWorld
  },
  setup() {
    const jobs = ref<Job[]>([
      {
        title: "f-job",
        location: "AL-HP",
        salary: 100,
        id: '1'
      },
      {
        title: "2-job",
        location: "AL-HP",
        salary: 5000,
        id: '2'
      },
      {
        title: "3-job",
        location: "AL-HP",
        salary: 3500,
        id: '3'
      },
      {
        title: "4-job",
        location: "AL-HP",
        salary: 1500,
        id: '4'
      },
    ]);
    ///
    const order = ref<OrderTerm>('title'); // init default value
    const handleClick = function (term: OrderTerm) {
      order.value = term;
    }

    return {
      jobs,
      handleClick,
      order
    }
  },


});
</script>

<style>
header {
  text-align: center;
}

header .order {
  margin-top: 20px;
}

button {
  margin: 0 10px;
  color: #1195c9;
  border: 3px solid #1195c9;
  background: #d5f0ff;
  padding: 8px 16px;
  border-radius: 4px;
  cursor: pointer;
  font-weight: bold;
}
header .title {
  display: flex;
  justify-content: center;
}
header img {
  width: 60px;
  margin-right:20;
}
</style>

