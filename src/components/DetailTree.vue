<template>
    
    <ul class="menu">
        
        <node-edit-form v-on:save="onAddNew" label="вариант"></node-edit-form>

        <template v-if="tree.length > 0">
            <template  v-for="item in tree">

                <detail-tree-group v-if="item.childs.length === 0" 
                    :key="item.id" 
                    :nodeId="item.id" 
                    :title="item.title"
                    :weight="item.weight"
                    :categories="categories"
                    v-on:add-child="onAddChild"
                    v-on:set-rating="onSetRating"
                ></detail-tree-group>

                <li v-else class="menu-item" :key="item.id">
                    <div class="menu-addon">
                        <span class="icon">
                            <i class="fa fa-wrapper fa-folder small" aria-hidden="true"></i>
                        </span>
                    </div>
                    <a href="#">
                        {{item.title}}
                        <span class="tag text-orange-500" v-if="item.weight > 0">
                            {{item.weight.toFixed(2)}}
                        </span>
                    </a>
                    
                    <!-- sub groups -->
                    <detail-tree 
                        :tree="item.childs" 
                        :parent="item"
                        :categories="categories"
                        v-on:add="onAddChild" 
                        v-on:update="onUpdate"
                        v-on:set-rating="onSetRating"
                    ></detail-tree>

                </li>            
            </template>

        </template>
        

    </ul>

</template>

<script>
import DetailTreeGroup from '../components/DetailTree/DetailTreeGroup.vue';
import NodeEditForm from '../components/DetailTree/NodeEditForm.vue';
export default {
    name: 'DetailTree',
    components: {
        DetailTreeGroup, NodeEditForm
    },
    props: {
        tree: {
            type: Array
        },
        parent: {
            type: Object,
            default() {
                return {
                    id: null,
                    label: '' 
                }
            }
        },
        categories: {
            type: Array,
            default() {
                return [];
            }
        }
    },
    data() {
        return {
            editableNodeId: null
        }
    },
    methods: {
        onAddNew(payload) {
            console.log('DT.onAddNew', this.parent.id, payload);
            this.$emit('add', {
                parentId: this.parent.id,
                title: payload.title
            });
        },
        onSave(payload) {
            /*if (this.editableNodeId) {
                this.$emit('update', {
                    nodeId: this.editableNodeId,
                    title: payload.title
                });
            } else {
                this.$emit('add', {
                    parentId: parent.id,
                    title: payload.title
                });
            }*/
        },
        onAddChild(payload) {
            console.log('DT.onAddChild', this.parent.id, payload);
            this.$emit('add', {
                parentId: payload.parentId,
                title: payload.title
            });
        },
        onUpdate(payload) {
            console.log('DT.onUpdate', this.parent, payload);
        },
        onSetRating(payload) {
            console.log('DT.onSetRating', payload);
            this.$emit('set-rating', payload);
        }
    }
}
</script>