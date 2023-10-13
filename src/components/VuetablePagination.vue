<template>
  <div v-show="tablePagination && lastPage > firstPage" :class="insideCss.wrapperClass">
    <a @click="loadPage(firstPage)"
      :class="['btn-nav', insideCss.linkClass, isOnFirstPage ? insideCss.disabledClass : '']">
        <i v-if="insideCss.icons.first != ''" :class="[insideCss.icons.first]"></i>
        <span v-else>&laquo;</span>
    </a>
    <a @click="loadPage('prev')"
      :class="['btn-nav', insideCss.linkClass, isOnFirstPage ? insideCss.disabledClass : '']">
        <i v-if="insideCss.icons.next != ''" :class="[insideCss.icons.prev]"></i>
        <span v-else>&nbsp;&lsaquo;</span>
    </a>
    <template v-if="notEnoughPages">
      <template v-for="(n, i) in totalPage">
        <a @click="loadPage(i+firstPage)" :key="i"
          :class="[insideCss.pageClass, isCurrentPage(i+firstPage) ? insideCss.activeClass : '']"
          v-html="n">
        </a>
      </template>
    </template>
    <template v-else>
      <template v-for="(n, i) in windowSize">
        <a @click="loadPage(windowStart+i+firstPage-1)" :key="i"
          :class="[insideCss.pageClass, isCurrentPage(windowStart+i+firstPage-1) ? insideCss.activeClass : '']"
          v-html="windowStart+n-1">
        </a>
      </template>
    </template>
    <a @click="loadPage('next')"
      :class="['btn-nav', insideCss.linkClass, isOnLastPage ? insideCss.disabledClass : '']">
      <i v-if="insideCss.icons.next != ''" :class="[insideCss.icons.next]"></i>
      <span v-else>&rsaquo;&nbsp;</span>
    </a>
    <a @click="loadPage(lastPage)"
      :class="['btn-nav', insideCss.linkClass, isOnLastPage ? insideCss.disabledClass : '']">
      <i v-if="insideCss.icons.last != ''" :class="[insideCss.icons.last]"></i>
      <span v-else>&raquo;</span>
    </a>
  </div>
</template>

<script>
import PaginationMixin from './VuetablePaginationMixin.vue'

export default {
  mixins: [PaginationMixin],
}
</script>
<style>
  .vuetable-pagination {
    background: #f9fafb !important;
  }
</style>
