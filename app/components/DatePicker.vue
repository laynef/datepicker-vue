<template>
    <div class="datepicker">
      <div class="datepicker datepicker-orient-left datepicker-orient-bottom dates">
          <div class="datepicker-days" style="display: block;">
              <table class=" table-condensed">
                  <thead>
                      <tr>
                          <th class="prev" style="visibility: visible;" v-on:click="
                          startingMonth--; 
                          startingMonth % 12 === 11 ? year-- : year;
                          startingDay = func(startingMonth, year, startingDay)[4].indexOf(1) + 1;
                          ">«</th>
                          <th colspan="5" class="datepicker-switch">{{month[startingMonth  % 12]}} {{year}}</th>
                          <th class="next" style="visibility: visible;" v-on:click="
                          startingMonth++; 
                          startingMonth % 12 === 0 ? year++ : year;
                          startingDay = func(startingMonth, year, startingDay)[4].indexOf(1) + 1;
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
                      <tr v-for="array in func(startingMonth, year, startingDay)">
                          <td class="day" v-for="item in array">
                              <th v-on:click="day = item">{{item}}</th>
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
                      <input type="email" class="form-control" id="datepicker-component2" placeholder="Pick a date">
                        {{day ? month[startingMonth  % 12] + '/' + day + '/' + year : "Pick a date"}}
                      </input>
                      <span class="input-group-addon">
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
  </div>
</template>

<script>
const _ = require('lodash')
const isLeapYear = (year) => (year % 4 === 0 && year % 100 !== 0) || year % 400 === 0
const monthToName = { 0: 'January', 1: 'Febrauary', 2: 'March', 3: 'April', 4:'May', 5: 'June', 6: 'July', 7: 'August', 8: 'September', 9: 'October', 10: 'November', 11: 'December' }
const daysInMonth = (year) => ({ 0: 31, 1: (isLeapYear(year) ? 29 : 28), 2: 31, 3: 30, 4: 31, 5: 30, 6: 31, 7: 31, 8: 30, 9: 31, 10: 30, 11: 31 })

const viewCalendar = (m,y,s) => {
    let end = 0
    let calendarDays = {}
    for (let i = 0; i < 35; i++) {
        calendarDays[i] = 0
    }
    for (let i = 1; i <= daysInMonth(y)[m % 12]; i++) {
        calendarDays[i - 1 + s] = i
    }
    for (var j = 1; j <= (35 - (s + daysInMonth(y)[(m) % 12])); j++) {
        calendarDays[j + s + daysInMonth(y)[(m) % 12] - 1] = j
    }
    for (var i = s - 1; i >= 0; i--) {
        calendarDays[i] = daysInMonth(y)[(m - 1) % 12] - end
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
      startingDay: 1,
      day: null
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="sass" scoped>
  .panel {
    margin: 200px auto;
    width: 50%;
    background-color: rgba(255,255,255,0.4);
  }
  .dates {
        display: block; 
        top: 2671px; 
        left: 122px;
        background-color: #f5f5f5;
        width: 240px;
    }
</style>