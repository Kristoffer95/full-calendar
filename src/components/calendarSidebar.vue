<template>
  <div class='calendar-sidebar'>
    <!-- This is sidebar -->
    <full-calendar class="calendar-calendar"
      :options="calendarOptions"/>
    
    <!-- <hr style="border-color: #E4E4E4;"/> -->
    <div class="find-customer">
      <div class="find-customer-top">
        <span class="find-customer-title">Find Customer</span>
        <div class="find-customer-topRight">
          <i class="icon-add-arrow cursor-pointer" style="margin-right: 24px;"></i>
          <i class="icon-collapse-arrow cursor-pointer"></i>
        </div>
      </div>

      <div class="find-customer-bottom">
        <i class="icon-search-icon" />
        <input type="text" placeholder="Customer name...">
      </div>
      <!-- <img :src="icon('add-arrow')" alt=""> -->
    </div>

    <div class="calendars-list">
      <div class="calendars-top">
        <span class="calendars-title">Calendars</span>
        <div class="calendars-topRight">
          <i class="icon-add-arrow cursor-pointer" style="margin-right: 24px;"></i>
          <i class="icon-collapse-arrow cursor-pointer"></i>
        </div>
      </div>

      <div class="list-wrapper">
        <div class="list list-top">
          <input class="list-checkbox" type="checkbox">
          <span style="color: red;">Select All(N selected)</span>
        </div>

        <div class="list" v-for="(list, listIndex) in calendarsList" :key="listIndex">
          <input type="checkbox">
          <div class="list-image"></div>
          <span class="list-name">{{ list.name }}</span>
        </div>

        <div class="list-edit cursor-pointer">
          <i class="icon-edit-calendars-icon" />
          <span class="">Edit calendars</span>
        </div>

      </div>
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
        calendarsList: [
          { name: 'Matthew Skilton', selected: false },
          { name: 'Very long name and last name', selected: false },
          { name: 'Tedy Bargle', selected: false },
          { name: 'John Doe', selected: false },
        ],
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
        margin: 0 10px;
        padding: 30px 0;
        
      .find-customer-top {
        display: flex;
        justify-content: space-between;
        align-items: center;
        span.find-customer-title {
          font-size: 14px;
          font-weight: 600;
        }
        .find-customer-topRight {
          display: flex
        }
      }

      .find-customer-bottom {
        border: 1px solid #D5D7D6;
        padding: 10px;
        display: flex;
        border-radius: 50px;
        margin-top: 18px;

        i {
          font-size: 18px;
        }
        input {
          border: 0;
          width: 150px;
          background: transparent;
          outline: none;
          margin-left: 11px;
          font-size: 14px;
        }
      }
    }
    .calendars-list {
      padding: 0 10px;

      .calendars-top {
        margin-top: 30px;
        display: flex;
        justify-content: space-between;
        .calendars-title {
          font-size: 14px;
          font-weight: 600;
        }
        .calendars-topRight {
          display: flex;
          align-items: center;
        }
      }
      .list-wrapper {

        .list {
          margin-top: 21px;
          display: flex;
          align-items: flex-start;

          input {
            min-width: 18px;
            height: 18px;
            margin-top: 2px;
            margin-right: 5px;
            // align-self: center;
          }
          .list-image {
            min-width: 28px;
            height: 28px;
            background-color: #30A26B;
            border-radius: 50px;
            margin-right: 5px;
            // align-self: center;
          }
          .list-name {
            color: #3F4140;
          }
        }
        .list-edit {
          display: flex;
          align-items: center;
          // border: 1px solid red;
          margin-top: 22px;

          i {
            font-size: 18px;
            margin-right: 8px;
          }
          span {
            font-size: 14px;
            color: #30A26B;
            font-weight: 500;
          }
        }
      }
      
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