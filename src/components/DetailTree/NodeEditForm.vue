<template>
    <div class="node-edit-form">
        <button class="btn-xsmall m-0 mt-1 mb-1" v-if="!isEdit" @click="isEdit = true">
            <i class="fa fa-plus"></i> {{label}}
        </button>
        <div class="form-group" v-else>
            <label class="form-group-label label-small">{{label}}</label>
            <input type="text" class="form-group-input input-small" v-model="inputText"  v-on:keyup.enter="save" />
            <button class="form-group-btn btn-small" @click="closeForm">
                <i class="fa fa-times"></i>
            </button>
            <button class="form-group-btn btn-primary btn-small" @click="save">
                <i class="fa fa-check"></i>
            </button>
        </div>
    </div>
</template>

<script>
export default {
    name: 'NodeEditForm',
    props: {
        label: {
            type: String
        }
    },
    data() {
        return {
            isEdit: false,
            inputText: ''
        }
    },
    methods: {
        closeForm() {
            this.isEdit = false;
            this.inputText = '';
        },
        save() {
            this.$emit('save', {
                title: this.inputText
            })
            this.closeForm();
        }
    }
}
</script>