<template>
    <div class="">
        <div v-if="isLengthMenu && lengthMenu.length > 0" class="p-5 inline-block">
          <div class="inline-block float-left">
            <label for="inputSearch" class="col-form-label">&nbsp;{{formatLang.labelMenu1}}&nbsp;</label>
            <select v-model="menuSelect"
                    class="inline-block border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-20 p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                    @change="selectMenu">
              <option v-for="(menu, index) in lengthMenu" :key="index" :value="menu"> {{menu}}</option>
            </select>
            <label for="inputSearch" class="col-form-label">&nbsp;{{ formatLang.labelMenu2}}&nbsp;</label>
          </div>
        </div>
        <div v-if="isSearch" class="p-1 inline-block float-right">
            <div class="inline-block float-right">
                <label class="col-form-label">&nbsp;{{formatLang.labelSearch}}&nbsp;</label>
                <input v-model.trim="search" type="search"
                       class="inline-block border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-500 p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                       @input="inputSearch" />
            </div>
        </div>
    </div>
</template>

<script>
import debounce from 'lodash/debounce';
export default {
    props: {
        lengthMenu: Array,
        menu: Number,
        isLengthMenu: Boolean,
        isSearch: Boolean,
        language: Object  
    },
    emits: ['onChangeMenu', 'onSearch'],
    data() {
        return {
            menuSelect: this.menu,
            search: '',            
        }
    },
    methods: {
        selectMenu(){            
            this.$emit('onChangeMenu', this.menuSelect);
        },
        inputSearch: debounce(function() {            
            this.$emit('onSearch', this.search);
        }, 500),        
    },    
    computed: {
        formatLang(){
            const labelMenu = this.language.lengthMenu.split('_MENU_');
            const labelSearch = this.language.search;            
            return {
                labelMenu1: labelMenu.length > 0 ? labelMenu[0] : null,
                labelMenu2:labelMenu.length > 1 ? labelMenu[1] : null,
                labelSearch
            };
        }
    }
}
</script>