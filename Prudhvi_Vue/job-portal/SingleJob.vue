<template>
  <div :class="['job-card', job.SalaryType === 'Paid' ? 'paid' : 'unpaid']">
    <div class="job-header">
      <img v-if="job.CompanyLogo" :src="job.CompanyLogo" alt="Company logo" class="company-logo" />
      <div class="job-header-text">
        <h2 class="company-name">{{ job.CompanyName }}</h2>
        <h3 class="job-title">{{ job.JobTitle }}</h3>
        <p class="job-type">{{ job.JobType }} - {{ job.Location }}</p>
      </div>
    </div>
    <p class="salary">{{ job.SalaryType }} - {{ job.EstimatedSalary }}</p>
    <p class="description">{{ job.JobDescription }}</p>
    <div class="card-footer">
      <a :href="job.ApplyLink" target="_blank" class="apply-button" aria-label="Apply for this job">Apply Now</a>
      <div v-if="job.IsRemote" class="remote-tag">Remote</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SingleJob',
  props: {
    job: {
      type: Object,
      required: true
    }
  }
}
</script>

<style scoped>
.job-card {
  background-color: #fff;
  border-radius: 10px;
  padding: 20px;
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.08);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  position: relative;
  display: grid;
  grid-template-rows: auto auto auto 1fr auto;
  grid-gap: 10px;
  height: 100%;
}

.job-card.paid {
  border-left: 8px solid #27ae60;
}

.job-card.unpaid {
  border-left: 8px solid #c0392b;
}

.job-card:hover {
  transform: translateY(-8px);
  box-shadow: 0 12px 24px rgba(0, 0, 0, 0.15);
}

/* Using CSS Grid for job-header instead of flexbox */
.job-header {
  display: grid;
  grid-template-columns: auto 1fr;
  grid-gap: 15px;
  margin-bottom: 12px;
}

.company-logo {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  float: left; /* Using float as an alternative approach */
}

.job-header-text {
  overflow: hidden; /* Clearfix for the floated logo */
}

.company-name {
  font-size: 1.6rem;
  font-weight: bold;
  color: #2c3e50;
  margin-top: 0;
  margin-bottom: 5px;
}

.job-title {
  font-size: 1.4rem;
  font-weight: 600;
  color: #34495e;
  margin-top: 0;
  margin-bottom: 5px;
}

.job-type {
  font-size: 1rem;
  color: #7f8c8d;
  margin-top: 0;
  margin-bottom: 0;
}

.salary {
  font-size: 1.1rem;
  font-weight: bold;
  color: #16a085;
  margin-top: 10px;
}

.description {
  font-size: 1rem;
  color: #555;
  line-height: 1.6;
  margin-top: 10px;
  display: -webkit-box;
  -webkit-line-clamp: 4;
  -webkit-box-orient: vertical;
  overflow: hidden;
  text-overflow: ellipsis;
  max-height: 96px; /* Approximately 4 lines of text */
}

.apply-button {

  display: block;

  background-color: #3498db;

  color: #fff;

  padding: 10px 20px;

  border-radius: 6px;

  text-align: center;

  text-decoration: none;

  font-weight: bold;

  transition: all 0.3s ease;

  width: fit-content;

  margin-top: auto;

  align-self: end;

  position: relative;

  overflow: hidden;

  z-index: 1;

  cursor: pointer; /* Add this line */
}


.apply-button:before {
  content: "";
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 0;
  background-color: #2980b9;
  transition: all 0.3s ease;
  z-index: -1;
}

.apply-button:hover {
  transform: translateY(-3px);
  box-shadow: 0 5px 15px rgba(52, 152, 219, 0.4);
  color: #fff;
}

.apply-button:hover:before {
  height: 100%;
}

.card-footer {
  display: grid;
  grid-template-columns: auto 1fr;
  align-items: center;
  margin-top: auto;
}

.remote-tag {
  background-color: #f39c12;
  color: white;
  padding: 6px 12px;
  border-radius: 4px;
  font-weight: bold;
  font-size: 1rem;
  justify-self: end;
}
</style>