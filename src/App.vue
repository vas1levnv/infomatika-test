<script setup>
import {Swiper, SwiperSlide} from 'swiper/vue';
import {Pagination, Navigation} from 'swiper/modules';
import 'swiper/css';
import {ref} from 'vue'

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
				:centeredSlides="true"
				:initial-slide="2"
				@swiper="onSwiper"
				@slideChange="onSlideChange"
			>
				<swiper-slide
					@click="slideEventsTo(event.id)"
					v-for="event in events">
					<div class="events-item">
						<div class="events-item__place">{{ event.place }}</div>
						<div class="events-item__date">{{ event.date }}</div>
						<div class="events-item__time">{{ event.time }}</div>
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

<style scoped lang="sass">
header
	line-height: 1.5

.team
	background: white
	position: absolute
	z-index: 10
	font-size: 3rem
	
	&-home
		top: 50%
		left: 50%
		transform: translate(-165%, -210%)
		
		
		&:before
			content: ""
			position: absolute
			top: -40px
			right: -40px
			width: 2000px
			height: 150px
			-webkit-transform: skew(-30deg)
			-moz-transform: skew(-30deg)
			-o-transform: skew(-30deg)
			background: white
			border-radius: 15px
			z-index: -2
		
	&-guest
		bottom: 50%
		right: 50%
		transform: translate(165%, 185%)
		&:before
			content: ""
			position: absolute
			top: -40px
			left: -40px
			width: 2000px
			height: 150px
			-webkit-transform: skew(-30deg)
			-moz-transform: skew(-30deg)
			-o-transform: skew(-30deg)
			background: white
			border-radius: 15px
			z-index: -2
		
.events
	&-wrapper
		position: relative
		width: 100vw
		height: 100vh
		display: flex
		justify-content: center
		align-items: center
	
	&-item
		display: flex
		flex-direction: column
		justify-content: center
		background: white
		color: black
		cursor: pointer
		position: relative
		top: 0
		margin: 0 auto
		width: 4em
		height: 6.52em
		border-radius: 6px
		transition: all .6s ease
		align-items: center
		text-align: center
		
		&:before, &:after
			position: absolute
			width: inherit
			height: inherit
			border-radius: inherit
			background: inherit
			content: ""
			z-index: -1
		&:before
			position: absolute
			top: 0
			transform: rotate(60deg)
		&:after
			position: absolute
			top: 0
			transform: rotate(-60deg)
			
		&__place, &__time
			transition: all 0.3s ease
			transform: scale(0)

.swiper
	width: 100%
	height: 100%
	
	&-slide
		display: flex
		align-items: center
		.events-item
			margin-top: auto
			margin-bottom: 20%
		&-active
			.events-item
				transform: scale(3)
				margin: auto
			.events-item__place, .events-item__time
				transform: scale(1)
		&-prev
			.events-item
				margin-top: 150%
				margin-bottom: 0
				transform: scale(1.5)
		&-next
			
			& + .swiper-slide
				margin-top: 20%
				margin-bottom: auto
			
			.events-item
				margin-top: 0
				margin-bottom: 150%
				transform: scale(1.5)
</style>
