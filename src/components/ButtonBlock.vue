<template>
  <div btn-group data-grouptype="И">
    <a v-on:click.stop.prevent="Submit">Сканировать</a>
    <a v-on:click.stop.prevent="Save">Сохарнить PDF</a>
  </div>
</template>

<script>
export default {
  methods:{
    Submit(){
       this.$emit('ScanButtonHandler', event)
    },
  Save(){
    this.$emit('SaveButtonHandler', event)
  }
  }
}
</script>

<style scoped>
[btn-group] {
	position:relative;
	display:inline-block;
	margin:10px 0;
}

[btn-group]:before {
	content:attr(data-grouptype);
	color:#999;
	display:block;
	font-size:0.7125em;
	width:19px;
	height:19px;
	padding:5px;
	border-radius:50%;
	background:#FFF;
	position:absolute;
	left:49%;
	top:6px;
	margin-left:-18px;
	line-height:19px;
}

[btn-group] > a + a {
	margin-left:5px;
}

[btn-group] > a {
	display:inline-block;
	padding:6px 14px;
	background:#F2F2F2;
	border-radius:3px;
	font-size:0.8125em;
	color:#B9BCBC;
	transition:background .3s ease, color .3s ease;
	text-decoration:none;
	transition:color .3s ease;
	padding:12px 28px;
	text-transform:uppercase;
}

[btn-group] > a:nth-of-type(1) {
	background:#A1D36E;
	color:#FFF;
}

[btn-group] > a:nth-of-type(1):hover {
	background:#94CD5A;
}

[btn-group] > a:nth-of-type(2) {
	background:#6AD1DD;
	color:#FFF;
}

[btn-group] > a:nth-of-type(2):hover {
  cursor: pointer;
	background:#55CBD8;
}
</style>