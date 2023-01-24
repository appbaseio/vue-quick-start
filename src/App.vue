<template>
	<div id="app">
		<reactive-base
			url="https://appbase-demo-ansible-abxiydt-arc.searchbase.io"
			app="good-books-ds"
			credentials="04717bb076f7:be54685e-db84-4243-975b-5b32ee241d31"
		>
      <search-box
        componentId="SearchBox"
        placeholder="Search for books or authors"
        :dataField="[
          {
            'field': 'authors',
            'weight': 3
          },
          {
            'field': 'authors.autosuggest',
            'weight': 1
          },
          {
            'field': 'original_title',
            'weight': 5
          },
          {
            'field': 'original_title.autosuggest',
            'weight': 1
          }
        ]"
      />
      <multi-list
        componentId="Authors"
        dataField="authors.keyword"
        title="Popular Authors"
        :aggregationSize="5"
      />
      <single-range
        componentId="Ratings"
        dataField="average_rating"
        defaultValue="All Books"
        :data="[
          { start: 0, end: 5, label: 'All Books' },
          { start: 4, end: 5, label: '4 stars and up' },
          { start: 3, end: 5, label: '3 stars and up' },
        ]"
        title="Book Ratings"
      />
		</reactive-base>
	</div>
</template>

<script>
import { 
  ReactiveBase, 
  SearchBox, 
  MultiList, 
  SingleRange
} from '@appbaseio/reactivesearch-vue';

export default {
  name: 'App',
  components: {
    ReactiveBase,
    SearchBox,
    MultiList,
    SingleRange
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
