<template>
    <li class="menu-item">

        <a href="javascript:">
            <div class="row">
                <div class="col-1">
                    <span class="icon">
                        <i class="fa fa-wrapper fa-star small text-primary" aria-hidden="true"></i>
                    </span>
                </div>
                <div class="col-3">
                    {{title}}
                    <span class="tag text-orange-500" v-if="weight > 0">
                        Вес: {{weight.toFixed(2)}}
                    </span>
                </div>
                <div class="col">
                    <div class="rate-stars" v-for="(category,i) in categories" :key="i">
                        <span class="category-name">{{category.name}}</span>
                        <span class="tag text-orange-500">
                            <rating v-on:click="onRatingClick" :value="categoryRating" :meta="category"></rating>
                        </span>
                    </div>
                </div>
                <div class="col-1 node-input-btn">
                    <a href="javascript:" @click="showControls = !showControls" class="p-0">
                        <i class="fas fa-sitemap" :class="{'text-gray-300': showControls}"></i>
                    </a>
                </div>
            </div>
        </a>

        <div class="row p-0" v-if="showControls">
            <div class="pl-0 col-6">
                <node-edit-form label="Детализировать" v-on:save="onSave"></node-edit-form>
            </div>
        </div>

    </li>
</template>

<script>
import NodeEditForm from './NodeEditForm.vue';
import Rating from './Rating.vue';
export default {
    name: 'DetailTreeGroup',
    components: {
        NodeEditForm, Rating
    },
    props: {
        nodeId: {
            type: String|Number,
        },
        title: {
            type: String
        },
        categoryRating: {
            type: Number,
            default: 0
        },
        categories: {
            type: Array,
            default() {
                return [];
            }
        },
        weight: {
            type: Number,
            default: 0
        }
    },
    data() {
        return {
            showControls: false
        }
    },
    methods: {
        onClickNode() {
            this.showControls = true;
        },
        onSave(payload) {
            console.log('DTG.add-child', this.nodeId);
            this.$emit('add-child', {
                parentId: this.nodeId,
                title: payload.title
            })
        },
        onRatingClick(payload) {
            console.log('onRatingClick', payload);
            this.$emit('set-rating', {
                nodeId: this.nodeId,
                category: payload.meta,
                value: payload.value
            });
        }
    }
}
</script>

