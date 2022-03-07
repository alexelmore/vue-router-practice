<template>
  <div v-if="job">
    <h1>Job Overview</h1>
    <p><strong>Job Title:</strong> {{ job.title }}</p>
    <p><strong>Job ID:</strong> {{ id }}</p>
    <p><strong>Job Details:</strong> {{ job.details }}</p>
  </div>
  <div v-else>Loading Job Details...</div>
</template>

<script>
export default {
  props: ["id"],
  data() {
    return {
      job: null,
    };
  },
  // Use mounted lifecycle hook to send out a GET fetch request as soon as our component has mounted the DOM
  mounted() {
    // Setup a fetch request to our local db.json file for the indiviual job listings, using the job id in the url
    const url = `http://localhost:3000/jobs/${this.id}`;
    fetch(url)
      .then((res) => {
        return res.json();
      })
      // Init our job data property with the data that gets returned.
      .then((data) => {
        this.job = data;
      })
      // Catch and log any errors to the console.
      .catch((error) => {
        console.log(error.message);
      });
  },
};
</script>

<style></style>
