<template>
  <v-app>
    <v-app-bar
      app
      color="secondary"
      dark
      absolute
      prominent
      src="https://picsum.photos/1920/1080?random"
      fade-img-on-scroll
      scroll-target="#scrolling-techniques-3"
      shrink-on-scroll
    >
      <v-spacer />
      <h2 class="pa-9">
        <div style="margin-top">
          SpaceX Timeline
        </div>
      </h2>

      <v-spacer></v-spacer>
    </v-app-bar>

    <v-content>
      <v-container>
        <v-timeline v-if="launches.length > 0">
          <launchTimelineItem
            v-for="launch in launches"
            :key="launch.flight_number"
            :launch="launch"
          />
        </v-timeline>
      </v-container>
    </v-content>

    <!-- <v-main> </v-main> -->
  </v-app>
</template>

<script>
import axios from "axios";
import LaunchTimelineItem from "./components/LaunchTimelineItem.vue";
export default {
  name: "App",

  components: {
    LaunchTimelineItem,
  },

  data: () => ({
    launches: [],
  }),

  async created() {
    const { data } = await axios.get("https://api.spacexdata.com/v3/launches");

    data.forEach((launch) => {
      this.launches.push(launch);
    }),
      console.log(this.launches);
  },
};
</script>
