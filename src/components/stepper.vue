<template>
	<div>
		<div class="row">
			<div class="col-xs-12 col-md-8 offset-md-2 block border">
				<div class="wrapper-stepsBar">
					<ul class="stepsBar">
						<li 
						v-for="s in steps" :key="s"
						:class="{ 'active': s <= step }"><div>{{s}}</div></li>
					</ul>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
  props: ["steps", "step"]
};
</script>

<style>
	.wrapper-stepsBar {
		width: 100%
	}

	.stepsBar li {
		list-style-type: none;
		float: left;
		width: 33%;
		position: relative;
		text-align: center;
		font-weight: bold;
	}
	
	.stepsBar li div {
		line-height: 30px;
		border-radius: 50%;
		width: 30px;
		height: 30px;
		border: 1px solid #ddd;
		display: block;
		text-align: center;
		margin: 0 auto 10px;
		background-color: white
	}

	.stepsBar li.active div {
		border-color: dodgerblue;
		background-color: dodgerblue;
		color: white;
	}

	.stepsBar li:after {
		content: "";
		position: absolute;
		width: 100%;
		height: 4px;
		background-color: #ddd;
		top: 15px;
		left: -50%;
		z-index: -1;
	}

	.stepsBar li:first-child:after {
		content: none;
	}

	.stepsBar li.active {
		color: dodgerblue;
	}
	.stepsBar li.active:before {
		border-color: dodgerblue;
		background-color: dodgerblue
	}
	.stepsBar .active:after {
		background-color: dodgerblue;
	}
	
	
</style>