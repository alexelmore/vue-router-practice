<template>
  <h1><u>Technology Jobs</u></h1>
  <div v-if="jobs.length" v-for="job in jobs" :key="job.id" class="job">
    <router-link :to="{ name: 'JobDetails', params: { id: job.id } }">
      <h2>{{ job.title }}</h2>
    </router-link>
  </div>
  <div v-else>
    Loading Job Details...
  </div>
</template>

<script>
export default {
  data() {
    return {
      jobs: [],
    };
  },
  // Use mounted lifecycle hook to send out a GET fetch request as soon as our component has mounted the DOM
  mounted() {
    // Setup a fetch request to our local db.json file for the job listings
    const url = `http://localhost:3000/jobs`;
    fetch(url)
      .then((res) => {
        return res.json();
      })
      .then((data) => {
        // Init our jobs data property with the data that gets returned.
        this.jobs = data;
      })
      // Catch and log any errors to the console.
      .catch((error) => {
        console.log(error.message);
      });
  },
};
</script>
<style>
.job h2 {
  background: #f4f4f4;
  padding: 20px;
  border-radius: 10px;
  margin: 10px auto;
  max-width: 600px;
  cursor: pointer;
  color: #444;
}
.job h2:hover {
  background: #ddd;
}
.job a {
  text-decoration: none;
}
</style>
