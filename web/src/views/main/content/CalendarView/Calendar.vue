<script setup lang="ts">
import { Icon } from '@iconify/vue'
import {
  CalendarCell,
  CalendarCellTrigger,
  CalendarGrid,
  CalendarGridBody,
  CalendarGridHead,
  CalendarGridRow,
  CalendarHeadCell,
  CalendarHeader,
  CalendarHeading,
  CalendarNext,
  CalendarPrev,
  CalendarRoot,
  type CalendarRootProps,
} from 'radix-vue'
import './styles.css'

const isDateUnavailable: CalendarRootProps['isDateUnavailable'] = (date) => {
  //   return date.day === 17 || date.day === 18
  return null
}

const emit = defineEmits(['dateSelected'])

const handleDateClick = (day) => {
  // console.log(day)
  emit('dateSelected', day)
}
</script>

<template>
  <div class="Canlendar-View">
    <CalendarRoot
      v-slot="{ weekDays, grid }"
      :is-date-unavailable="isDateUnavailable"
      class="Calendar"
      fixed-weeks
    >
      <CalendarHeader class="CalendarHeader">
        <CalendarPrev class="CalendarNavButton leftButton">
          <Icon icon="radix-icons:chevron-left" class="Icon" />
        </CalendarPrev>
        <CalendarHeading class="CalendarHeading" />
        <CalendarNext class="CalendarNavButton rightButton">
          <Icon icon="radix-icons:chevron-right" class="Icon" />
        </CalendarNext>
      </CalendarHeader>

      <div class="Canlendar-Connector-left"></div>
      <div class="Canlendar-Connector-right"></div>

      <div class="CalendarWrapper">
        <CalendarGrid v-for="month in grid" :key="month.value.toString()" class="CalendarGrid">
          <CalendarGridHead>
            <CalendarGridRow class="CalendarGridRow">
              <CalendarHeadCell v-for="day in weekDays" :key="day" class="CalendarHeadCell">
                {{ day }}
              </CalendarHeadCell>
            </CalendarGridRow>
          </CalendarGridHead>
          <CalendarGridBody class="CalendarGridWrapper">
            <CalendarGridRow
              v-for="(weekDates, index) in month.rows"
              :key="`weekDate-${index}`"
              class="CalendarGridRow"
            >
              <CalendarCell
                v-for="weekDate in weekDates"
                :key="weekDate.toString()"
                :date="weekDate"
                class="CalendarCell"
              >
                <CalendarCellTrigger
                  :day="weekDate"
                  :month="month.value"
                  class="CalendarCellTrigger"
                  @click="handleDateClick(weekDate)"
                />
              </CalendarCell>
            </CalendarGridRow>
          </CalendarGridBody>
        </CalendarGrid>
      </div>
    </CalendarRoot>
  </div>
</template>