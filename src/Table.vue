<template>
    <table :class="tableClass">
        <TableHeader
            :tHeadClass="tHeadClass"
            :columns="columns"
            :isSort="isSort"
            :sortDt="sortDt"
            @changeSort="setSort"
        />
        <TableBody 
            :columns="columns" 
            :data="data"
            :language="language"
            :isLoading="isLoading"
        />         
    </table>

</template>
<script>
import TableHeader from './TableHeader.vue';
import TableBody from './TableBody.vue';
export default {
    props: {
      tableClass: {
        type: String,
        default: () => {
          return "table table-hover table-responsive align-middle"
        }
      },
      tHeadClass: {
        type: String,
      },
        columns: Array,
        data: Array,
        isSort: Boolean,
        sortDt: Object,
        language: Object,
        isLoading: Boolean
    },
    emits: ['onChangeSort'],
    components: {
        TableHeader,
        TableBody
    },
    methods: {
        setSort(sort){            
            this.$emit('onChangeSort', sort);
        }
    }
}
</script>