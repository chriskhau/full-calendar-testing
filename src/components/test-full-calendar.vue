<template>
  <div class='demo-app'>
    <div class='demo-app-top'>
    </div>
    <FullCalendar
      class='demo-app-calendar'
      ref="fullCalendar"
      defaultView="timeGrid"
      :header="{
        left: 'prev,next today',
        center: 'title',
        right: 'dayGridMonth,timeGridWeek,timeGridDay,listWeek'
      }"
      :plugins="calendarPlugins"
      :weekends="calendarWeekends"
      :events="calendarEvents"
      :selectable="selectable"
      :visibleRange="visibleRange"
      :allDaySlot="false"
      slotDuration='01:00:00'
      minTime='9:00:00'
      maxTime='22:00:00'

      @select="select"
      
      />
  </div>
</template>

<script>
import FullCalendar from '@fullcalendar/vue'
import dayGridPlugin from '@fullcalendar/daygrid'
import timeGridPlugin from '@fullcalendar/timegrid'
import interactionPlugin from '@fullcalendar/interaction'
export default {
  components: {
    FullCalendar // make the <FullCalendar> tag available
  },
  data: function() {
    return {
      calendarPlugins: [ // plugins must be defined in the JS
        dayGridPlugin,
        timeGridPlugin,
        interactionPlugin // needed for dateClick
      ],
      selectable:true,
      calendarWeekends:true,
      calendarEvents: [ // initial event data
        { title: 'Event Now', start: new Date() , end: new Date()}
      ],
      visibleRange:{
         start: '2017-03-22',
            end: '2017-03-25'
      }
    //   select:function(info){
    //       alert('selected '+ info.dateStr);
          
    //   }
    }
  },
  methods: {
    toggleWeekends() {
      this.calendarWeekends = !this.calendarWeekends // update a property
    },
    gotoPast() {
      let calendarApi = this.$refs.fullCalendar.getApi() // from the ref="..."
      calendarApi.gotoDate('2000-01-01') // call a method on the Calendar object
    },
    handleDateClick(arg) {
      if (confirm('Would you like to add an event to ' + arg.dateStr + ' ?')) {
        this.calendarEvents.push({ // add new event data
          title: 'New Event',
          start: arg.date,
          allDay: arg.allDay
        })
      }
    },
    select(arg){
        if (confirm(arg.startStr + ' - ' +arg.endStr)){
            this.calendarEvents.push({
                title:"new Event",
                start:arg.start,
                end:arg.end,
                allDay:arg.allDay
            })
            console.log(arg);
        }
    }

    
  }
}
</script>

<style lang='scss'>
// you must include each plugins' css
// paths prefixed with ~ signify node_modules
@import '~@fullcalendar/core/main.css';
@import '~@fullcalendar/daygrid/main.css';
@import '~@fullcalendar/timegrid/main.css';
.demo-app {
  font-family: Arial, Helvetica Neue, Helvetica, sans-serif;
  font-size: 14px;
}
.demo-app-top {
  margin: 0 0 3em;
}
.demo-app-calendar {
  margin: 0 auto;
  max-width: 900px;
}
.fc-time-grid .fc-slats td{
  height:3em
}
</style>