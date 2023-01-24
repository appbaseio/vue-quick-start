<template>
  <reactive-base
    url="https://appbase-demo-ansible-abxiydt-arc.searchbase.io"
    app="good-books-ds"
    credentials="04717bb076f7:be54685e-db84-4243-975b-5b32ee241d31"
  >
    <div id="app">
      <div v-bind:style="{ display: 'flex', 'flex-direction': 'row' }">
        <div
          v-bind:style="{
            width: '30%',
            'flex-direction': 'column',
            'text-align': 'left',
            padding: '10px',
            'font-size': '14px',
          }"
        >
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
        </div>
        <div
          v-bind:style="{
            display: 'flex',
            'flex-direction': 'column',
            padding: '10px',
            width: '66%',
          }"
        >
          <search-box
            componentId="SearchBox"
            placeholder="Search for books or authors"
            :dataField="[
              {
                field: 'authors',
                weight: 3,
              },
              {
                field: 'authors.autosuggest',
                weight: 1,
              },
              {
                field: 'original_title',
                weight: 5,
              },
              {
                field: 'original_title.autosuggest',
                weight: 1,
              },
            ]"
          />
          <reactive-list
            componentId="SearchResult"
            dataField="original_title.keyword"
            :class="{ full: showBooks }"
            :pagination="true"
            :from="0"
            :size="5"
            :react="{ and: ['Ratings', 'Authors', 'SearchBox'] }"
          >
            <template #renderItem="{ item }">
              <div
                key="item._id"
                v-bind:style="{
                  display: 'flex',
                  background: 'white',
                  margin: '10px 0',
                  'box-shadow':
                    '0 1px 3px rgba(0, 0, 0, 0.12), 0 1px 2px rgba(0, 0, 0, 0.24)',
                }"
              >
                <img
                  :src="item.image"
                  alt="Book Cover"
                  v-bind:style="{
                    height: '150px',
                    width: '110px',
                    'background-size': 'cover',
                  }"
                />
                <div v-bind:style="{ 'text-align': 'left' }">
                  <div
                    v-bind:style="{
                      'font-weight': 'bold',
                      padding: '10px 10px 5px 10px',
                    }"
                  >
                    {{ item.original_title }}
                  </div>
                  <div v-bind:style="{ padding: '5px 10px' }">
                    by {{ item.authors }}
                  </div>
                  <div v-bind:style="{ padding: '5px 10px' }">
                    ({{ item.average_rating }} avg)
                  </div>
                  <div v-bind:style="{ padding: '5px 10px' }">
                    Pub {{ item.original_publication_year }}
                  </div>
                </div>
              </div>
            </template>
          </reactive-list>
        </div>
      </div>
    </div>
  </reactive-base>
</template>

<script>
import {
  ReactiveBase,
  SearchBox,
  MultiList,
  SingleRange,
  ReactiveList,
} from "@appbaseio/reactivesearch-vue";

export default {
  name: "App",
  components: {
    ReactiveBase,
    SearchBox,
    MultiList,
    SingleRange,
    ReactiveList,
  },
};
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
