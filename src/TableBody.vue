<template>
    <tbody v-if="data.length > 0" class="text-left text-gray-700">
        <!-- <template v-if="isLoading">
            <tr>
                {{language.loading}}                
            </tr>
        </template>
        <template v-else-if="data.length === 0">
            <tr>
                {{language.zeroRecords}}                
            </tr>

        </template> -->
        <template  v-for="(row, index1) in data" :key="index1">
            <tr class="bg-white border-b">
            <template v-for="(column, index2) in columns" :key="index2">   
                <template v-if="Object.keys(row).find(key => key === column.key)">
                    <td class="px-6 py-3 p-4" v-if="!column.isAction && (column.isHide == false || column.isHide == undefined)">
                        {{ row[column.key]}}
                    </td> 
                    <template v-else>      
                        <td  class="px-6 py-3 p-4" v-if="typeof column.component ==='object' && (column.isHide == false || column.isHide == undefined)">
                            <component                                                                    
                                :is="column.component" 
                                :row="row"
                                :column="column"                                
                            ></component>
                        </td>                  
                    </template>                                        
                </template>                
            </template>
            </tr>
        </template>
    </tbody>    
    <tbody v-else-if="!isLoading" class="text-left text-gray-700">
        <tr>
            {{language.zeroRecords}}                
        </tr>
    </tbody>
</template>
<script>
export default {
    props: {
        columns: {
            required: true,
            type: Array,
        },
        data: Array,
        language: Object,
        isLoading: Boolean
    },
}
</script>