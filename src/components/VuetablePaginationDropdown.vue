<template>
  <div :class="[insideCss.wrapperClass]">
    <a @click="loadPage('prev')"
       :class="[insideCss.linkClass, {[insideCss.disabledClass] : isOnFirstPage}]">
      <i :class="insideCss.icons.prev"></i>
    </a>
    <select :class="['vuetable-pagination-dropdown', insideCss.dropdownClass]" @change="loadPage($event.target.selectedIndex+firstPage)">
      <option v-for="(n, i) in totalPage" :key="n" :class="[insideCss.pageClass]" :value="i+firstPage" :selected="isCurrentPage(i+firstPage)">
        {{pageText}} {{n}}
      </option>
    </select>
    <a @click="loadPage('next')"
       :class="[insideCss.linkClass, {[insideCss.disabledClass] : isOnLastPage}]">
      <i :class="insideCss.icons.next"></i>
    </a>
  </div>
</template>

<script>
import PaginationMixin from './VuetablePaginationMixin.vue'

export default {
  mixins: [PaginationMixin],
  props: {
    pageText: {
      type: String,
      default () {
        return 'Page'
      }
    }
  },
  methods: {
    registerEvents () {
      this.$on('vuetable:pagination-data', (tablePagination) => {
        this.setPaginationData(tablePagination)
      })
    }
  },
  created () {
    this.registerEvents()
  }
}
</script>
