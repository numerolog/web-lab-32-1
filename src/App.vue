<template>
  <div id="app">
	<h1>Вариатор распада</h1>
	<stepper :steps="3" :step="stepId"></stepper>

	<div v-if="stepIs('/root')">
		<form @submit="goto('/root/identify', 2)" onsubmit="return false;" name="slon">
			<div class="formBlock">
				<label for='slon'>Выберите количество слонов, поглащающих вселенную за период распада цезия-137</label><br>
				<input id='slon' v-model='slon' name='slon' type='number' min='1' max='337' required /><br>
			</div>
			<sub><i>Не забудьте, слоны хрупкие! Небрежная раздача слонов может п<sub>р</sub>овернуть <b>нетуда</b>.</i></sub>
			<hr>
			<input type='submit' value='Продолжить'>
		</form>
	</div>
	<div v-if="stepIs('/root/identify')">
		<form @submit="goto('/root/end', 3)" onsubmit="return false;" id="name">
			<div class="formBlock">
				<label for='name'>Укажите имя</label><br>
				<input id='name' v-model='name' name='name' type='string' pattern="^[A-Za-zА-Яа-яЁё]+$" required /><br>
				<label for='name1'>Укажите фамилию</label><br>
				<input id='name1' v-model='name1' name='name1' type='string' pattern="^[A-Za-zА-Яа-яЁё]+$" required />
			</div>
			<sub><i>А вы знали, что алабамские ученые открыли новый вид проектирования веб-интерфейсов на три буквы¿</i></sub>
			<hr>
			<button v-on:click="goto('$back')">Назад</button>
			<input type='submit' value='Продолжить'>
		</form>
	</div>
	<div v-if="stepIs('/root/end')">
		<div v-if="Math.random() > 0.3">
			<div class="formBlock">
				<h3>OK!</h3>
				Кол-во слонов: {{slon}}<br>
				Поглащение: {{slon}} * 9 192 631 770 = {{slon * 9192631770}} периодов излучения.<br>
			</div>
		</div>
		<div v-else>
			<div class="formBlock">
				Уважаемый {{name}}, к сожалению не удалось произвести расчет, вернуться вначало?
			</div>
			<button v-on:click="goto('$start')">Да</button>
		</div>
	</div>
  </div>
</template>
<script>
import stepper from './components/stepper.vue'

export default {
  name: 'App',
  data: function(){
	return {
		stepStack: [],
		step: '/root',
		stepId: 1,
		
		slon: 33,
		name: 'Иван',
		name1: 'Хандусенко'
	};
  },
  methods: {
	goto(path, num){
		if (path == '$back') {
			var stepData = this.$data.stepStack.pop();
			this.$data.step = stepData[0];
			this.$data.stepId = stepData[1];
		} else if (path == '$start') {
			var first = this.$data.stepStack[0];
			this.$data.stepStack = [];
			this.goto(first[0], first[1]);
		} else {
			this.$data.stepStack.push([this.$data.step, this.$data.stepId]);
			this.$data.step = path;
			this.$data.stepId = num;
		}
	},
	stepIs(path){
		return this.$data.step == path;
	}
  },
  components: {
	stepper
  }
}
</script>

<style>
	#app {
		font-family: Avenir, Helvetica, Arial, sans-serif;
		color: rgb(43, 22, 37);
		margin-top: 60px;
		width: 70em;
		margin: 0 auto;
		padding-top: 2em;
		padding-left: 6em;
		padding-right: 3em;
		padding-bottom: 2em;
		background: rgba(22, 37, 22, 0.05);
	}
	input[type='submit'] {
		float: right;
	}
	.formBlock {
		padding-top: 2em;
		padding-left: 3em;
		padding-bottom: 2em;
	}
</style>
