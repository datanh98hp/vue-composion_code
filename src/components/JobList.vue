<template>
    <div class="job-list">
        <p>Order by  {{ order }}</p>
        <!-- animation transition  -->
        <transition-group name="list" tag="ul"> 
            <li v-for="job in orderedJobs" :key="job.id">
                <h3>{{job.title}} in {{job.location}}</h3>
                <div class="salary">
                    <img src="../assets/logo.png">
                    <p>{{job.salary}} $</p>
                </div>
                <div class="description">
                    <p>
                        Lorem ipsum dolor sit amet consectetur adipisicing elit. Velit voluptatem quasi rerum, doloribus, incidunt illum ullam voluptate sapiente non provident quaerat amet quae pariatur ipsam. Sapiente, inventore magni. Tempora, voluptates!
                    </p>
                </div>
            </li>
        </transition-group>
    </div>
</template>

<script lang="ts">
import Job from '@/Type/Job'
import OrderTerm from '@/Type/OrderTerm'
import { computed, defineComponent,PropType} from 'vue'

export default defineComponent({
    props:{
        jobs: {
            required: true,
            type:Array as PropType<Job[]> // define props 
        },
        order:{
            type: String as PropType<OrderTerm>,
            required:true
        }
    },
    setup(props){
        
        // caculate before render
        const orderedJobs = computed(function(){
            return [ ... props.jobs].sort(function(a:Job,b:Job){
                return a[props.order] > b[props.order] ? 1 : -1
            })
        });

        return {
            orderedJobs
        }
    }
})
</script>
<style scoped>
.job-list {
    max-width: 960px;
    margin: 40px auto;
  }
  .job-list ul {
    padding: 0;
  }
  .job-list li {
    list-style-type: none;
    background: white;
    padding: 16px;
    margin: 16px 0;
    border-radius: 4px;
  }
  .job-list h2 {
    margin: 0 0 10px;
    text-transform: capitalize;
  }
  .salary {
    display: flex;
  }
  .salary img {
    width: 30px;
  }
  .salary p {
    color: #17bf66;
    font-weight: bold;
    margin: 10px 4px;
  }

  .list-move { 
    transition: all 1s;
  }
</style>