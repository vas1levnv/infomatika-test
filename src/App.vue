<script setup>
import {Swiper, SwiperSlide} from 'swiper/vue';
import {Pagination, Navigation} from 'swiper/modules';
import 'swiper/css';
import { ref } from 'vue'

let swiperInstance = ref(null)
const events = [
  {id: 1, place: 'Стадион', date: '30 мая', time: '17:00', teamHome: 'Соперник №9', teamGuest: 'Соперник №10'},
  {id: 2, place: 'Стадион', date: '17 июня', time: '18:00', teamHome: 'Соперник №7', teamGuest: 'Соперник №8'},
  {id: 3, place: 'Стадион', date: '26 июня', time: '19:00', teamHome: 'Соперник №1', teamGuest: 'Соперник №2'},
  {id: 4, place: 'Стадион', date: '16 июля', time: '20:00', teamHome: 'Соперник №3', teamGuest: 'Соперник №4'},
  {id: 5, place: 'Стадион', date: '30 сентября', time: '21:00', teamHome: 'Соперник №5', teamGuest: 'Соперник №6'},
]
let teamHome = ref(null)
let teamGuest = ref(null)
const onSwiper = (swiper) => {
  swiperInstance = swiper
  teamHome.value = events.find(x => x.id === swiper.activeIndex + 1).teamHome
  teamGuest.value = events.find(x => x.id === swiper.activeIndex + 1).teamGuest
};

const onSlideChange = (e) => {
  teamHome.value = events.find(x => x.id === e.activeIndex + 1).teamHome
  teamGuest.value = events.find(x => x.id === e.activeIndex + 1).teamGuest
};
const slideEventsTo = (position) => {
  swiperInstance?.slideTo(position - 1)
}
</script>

<template>
  <main>
    <div class="events-wrapper">
      <swiper
          :slides-per-view="5"
          :space-between="50"
          :centeredSlides="true"
          :initial-slide="2"
          @swiper="onSwiper"
          @slideChange="onSlideChange"
      >
        <swiper-slide
            class="events-item"
            @click="slideEventsTo(event.id)"
            v-for="event in events">
          <div class="events-item__place">{{ event.place }}</div>
          <div class="events-item__date">{{ event.date }}</div>
          <div class="events-item__time">{{ event.time }}</div>
        </swiper-slide>
      </swiper>
    </div>
    <div class="team">
      {{ teamHome }}
    </div>
    <div class="team">
      {{ teamGuest }}
    </div>
  </main>
</template>

<style scoped lang="sass">
header
  line-height: 1.5

.team
  background: white

.events
  &-wrapper
    position: relative
    width: 100vw
    //height: 100vh
    display: flex
    justify-content: center
    align-items: center

  &-item
    display: flex
    flex-direction: column
    justify-content: center
    align-items: center
    width: 100px
    height: 100px
    background: white
    color: black
    cursor: pointer

    &__place, &__time
      transition: all 0.3s ease
      transform: scale(0)

.swiper
  &-slide
    &-active
      .events-item__place, .events-item__time
        transform: scale(1)


</style>
