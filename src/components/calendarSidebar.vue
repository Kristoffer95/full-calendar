<template>
  <div class='calendar-sidebar'>
    <!-- This is sidebar -->
    <full-calendar class="calendar-calendar"
      :options="calendarOptions"/>
    <!-- <div class='calendar-sidebar-section'>
      <h2>Instructions</h2>
      <ul>
        <li>Select dates and you will be prompted to create a new event</li>
        <li>Drag, drop, and resize events</li>
        <li>Click an event to delete it</li>
      </ul>
    </div>
    <div class='calendar-sidebar-section'>
      <label>
        <input
          type='checkbox'
          :checked='calendarOptions.weekends'
          @change='handleWeekendsToggle'
        />
        toggle weekends
      </label>
    </div>
    <div class='calendar-sidebar-section'>
      <h2>All Events ({{ currentEvents.length }})</h2>
      <ul>
        <li v-for='event in currentEvents' :key='event.id'>
          <b>{{ event.startStr }}</b>
          <i>{{ event.title }}</i>
        </li>
      </ul>
    </div> -->
  </div>
</template>

<script>
  import Vue from 'vue'

  import fullCalendar from '@fullcalendar/vue'
  import dayGridPlugin from '@fullcalendar/daygrid'
  import timeGridPlugin from '@fullcalendar/timegrid'
  import interactionPlugin from '@fullcalendar/interaction'
  
  export default Vue.extend({
    name: 'calendarSidebar',
    data() {
      return {
        calendarOptions: {
          plugins: [ dayGridPlugin, timeGridPlugin, interactionPlugin /* needed for dateClick */ ],
          headerToolbar: {
            // left: 'prev,next today',
            left: 'prev',
            center: 'title',
            right: 'next'
          },
          initialView: 'dayGridMonth',
        }
      }
    },
    components: { fullCalendar }
  })
</script>

<style lang="scss">
  .calendar-sidebar > .fc .fc-daygrid-body-unbalanced .fc-daygrid-day-events {
    min-height: 0px !important;
  }
</style>

<style lang="scss" scoped>
  .calendar-sidebar {
    width: 300px;
    padding-top: 32px;
    line-height: 1.5;
    background: white;
    border-right: 1px solid #d3e2e8;
  }
  .calendar-sidebar-section {
    padding: 2em;
  }
  // .sidebar-calendar {
  //   height: 440px;
  // }
</style>