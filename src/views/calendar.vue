<template>
  <div class='calendar'>
    <calendar-sidebar />
    
    <div class='calendar-main'>
      <!-- <div class="calendar-main-top">
        <div>
          <span><i class="icon-sidebar-arrow-close cursor-pointer" style="font-size: 20px;" /></span>
        </div>

        <div>
          <img class="cursor-pointer"
            :src="icon('settings-icon')" alt="">
        </div>
      </div> -->
      <full-calendar id="calendar-main"
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
  },
  mounted() {
    

    // getting the id="calendar-main"
    let calenarHeader = document.getElementById("calendar-main").children[0]

    // hide sidebar button
    const div = document.createElement('div');
    div.classList.add('sidebar-visible')
    const hideSidebar = document.createElement('img')
    hideSidebar.classList.add('cursor-pointer')
    hideSidebar.setAttribute('src', `${this.icon('sidebar-arrow-close')}`)
    calenarHeader.children[0].appendChild(div).appendChild(hideSidebar)
    
    // Add Appointment
    const addAppointmentBtn = document.createElement('div')
    addAppointmentBtn.classList.add('calendar-add-appointment')
    addAppointmentBtn.classList.add('cursor-pointer')
    const addIcon = document.createElement('i')
    addIcon.classList.add('icon-add-arrow')
    const span = document.createElement('span')
    const spanTest = document.createTextNode('Add Appointment')
    calenarHeader.children[0].appendChild(addAppointmentBtn).appendChild(addIcon)
    calenarHeader.children[0].children[1].appendChild(span).appendChild(spanTest)

    // settings
    const settings = document.createElement('img')
    settings.classList.add('cursor-pointer')
    settings.setAttribute('src', `${this.icon('settings-icon')}`)
    calenarHeader.children[2].appendChild(settings)
    
    // console.log(document.getElementById("calendar-main").children[0].children[2].appendChild(div).appendChild(i))
  }
}
</script>

<style lang='scss'>

  .calendar-main {
    // border: 1px solid red;
    position: relative;
    > .calendar-main-top {
      // border: 1px solid red;
      position: absolute;
      width: 100%;
      max-width: 1604px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      left: 50%;
      transform: translate(-50%, 0);
      padding: 0 20px;
    }

    > .calendar-calendar {
      .fc-button-group {
        margin-right: 64px;
      }
      button.fc-today-button.fc-button.fc-button-primary {
        margin-left: 64px;
      }
    }
  }

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
