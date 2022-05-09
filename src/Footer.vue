<template>
  <div class="bg-white px-4 py-3 flex items-center justify-between border-t border-gray-200 sm:px-6">
    <p class="text-sm text-gray-700">
      {{ formatLang.labelInfo1 }} <span class="font-medium"> {{ metaData.from }} </span>
      {{ formatLang.labelInfo2 }} <span class="font-medium"> {{ metaData.to }} </span>
      {{ formatLang.labelInfo3 }} <span class="font-medium"> {{ metaData.total }} </span> {{ formatLang.labelInfo4 }}</p>
    <nav>
      <nav class="relative z-0 inline-flex rounded-md shadow-sm -space-x-px">
        <template v-for="(link, index) in links" :key="index">
          <span v-if="!link.url"
                v-html="link.label"
                class="relative inline-flex items-center px-4 py-2 border border-gray-300 bg-white text-sm font-medium text-gray-700">
          </span>
          <a v-else
             @click="selectPage(link.url)"
             href="#"
             v-html="link.label"
             :class="(link.active) ? 'z-10 bg-indigo-50 border-indigo-500 text-indigo-600 hidden md:inline-flex relative items-center px-4 py-2 border text-sm font-medium' : 'bg-white border-gray-300 text-gray-500 hover:bg-gray-50 hidden md:inline-flex relative items-center px-4 py-2 border text-sm font-medium'">
          </a>
        </template>
      </nav>
    </nav>
  </div>
</template>

<script>
export default {
  props: {
    metaData: Object,
    links: Array,
    language: Object
  },
  methods: {
    selectPage(url) {

      this.$emit('onChangePage', {
        url,
        isPrevious: this.links[0] ? true : false,
        isNext: this.links[this.links.length - 1] ? true : false,
        isPaginate: (!this.isPrevious && !this.isNext) ? true : false,
      });
    },

  },
  computed: {
    formatLang() {
      const labelSplit = this.language.info.split('_FROM_').join(',').split('_TO_').join(',').split('_TOTAL_').join(',').split(',');

      return {
        labelInfo1: labelSplit.length > 0 ? labelSplit[0] : null,
        labelInfo2: labelSplit.length > 1 ? labelSplit[1] : null,
        labelInfo3: labelSplit.length > 2 ? labelSplit[2] : null,
        labelInfo4: labelSplit.length > 3 ? labelSplit[3] : null,
      };
    }
  }
}
</script>