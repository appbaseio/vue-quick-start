<template>
	<div id="app">
		<reactive-base
			url="https://appbase-demo-ansible-abxiydt-arc.searchbase.io"
			app="good-books-ds"
			credentials="04717bb076f7:be54685e-db84-4243-975b-5b32ee241d31"
		>
			<h1>Hello from ReactiveBase 👋</h1>
		</reactive-base>
	</div>
</template>

<script>
import { ReactiveBase } from '@appbaseio/reactivesearch-vue';

export default {
  name: 'App',
  components: {
    ReactiveBase
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
