<template>
    <div class="datepicker">
      <div id="dates" 
        class="datepicker datepicker-orient-left datepicker-orient-bottom dates"
        v-bind:class="{hidden: hidden}">
          <div class="datepicker-days" style="display: block;">
              <table class=" table-condensed"  style="cursor:pointer">
                  <thead>
                      <tr>
                          <th class="prev" style="visibility: visible;" v-on:click="
                          startingMonth--; 
                          startingMonth % 12 === 11 ? year-- : year;
                          startingDay = daysInMonth(year)[(startingMonth + 2) % 12] == 28 ? startingDay : daysInMonth(year)[(startingMonth + 2) % 12] == 29 ? startingDay - 1 : daysInMonth(year)[(startingMonth + 2) % 12] == 30 ? startingDay - 2 : daysInMonth(year)[(startingMonth + 2) % 12] == 31 ? startingDay - 3 : startingDay; 
                          ">«</th>
                          <th colspan="5" class="datepicker-switch">{{month[startingMonth  % 12]}} {{year}}</th>
                          <th class="next" style="visibility: visible;" v-on:click="
                          startingMonth++; 
                          startingMonth % 12 === 0 ? year++ : year;
                          startingDay = daysInMonth(year)[(startingMonth - 1) % 12] == 28 ? startingDay : daysInMonth(year)[(startingMonth - 1) % 12] == 29 ? startingDay + 1 : daysInMonth(year)[(startingMonth - 1) % 12] == 30 ? startingDay + 2 : daysInMonth(year)[(startingMonth - 1) % 12] == 31 ? startingDay + 3 : startingDay;
                          ">»</th>
                      </tr>
                      <tr>
                          <th class="dow">Su</th>
                          <th class="dow">Mo</th>
                          <th class="dow">Tu</th>
                          <th class="dow">We</th>
                          <th class="dow">Th</th>
                          <th class="dow">Fr</th>
                          <th class="dow">Sa</th>
                      </tr>
                  </thead>
                  <tbody>
                      <tr class="center" v-for="array in func(startingMonth, year, startingDay)">
                          <td class="center" v-for="item in array">
                              <th 
                              v-on:click="
                              day = item.day;
                              currentMonth = item.month;
                              currentYear = item.year;
                              hidden = true;
                              "
                              class="day center"
                              v-bind:class="{
                                    olds: (item.month != month[startingMonth % 12]),
                                    active: item.day == day && item.month == currentMonth
                                }">{{item.day}}</th>
                          </td>
                      </tr>
                  </tbody>
              </table>
          </div>
      </div>
      <div class="panel panel-default">
          <div class="panel-heading">
              <div class="panel-title">Date Controls</div>
                <div class="panel-body">
                  <div class="row">
                    <div class="col-md-12">
                    <div class="form-group form-group-default input-group col-sm-12">
                      <label>Check In</label>
                      <input type="email" 
                        class="form-control" 
                        :value="day ? currentMonth + '/' + day + '/' + currentYear : null" 
                        id="datepicker-component2" 
                        placeholder="Pick a date"
                        v-on:click="hidden = !hidden;">
                      <span class="input-group-addon" v-on:click="hidden = !hidden;">
                        <i class="fa fa-calendar"></i>
                      </span>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>      
    </div>
</template>

<script>
import _ from 'lodash'
const isLeapYear = (year) => (year % 4 === 0 && year % 100 !== 0) || year % 400 === 0
const monthToName = { 0: 'January', 1: 'Febrauary', 2: 'March', 3: 'April', 4:'May', 5: 'June', 6: 'July', 7: 'August', 8: 'September', 9: 'October', 10: 'November', 11: 'December' }
const daysInMonth = (year) => ({ 0: 31, 1: (isLeapYear(year) ? 29 : 28), 2: 31, 3: 30, 4: 31, 5: 30, 6: 31, 7: 31, 8: 30, 9: 31, 10: 30, 11: 31 })
const abs = (num) => num < 0 ? num *= - 1 : num 
const viewCalendar = (m,y,s) => {
    let end = 0
    let calendarDays = {}
    for (let i = 0; i < 42; i++) {
        calendarDays[i] = {}
        calendarDays[i].day = 0
        calendarDays[i].month = ''
        calendarDays[i].year = 0
    }
    for (let i = 1; i <= daysInMonth(y)[m % 12]; i++) {
        calendarDays[i - 1 + (s % 7)].day = i
        calendarDays[i - 1 + (s % 7)].month = monthToName[m % 12]
        calendarDays[i - 1 + (s % 7)].year = y
    }
    for (let j = 1; j <= (42 - ((s % 7)+ daysInMonth(y)[(m) % 12])); j++) {
        calendarDays[j + (s % 7)+ daysInMonth(y)[(m) % 12] - 1].day = j
        calendarDays[j + (s % 7)+ daysInMonth(y)[(m) % 12] - 1].month = monthToName[(m + 1) % 12] 
        if (calendarDays[j + (s % 7)+ daysInMonth(y)[(m) % 12] - 1].month == 'January') {
            calendarDays[j + (s % 7)+ daysInMonth(y)[(m) % 12] - 1].year = y + 1
        } else {
            calendarDays[j + (s % 7)+ daysInMonth(y)[(m) % 12] - 1].year = y
        }
    }
    for (let i = (s % 7)- 1; i >= 0; i--) {
        calendarDays[i].day = daysInMonth(y)[(m - 1) % 12] - end
        calendarDays[i].month = monthToName[(m - 1) % 12]
        if (calendarDays[i].month == 'December') {
            calendarDays[i].year = y - 1
        } else {
            calendarDays[i].year = y
        }
        end++
    }
    return _.chunk(Object.values(calendarDays), 7)
}

export default {
  name: 'datepicker',
  components: {

  },
 data () {

    return {
      year: 2017,
      month: monthToName,
      startingMonth: 24208,
      func: viewCalendar,
      startingDay: 700001,
      day: null,
      hidden: true,
      daysInMonth: daysInMonth,
      currentMonth: null,
      currentYear: null
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="sass" scoped>
  .panel {
    margin: 200px auto 0 auto;
    width: 50%;
    background-color: rgba(255,255,255,0.4);
    position: relative;
  }
  .dates {
        display: block; 
        background-color: #f5f5f5;
        width: 240px;
        float: left;
        margin: 315px 340px;
        position: absolute;
        z-index: 1000;
    }
    .olds {
        color: rgb(175, 175, 175);
    }
    th {
        width: 20px;
    } 
    tbody:hover tr:hover td:hover th:hover {
      background: #6d5cae;
      color: white;
      cursor: pointer;
      cursor: hand;
    }
    .center {
        margin: 0 auto;
        text-align: center;
    }
    .active {
        background-color: #6d5cae;
        color: white;
        width: 20px;
        margin: 0 auto;
    }
</style>