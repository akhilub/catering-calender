<script lang="ts">
import VueCal from "vue-cal";
import { defineComponent } from "vue";
import Modal from "@/components/modal/Modal.vue"
export default defineComponent({
  components: {
    VueCal,
    Modal
  },
  data() {
    return {
      selectedEvent: {},
      showDialog: false,
      events: [
        {
          start: "2018-11-20 14:00",
          end: "2018-11-20 18:00",
          title: "Need to go shopping",
          icon: "shopping_cart", // Custom attribute.
          content: "Click to see my shopping list",
          contentFull:
            "My shopping list is rather long:<br><ul><li>Avocados</li><li>Tomatoes</li><li>Potatoes</li><li>Mangoes</li></ul>", // Custom attribute.
          class: "leisure",
        },
        {
          start: "2018-11-22 10:00",
          end: "2018-11-22 15:00",
          title: "Golf with John",
          icon: "golf_course", // Custom attribute.
          content: "Do I need to tell how many holes?",
          contentFull: "Okay.<br>It will be a 18 hole golf course.", // Custom attribute.
          class: "sport",
        },
      ],
    };
  },
  methods: {
    onEventClick(event: any, e: any) {
      this.selectedEvent = event;
      this.showDialog = true;

      // Prevent navigating to narrower view (default vue-cal behavior).
      e.stopPropagation();
    },
    close(event: any, e: any) {
      this.showDialog = false;

      // Prevent navigating to narrower view (default vue-cal behavior).
      e.stopPropagation();
    },
  },
});
</script>

<template>
  <div id="#calendar" class="text-xl font-bold justify-center">
    <p class="text-center">Calender Catering</p>
    <vue-cal
      selected-date="2018-11-19"
      :time-from="9 * 60"
      :time-to="19 * 60"
      :disable-views="['years', 'year']"
      hide-weekends
      :events="events"
      :on-event-click="onEventClick"
    >
    </vue-cal>
    <!-- Using Vuetify (but we prefer Wave UI 🤘) -->
    <Modal :showing="showDialog" @close="showDialog = false;">
      <v-card>
        <v-card-title>
          <v-icon>{{ selectedEvent.icon }}</v-icon>
          <span>{{ selectedEvent.title }}</span>
          <v-spacer />
          <strong>{{
            selectedEvent.start && selectedEvent.start.format("DD/MM/YYYY")
          }}</strong>
        </v-card-title>
        <v-card-text>
          <p v-html="selectedEvent.contentFull" />
          <strong class="text-catering-calendar-pink">Event details:</strong>
          <ul>
            <li>
              Event starts at:
              {{ selectedEvent.start && selectedEvent.start.formatTime() }}
            </li>
            <li>
              Event ends at:
              {{ selectedEvent.end && selectedEvent.end.formatTime() }}
            </li>
          </ul>
        </v-card-text>
      </v-card>
    </Modal>
  </div>
</template>
<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #e38525;
}
.vuecal__event {
  cursor: pointer;
}

.vuecal__event-title {
  font-size: 1.2em;
  font-weight: bold;
  margin: 4px 0 8px;
}

.vuecal__event-time {
  display: inline-block;
  margin-bottom: 12px;
  padding-bottom: 12px;
  border-bottom: 1px solid rgba(0, 0, 0, 0.2);
}

.vuecal__event-content {
  font-style: italic;
}

.vuecal {
  height: 90vh;
}
</style>
