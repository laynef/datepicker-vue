<template>
    <div class="datepicker datepicker-orient-left datepicker-orient-bottom" style="display: block; top: 2671px; left: 122px;">
        <div class="datepicker-days" style="display: block;">
            <table class=" table-condensed">
                <thead>
                    <tr>
                        <button class="prev" style="visibility: visible;" v-on:click="startingMonth--; startingMonth % 12 === 11 ? year-- : year;">«</button>
                        <th colspan="5" class="datepicker-switch">{{month[startingMonth  % 12]}} {{year}}</th>
                        <button class="next" style="visibility: visible;" v-on:click="startingMonth++; startingMonth % 12 === 0 ? year++ : year;">»</button>
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
                    <tr v-for="n in 5">
                        <td class="day" v-for="i in 7">
                            <th>{{func[n][i]}}</th>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
const _ = require('lodash')
const isLeapYear = (year) => (year % 4 === 0 && year % 100 !== 0) || year % 400 === 0
const monthToName = { 0: 'January', 1: 'Febrauary', 2: 'March', 3: 'April', 4:'May', 5: 'June', 6: 'July', 7: 'August', 8: 'September', 9: 'October', 10: 'November', 11: 'December' }
const daysInMonth = (year) => ({ 0: 31, 1: (isLeapYear(year) ? 29 : 28), 2: 31, 3: 30, 4: 31, 5: 30, 6: 31, 7: 31, 8: 30, 9: 31, 10: 30, 11: 31 })
let startingDay = 1

const viewCalendar = (m, y) => {
    let end = 0
    let calendarDays = {}
    for (let i = 0; i < 35; i++) {
        calendarDays[i] = 0
    }
    for (let i = startingDay; i <= daysInMonth(y)[m % 12]; i++) {
        calendarDays[i] = i
    }
    for (var i = startingDay + daysInMonth(y)[m % 12]; i < 35; i++) {
        calendarDays[i] = i - (daysInMonth(y)[m % 12])
    }
    for (var i = startingDay - 1; i >= 0; i--) {
        calendarDays[i] = daysInMonth(y)[(m - 1) % 12] - end
        end++
    }
    startingDay = startingDay + daysInMonth(y)[m % 12] % 7
    return _.chunk(Object.values(calendarDays), 7)
}

let array = viewCalendar(24208, 2017)

export default {
  name: 'calendar',
 data () {
    return {
        n: 0,
        i: 0,
        year: 2017,
        month: monthToName,
        startingMonth: 24208,
        func: array
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="sass" scoped>

</style>
