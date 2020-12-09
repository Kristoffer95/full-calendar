<template>
  <div class='calendar-sidebar'>
    <!-- This is sidebar -->
    <full-calendar class="calendar-calendar"
      :options="calendarOptions"/>
    
    <!-- <hr style="border-color: #E4E4E4;"/> -->
    <div class="find-customer">
      <div>
        <span>Find Customer</span>
      </div>
      <img :src="icon('add-arrow')" alt="">
    </div>
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
    components: { fullCalendar },
    methods: {
      icon(iconName) {
        return require(`@/assets/SVG/${iconName}.svg`)
      },
    }
  })
</script>

<style lang="scss">
  .calendar-sidebar {
    padding: 0 34px 0 34px;
    > .fc {
      max-width: 225px;
      height: 260px;

      .fc-daygrid-day-events {
        min-height: 0px !important;
      }
      // header
      .fc-header-toolbar {
        // border: 1px solid red;
        margin-bottom: 12px !important;
        // display: flex;
        // justify-content: center;
        // align-items: center;
        line-height: 0;
      }
      // title
      .fc-toolbar-title {
        font-size: 18px;
        font-weight: 500;
      }
      // prev
      button.fc-prev-button.fc-button.fc-button-primary {
        color: #30A26B !important;
        background-color: transparent;
        border: transparent;
        padding: 0 !important;
        margin-top: -2px;
      }
      // next
      button.fc-next-button.fc-button.fc-button-primary {
        color: #30A26B !important;
        background-color: transparent;
        border: transparent;
        padding: 0 !important;
        margin-top: -2px;
      }
      .fc-daygrid-day-top {
        justify-content: center !important;
        align-items: center;
      }
      .fc-scroller {
        overflow: hidden !important;
      }
      .fc-scroller.fc-scroller-liquid-absolute {
        overflow: hidden !important;
      }
      .fc-scrollgrid-liquid {
        height: 213px !important;
      }

      table, tbody, tr, td, th {
        border: hidden;
      }
    }
    > .find-customer {
      border-top: 1px solid #E4E4E4;
      border-bottom: 1px solid #E4E4E4;
      width: 100%;
    }
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