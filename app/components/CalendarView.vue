<template>
    <div class="datepicker datepicker-orient-left datepicker-orient-bottom" style="display: block; top: 2671px; left: 122px;">
        <div class="datepicker-days" style="display: block;">
            <table class=" table-condensed">
                <thead>
                    <tr>
                        <button class="prev" style="visibility: visible;" v-on:click="startingMonth--">«</button>
                        <th colspan="5" class="datepicker-switch">{{month[startingMonth  % 12]}} {{year}}</th>
                        <button class="next" style="visibility: visible;" v-on:click="startingMonth++">»</button>
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
                <tbody v-for="n in 6">
                    <tr v-for="day in days">
                     <!--   {{<td class={{day.class}}>{{day.number}}</td>}} -->
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
const isLeapYear = (year) => (year % 4 === 0 && year % 100 !== 0) || year % 400 === 0
const daysInMonth = (year) => ({ 1: 31, 2: (isLeapYear(year) ? 29 : 28), 3: 31, 4: 30, 5: 31, 6: 30, 7: 31, 8: 31, 9: 30, 10: 31, 11: 30, 12: 31 })
const monthToName = { 0: 'January', 1: 'Febrauary', 2: 'March', 3: 'April', 4:'May', 5: 'June', 6: 'July', 7: 'August', 8: 'September', 9: 'October', 10: 'November', 11: 'December' }
const daysToName = { 0: 'Sunday', 1: 'Monday', 2: 'Tuesday', 3: 'Wednesday', 4: 'Thursday', 5: 'Friday', 6: 'Saturday' }
let startingYear = 2017
let startingMonth = 28
let startingDay = 1

export default {
  name: 'calendar',
 data () {
    return {
        n: 1,
        year: startingYear,
        month: monthToName,
        startingYear: 2017,
        startingMonth: 28
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="sass" scoped>

</style>
