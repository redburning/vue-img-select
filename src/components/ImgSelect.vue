<template>
    <div class="img-select">
        <div class="input-wrapper" @click="showSelectOptions = true;">
            <div class="input-prefix-icon-container">
                <img class="input-prefix-icon" v-if="selectedOption.icon" :src="selectedOption.icon" :alt="selectedOption.label" />
            </div>
            <input v-model="inputContent" @focus="showAllOptions = true" @input="showAllOptions = false" class="input-text" />
            <div class="input-postfix-icon" @click="showAllOptions = true">
                <svg v-show="!showSelectOptions" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="16" height="16" class="css-1d3xu67-Icon">
                    <path d="M17,9.17a1,1,0,0,0-1.41,0L12,12.71,8.46,9.17a1,1,0,0,0-1.41,0,1,1,0,0,0,0,1.42l4.24,4.24a1,1,0,0,0,1.42,0L17,10.59A1,1,0,0,0,17,9.17Z"></path>
                </svg>
                <svg v-show="showSelectOptions" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="16" height="16" class="css-1d3xu67-Icon">
                    <path d="M21.71,20.29,18,16.61A9,9,0,1,0,16.61,18l3.68,3.68a1,1,0,0,0,1.42,0A1,1,0,0,0,21.71,20.29ZM11,18a7,7,0,1,1,7-7A7,7,0,0,1,11,18Z"></path>
                </svg>
            </div>
        </div>
        <div class="select-option-list" v-show="showSelectOptions">
            <div v-for="option in (showAllOptions ? options : filteredOptions)" :key="option.key"
                @click="selectOption(option)" class="select-option"
                :class="{ 'selected-option': option.key === selectedOption.key }">
                <div class="select-option-icon-container">
                    <img v-if="option.icon" :src="option.icon" :alt="option.label" class="select-option-icon" />
                </div>
                <div class="flex-between fill-content">
                    <div class="select-option-name">{{ option.label }}</div>
                    <div class="select-option-label">{{ option.type }}</div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        options: {
            type: Array,
            required: true
        }
    },
    data () {
        return {
            // 是否显示下拉选项
            showSelectOptions: false,
            // 显示全部的选项，还是过滤后的选项
            showAllOptions: false,
            // 选择的选项
            selectedOption: this.options[0],
            // 输入的搜索内容
            inputContent: this.options[0].label
        }
    },
    computed: {
        filteredOptions () {
            return this.options.filter(item => {
                return item.label.toLowerCase().includes(this.inputContent.toLowerCase())
            })
        }
    },
    methods: {
        selectOption (option) {
            this.selectedOption = option
            this.showSelectOptions = false
            this.inputContent = option.label
            // 将选择的选项通知给父组件
            this.$emit('input', option)
        },
        // 点击空白处选项列表消失
        handleClickOutside (event) {
            const inputWrapper = this.$el.querySelector('.input-wrapper')
            const selectOptionList = this.$el.querySelector('.select-option-list')
            if (inputWrapper && !inputWrapper.contains(event.target)) {
                if (selectOptionList && !selectOptionList.contains(event.target)) {
                    this.showSelectOptions = false
                }
            }
        }
    },
    mounted () {
        document.addEventListener('click', this.handleClickOutside)
    },
    beforeDestroy () {
        document.removeEventListener('click', this.handleClickOutside)
    }
}
</script>

<style scoped>
.img-select {
    position: relative;
    width: 400px;
}

.input-wrapper {
    display: flex;
    align-items: center;
    position: relative;
    height: 32px;
}

.input-prefix-icon {
    width: 100%;
    z-index: 1;
}

.input-prefix-icon-container {
    position: absolute;
    padding: 5px 8px;
    height: 100%;
    display: flex;
    justify-content: flex-start;
    box-sizing: border-box;
}

.input-prefix-icon-container:hover {
    cursor: pointer;
}

.input-postfix-icon {
    height: 100%;
    padding-left: 8px;
    padding-right: 8px;
    position: absolute;
    top: 0px;
    right: 0px;
    z-index: 1;
    display: flex;
    align-items: center;
}

.input-postfix-icon:hover {
    cursor: pointer;
}

.input-text {
    padding-left: 65px;
    padding-right: 28px;
    background: rgb(255, 255, 255);
    line-height: 1.57143;
    font-size: 14px;
    color: rgb(36, 41, 46);
    border: 1px solid rgba(36, 41, 46, 0.3);
    flex-grow: 1;
    border-radius: 4px;
    height: 100%;
    width: 100%;
    z-index: 0;
}

.input-text:focus {
    outline: unset;
    box-shadow: rgb(244, 245, 245) 0px 0px 0px 2px, rgb(56, 113, 220) 0px 0px 0px 4px;
}

.select-option-list {
    display: flex;
    flex-direction: column;
    box-shadow: rgba(24, 26, 27, 0.18) 0px 13px 20px 1px;
    max-height: 200px;
    width: 400px;
    overflow-y: auto;
    border: 1px solid rgba(36, 41, 46, 0.12);
    position: absolute;
    top: 38px;
}

.select-option {
    display: flex;
    align-items: center;
    height: 24px;
    padding: 6px;
    cursor: pointer;
    background-color: #ffffff;
    border-bottom: 1px solid rgba(36, 41, 46, 0.12);
}

.select-option:hover {
    background-color: #eceded;
}

.selected-option {
    background-color: #f5f7fa;
}

.select-option-icon-container {
    min-width: 60px;
    max-width: 60px;
    height: 100%;
}

.select-option-icon {
    height: 100%;
    display: flex;
}

.select-option-name {
    white-space: nowrap;
    font-size: 14px;
}

.select-option-label {
    font-size: 12px;
    color: rgba(36, 41, 46, 0.75);
    white-space: nowrap;
}

.flex-between {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 10px;
}

.fill-content {
    width: 100%;
    height: 100%;
}

/* 滚动条整体样式 */
.select-option-list::-webkit-scrollbar {
    width: 6px;
}
/* 滚动条轨道样式 */
.select-option-list::-webkit-scrollbar-track {
    background: #f1f1f1;
    border-radius: 6px;
}
/* 滚动条滑块样式 */
.select-option-list::-webkit-scrollbar-thumb {
    background: #dadcdd;
    border-radius: 6px;
}
/* 滑块 hover 样式 */
.select-option-list::-webkit-scrollbar-thumb:hover {
    background: #999;
}
</style>
