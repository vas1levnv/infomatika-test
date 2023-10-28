<script setup>
import {Swiper, SwiperSlide} from 'swiper/vue';
import {Mousewheel} from "swiper/modules";
import Header from "@/components/Header.vue";
import 'swiper/css';
import {ref} from 'vue'

let swiperInstance = ref(null)
const events = [
  {id: 1, place: 'Стадион', date: '30 мая', time: '17:00', teamHome: 'Соперник №9', teamGuest: 'Соперник №10', link: 'https://www.youtube.com/watch?v=bVSJLMkDxbE&ab_channel=%D0%9F%D0%B5%D1%80%D0%B5%D0%BC%D0%BE%D1%82%D0%BA%D0%B0%2FPeremotka'},
  {id: 2, place: 'Стадион', date: '17 июня', time: '18:00', teamHome: 'Соперник №7', teamGuest: 'Соперник №8', link: 'https://www.youtube.com/watch?v=bVSJLMkDxbE&ab_channel=%D0%9F%D0%B5%D1%80%D0%B5%D0%BC%D0%BE%D1%82%D0%BA%D0%B0%2FPeremotka'},
  {id: 3, place: 'Стадион', date: '26 июня', time: '19:00', teamHome: 'Соперник №1', teamGuest: 'Соперник №2', link: 'https://www.youtube.com/watch?v=bVSJLMkDxbE&ab_channel=%D0%9F%D0%B5%D1%80%D0%B5%D0%BC%D0%BE%D1%82%D0%BA%D0%B0%2FPeremotka'},
  {id: 4, place: 'Стадион', date: '16 июля', time: '20:00', teamHome: 'Соперник №3', teamGuest: 'Соперник №4', link: 'https://www.youtube.com/watch?v=bVSJLMkDxbE&ab_channel=%D0%9F%D0%B5%D1%80%D0%B5%D0%BC%D0%BE%D1%82%D0%BA%D0%B0%2FPeremotka'},
  {id: 5, place: 'Стадион', date: '30 сентября', time: '21:00', teamHome: 'Соперник №5', teamGuest: 'Соперник №6', link: 'https://www.youtube.com/watch?v=bVSJLMkDxbE&ab_channel=%D0%9F%D0%B5%D1%80%D0%B5%D0%BC%D0%BE%D1%82%D0%BA%D0%B0%2FPeremotka'},
]
let teamHome = ref(null)
let teamGuest = ref(null)
const onSwiper = (swiper) => {
  swiperInstance = swiper
};

const onSlideChange = (e) => {
  teamHome.value = events.find(x => x.id === e.activeIndex + 1).teamHome
  teamGuest.value = events.find(x => x.id === e.activeIndex + 1).teamGuest
};
const slideEventsTo = (position) => {
  swiperInstance?.slideTo(position - 1)
}

const modules = [Mousewheel]

</script>

<template>
  <Header/>
  <main>
    <div class="events-wrapper">
      <swiper
          :slides-per-view="5"
          :modules="modules"
          :centeredSlides="true"
          :initial-slide="2"
          :watchSlidesProgress="true"
          :mousewheel="true"
          :speed="1500"
          @swiper="onSwiper"
          @slideChange="onSlideChange"
      >
        <swiper-slide
            @click="slideEventsTo(event.id)"
            v-slot="{ isVisible }"
            v-for="event in events">
          <div class="events-item" :class="{notVisible: !isVisible}">
            <div class="events-item__place">{{ event.place }}</div>
            <div class="events-item__date">{{ event.date }}</div>
            <div class="events-item__time">{{ event.time }}</div>
            <a class="events-item__link" :href="event.link" target="_blank">Купить</a>
          </div>
        </swiper-slide>
      </swiper>
      <div class="team team-home">
        {{ teamHome }}
      </div>
      <div class="team team-guest">
        {{ teamGuest }}
      </div>
    </div>
  </main>
</template>

<style scoped lang="scss">
.team {
  position: absolute;
  z-index: 10;
  width: 310px;
  font-size: 3rem;
  white-space: nowrap;
  color: black;

  &-home {
    top: 50%;
    left: 50%;
    transform: translate(-165%, -210%);

    &:before {
      content: "";
      position: absolute;
      top: -40px;
      right: -40px;
      width: 2000px;
      height: 150px;
      -webkit-transform: skew(-30deg);
      -moz-transform: skew(-30deg);
      -o-transform: skew(-30deg);
      background: white;
      border-radius: 15px;
      z-index: -2;
    }
  }

  &-guest {
    bottom: 50%;
    right: 50%;
    transform: translate(165%, 185%);

    &:before {
      content: "";
      position: absolute;
      top: -40px;
      left: -40px;
      width: 2000px;
      height: 150px;
      -webkit-transform: skew(-30deg);
      -moz-transform: skew(-30deg);
      -o-transform: skew(-30deg);
      background: white;
      border-radius: 15px;
      z-index: -2;
    }
  }
}

.events {
  &-wrapper {
    position: relative;
    width: 100vw;
    height: 100vh;
    overflow: hidden;
    display: flex;
    justify-content: center;
    align-items: center;

    &:before{
      content: '';
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 35vw;
      height: 35vw;
      border-radius: 50%;
      border: 2px solid white;
    }
    &:after{
      content: '';
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 60vw;
      height: 60vw;
      border-radius: 50%;
      border: 2px solid white;
    }
  }

  &-item {
    display: flex;
    flex-direction: column;
    justify-content: center;
    background: white;
    color: black;
    cursor: pointer;
    position: relative;
    top: 0;
    margin: 0 auto;
    width: 4em;
    height: 6.52em;
    border-radius: 6px;
    transition: all .6s ease;
    align-items: center;
    text-align: center;

    &:before, &:after {
      position: absolute;
      width: inherit;
      height: inherit;
      border-radius: inherit;
      background: inherit;
      content: "";
      z-index: -1;
    }

    &:before {
      position: absolute;
      top: 0;
      transform: rotate(60deg);
    }

    &:after {
      position: absolute;
      top: 0;
      transform: rotate(-60deg);
    }

    &__date{
      font-weight: 600;
      white-space: nowrap;
    }

    &__place, &__time, &__link {
      transition: all 0.3s ease;
      display: none;
    }

    &__link{
      padding: 0.25rem 0.5rem;
      border-radius: 0.25rem;
      border: 1px solid black;
      &:hover{
        background: black;
      }
    }
  }
}

.notVisible {
  display: none;
}

.swiper {
  width: 80%;
  height: 100%;

  &-slide {
    display: flex;
    align-items: center;
    justify-content: end;

    .events-item {
      margin-right: 0;
      transition: all 1.5s ease;
      transform: translateY(250%);
    }

    &-active {
      .events-item {
        margin: 0 auto;
        transform: translateY(0) scale(3);
      }

      .events-item__place, .events-item__time, .events-item__link {
        transform: scale(0.75);
        display: block;
      }
    }

    &-prev {
      .events-item {
        margin: 0 auto;
        transform: translateY(150%) scale(1.5);
      }
    }

    &-next {
      .events-item {
        margin: 0 auto;
        transform: translateY(-150%) scale(1.5);
      }

      & + .swiper-slide {
        .events-item {
          margin-left: 0;
          margin-right: auto;
          transform: translateY(-250%);
        }
      }
    }
  }
}

</style>
