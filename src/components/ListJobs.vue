<template>
  <div class="mx-auto px-5 py-24 ">
    <div class="flex flex-wrap m-4 gap-4">
      <div
        class="mx-auto w-full max-w-sm overflow-hidden rounded border bg-white shadow"
        v-for="jobs in job"
        :key="jobs.id"
      >
        <div class="relative">
          <div class="h-40 bg-cover bg-no-repeat bg-center">
            <img
              class="w-auto h-40"
              :src="jobs.company.logoUrl"
              alt="Company Logo"
            />
          </div>
        </div>
        <div class="p-3">
          <h3 class="mr-10 text-sm truncate-2nd">
            {{ jobs.title }}
          </h3>
          <div class="flex items-start justify-between">
            <span class="text-xs text-gray-500">{{
              jobs.commitment.title
            }}</span>
          </div>
          <div class="flex items-start justify-between">
            <a
              :href="jobs.websiteUrl"
              class="hover:underline text-sm hover:text-blue-500"
              >{{ jobs.company.name }}</a
            >
            <!-- <span class="text-xs text-gray-800">{{ jobs.company.name }}</span> -->
          </div>
          <div class="flex items-start justify-end">
            <a
              :href="jobs.applyUrl"
              target="_blank"
              class="hover:underline text-sm hover:text-blue-500"
              >Apply</a
            >
          </div>
          <!-- <p class="text-xs text-gray-500">
        <a href="#" class="hover:underline hover:text-blue-500">username2019</a>
        • 2 days ago
      </p> -->
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "ListJobs",
  data() {
    return {
      job: []
    };
  },

  methods: {
    async GetList() {
      const response = await axios({
        method: "POST",
        url: "https://api.graphql.jobs/",
        data: {
          query: `
                {
                    jobs{
                        title
                        commitment{
                            title
                        }
                       company{
                           name
                           logoUrl
                           websiteUrl
                       }
                        applyUrl
                        cities{
                            name
                        }
                    }
                }
            `
        }
      });
      this.job = response.data.data.jobs;
      console.log(this.job);
    }
  },
  mounted() {
    this.GetList();
  }
};
</script>

<style></style>
