<template>
  <div class='calendar'>
    <calendar-sidebar />
    
    <div class='calendar-main'>
      <full-calendar
        class='calendar-calendar'
        :options='calendarOptions'
      >
        <template v-slot:eventContent='arg'>
          <b>{{ arg.timeText }}</b>
          <i>{{ arg.event.title }}</i>
        </template>
      </full-calendar>
    </div>
  </div>
</template>

<script>
import fullCalendar from '@fullcalendar/vue'
import dayGridPlugin from '@fullcalendar/daygrid'
import timeGridPlugin from '@fullcalendar/timegrid'
import interactionPlugin from '@fullcalendar/interaction'
import { INITIAL_EVENTS, createEventId } from '@/event-utils'

import calendarSidebar from '@/components/calendarSidebar'

export default {
  name: 'Home',
  components: { fullCalendar, calendarSidebar },
  data: function() {
    return {
      calendarOptions: {
        plugins: [ dayGridPlugin, timeGridPlugin, interactionPlugin /* needed for dateClick */ ],
        headerToolbar: {
          // left: 'prev,next today',
          left: '',
          center: 'today prev title next',
          right: 'timeGridDay,timeGridWeek,dayGridMonth'
        },
        // views: {
        //   dayGridMonth: { // name of view
        //     titleFormat: { year: 'numeric', month: '2-digit', day: '2-digit' }
        //     // other view-specific options here
        //   }
        // },
        initialView: 'dayGridMonth',
        initialEvents: INITIAL_EVENTS, // alternatively, use the `events` setting to fetch from a feed
        editable: true,
        selectable: true,
        selectMirror: true,
        dayMaxEvents: true,
        weekends: true,
        select: this.handleDateSelect,
        eventClick: this.handleEventClick,
        eventsSet: this.handleEvents,
        /* you can update a remote database when these fire:
        eventAdd:
        eventChange:
        eventRemove:
        */
      },
      currentEvents: []
    }
  },

  methods: {
    icon(iconName) {
      return require(`@/assets/SVG/${iconName}.svg`)
    },
    
    // FullCalendar
    handleWeekendsToggle() {
      this.calendarOptions.weekends = !this.calendarOptions.weekends // update a property
    },

    handleDateSelect(selectInfo) {
      let title = prompt('Please enter a new title for your event')
      let calendarApi = selectInfo.view.calendar

      calendarApi.unselect() // clear date selection

      if (title) {
        calendarApi.addEvent({
          id: createEventId(),
          title,
          start: selectInfo.startStr,
          end: selectInfo.endStr,
          allDay: selectInfo.allDay
        })
      }
    },

    handleEventClick(clickInfo) {
      if (confirm(`Are you sure you want to delete the event '${clickInfo.event.title}'`)) {
        clickInfo.event.remove()
      }
    },

    handleEvents(events) {
      this.currentEvents = events
    }
  }
}
</script>

<style lang='scss'>

  h2 {
    margin: 0;
    font-size: 16px;
  }
  ul {
    margin: 0;
    padding: 0 0 0 1.5em;
  }
  li {
    margin: 1.5em 0;
    padding: 0;
  }
  b { /* used for event dates/times */
    margin-right: 3px;
  }
  .calendar {
    display: flex;
    min-height: 100%;
    font-family: Arial, Helvetica Neue, Helvetica, sans-serif;
    font-size: 14px;
  }

  .calendar-main {
    flex-grow: 1;
    padding: 20px;
  }
  .fc { /* the calendar root */
    max-width: 1604px;
    margin: 0 auto;
  }

  .fc-toolbar-chunk {
    display: flex;
    align-items: center;
  }
</style>
