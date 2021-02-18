<template>
  <section class="section">
    <div class="hero">
      <div class="hero-body">
        <div class="content">
        
          <h1>Метод детализации с весами</h1>

          <blockquote>
            При высокой сложности проблемной ситуации принять решение поможет разбиение вариантов 
            на множество более простых решений, т.е. можно выполнить детализацию альтернатив. Это 
            позволит определить всё множество вариантов и найти более простые решения, которые можно 
            будет легко сравнить и выбрать наиболее подходящий.  
          </blockquote>

          
          <div class="row">
            <div class="col">
              <div class="form-section">
                  <label>Одним из важных моментов в принятии решения является корректное 
                    <a href="javascript:" class="tooltip" 
                    data-tooltip="Подробнее о формулировках">формулирование проблемы</a>: </label>
                  <input type="text" v-model="goalInput" placeholder="Давайте попробуем записать формулировку здесь">
                  <span class="info">
                    <div>Плохой пример: "хочу отдохнуть"</div>
                    <div>Хороший пример: "где провести отпуск в марте?"</div>
                  </span>
              </div>    
            </div>
          </div>

          <div class="row">
            <div class="col">
              <p>Далее выработаем <strong>критерии</strong>, по которым будем оценивать будущие варианты. Каждый критерий будет иметь свой вес, 
                и в процессе анализа мы будет давать по ним <strong>оценку</strong>. Высокая оценка плюс большой вес 
                дадут оцениваемому варианту большее преимущество перед другими.</p>
            </div>
          </div>

          <div class="row">
            <div class="col">
              <p>Поскольку дальше мы будем давать вариантам оценки, помните, что чем выше оценка по каждому из критериев, 
                тем лучше вариант, поэтому формулируйте критерии таким образом, чтобы высокие оценки давали преимущество.</p>
            </div>
          </div>

          
          <div class="row">
            <div class="col">
              <p>Плохие примеры:</p>
              <ul>
                <li><a href="javascript:" class="tooltip" data-tooltip="Противоречие: высокая оценка = низкая стоимость">стоимость</a></li>
                <li><a href="javascript:" class="tooltip" data-tooltip="А если не будет варианта с отелем?">количество звёзд у отеля</a></li>
                <li><a href="javascript:" class="tooltip" data-tooltip="Может лучше сделать это альтернативой?">с друзьями</a></li>
              </ul>
            </div>
            <div class="col">
              <p>Хорошие примеры:</p>
              <ul>
                <li><a href="javascript:" class="tooltip" data-tooltip="Высокая оценка = попадание в бюджет">бюджет</a></li>
                <li><a href="javascript:" class="tooltip" data-tooltip="Высокая оценка = высокое качество">качество отдыха</a></li>
                <li><a href="javascript:" class="tooltip" data-tooltip="Высокая оценка = хорошая доступность">транспортная доступность</a></li>
              </ul>
            </div>
          </div>

          <!-- Критерии -->
          <div class="card">
            <div class="content">
              <div class="form-section">
                <div class="form-group">
                    <input type="text" class="form-group-input" v-model="criteriaInput.name" 
                      placeholder="Новый критерий" v-on:keyup.enter="onClickAddCriteria"/>
                    <select class="select" placeholder="Вес" v-model="criteriaInput.weight">
                      <option value="5">Высокая значимость</option>
                      <option value="4">Не очень высокая значимость</option>
                      <option value="3">Средняя значимость</option>
                      <option value="2">Низкая значимость</option>
                      <option value="1">Почти ничего не значит</option>
                    </select>
                    <button class="form-group-btn" v-on:click="onClickAddCriteria" :disabled="criteriaInput.name === ''">
                      <i class="fa fa-check"></i>
                    </button>
                </div>
              </div>
              <label><strong>Список критериев</strong></label>
              <ul class="menu">
                <template v-if="criterias.length > 0">
                  <li class="menu-item" v-for="(item,i) in criterias" :key="i">
                    <a href="javascript:" @click="removeCriteria(i)">
                      <div class="row">
                      <div class="col">{{item.name}}</div>
                      <div class="col">Значимость <div class="tag tag--info">{{item.weight}} из 5</div></div>
                      </div>
                    </a>
                  </li>
                </template>
                <div class="toast toast--warning" v-else>
                  Введите хотя бы один критерий
                </div>
              </ul>
            </div>
          </div>
          

          <div class="row">
            <div class="col">
              <p>Далее идея заключается в поиске альтернативных способов достижения цели, то есть тех самых вариантов решения вопроса. 
                Сначала заводим максимально общие альтернативы. Например, первичные варианты для отдыха:</p>
              <ul>
                <li>Дача</li>
                <li>Путешествие</li>
                <li>Дома</li>
                <li>С родителями</li>
              </ul>
            </div>
          </div>

          <div class="frame">
            <div class="frame-header p-1 pl-3">
              <div class="frame__title">
                Детализация цели
              </div>
              <div class="frame__subtitle">
                {{goalInput}}
              </div>
            </div>
            <div class="frame__body">
              <detail-tree 
                v-if="criterias.length > 0"
                parent-label="Детализация"
                :tree="getSortedTree" 
                :categories="criterias"
                v-on:add="onAddChild" 
                v-on:update="onUpdate"
                v-on:set-rating="onUpdateRating"
                ></detail-tree>          
              <div class="toast toast--warning" v-else>
                Для детализации нужны критерии 
              </div>
            </div>
            
          </div>

          <div class="card mt-5 pt-3">
            <div class="content">
              Ссылки-источники:
              <ul>
                <li><a href="https://manprogress.com/ru/methods/making-decisions.html">https://manprogress.com/ru/methods/making-decisions.html</a></li>
                <li><a href="https://goal-life.com/ru/how-to-formulate-goals">https://goal-life.com/ru/how-to-formulate-goals</a></li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import DetailTree from '../components/DetailTree.vue';
import NodeEditForm from '../components/DetailTree/NodeEditForm.vue';
export default {
  name: 'Detail',
  components: {
    DetailTree,
    NodeEditForm
  },
  data() {
    return {
      goalInput: '',
      criteriaInput: {
        name: '',
        weight: '3'
      },
      criterias: [],
      tree: []
    }
  },
  methods: {

    onClickAddCriteria() {
      if (this.criteriaInput.name === '') {
        return;
      }
      this.criterias.push({name: this.criteriaInput.name, weight: this.criteriaInput.weight});
      this.criteriaInput.name = '';
      this.criteriaInput.weight = '3';
    },

    removeCriteria(i) {
      this.criterias.splice(i, 1);
    },

    /**
     * добавление дочернего узла
     */
    onAddChild(payload) {
      this.tree.push({
        id: Math.random(),
        title: payload.title,
        parentId: payload.parentId ? payload.parentId : null,
        categoryRatings: {},
        weight: 0,
        childs: []
      });
    },

    /**
     * обновление узла
     */
    onUpdate(payload) {
      this.tree = this.tree.map(item => {
        if (item.id === payload.item.id) {
          item = payload.item;
          item.isVisibleEditForm = payload.isEditable;
        }
        return item;
      });
    },

    getCategoryByName(name) {
      const categories = this.criterias.filter(item => item.name === name);
      return categories.length > 0 ? categories[0] : null;
    },

    /**
     * обновление рейтинга
     */
    onUpdateRating(payload) {

      let nodeIndex = null;
      for (let i in this.tree) {
        if (this.tree[i].id === payload.nodeId) {
          nodeIndex = i;
          break;
        }
      }
      if (nodeIndex === null) {
        console.error('null node not found');
        return;
      }
      this.tree[nodeIndex].categoryRatings[payload.category.name] = payload.value;
      /*
      tree[1] => {
        categoryRatings: {
          category1: 4,
          category2: 2
        }
      }
      */
      let categories = [];
      for (let categoryName in this.tree[nodeIndex].categoryRatings) {
        const category = this.getCategoryByName(categoryName);
        /*
        category => {
          name: category1,
          weight: 5
        }
        */
        let weight = 0;
        if (category) {
          weight = parseInt(category.weight);
        }
        //formula: sum(sqrt(rate * weight)) / count
        categories.push(Math.sqrt(weight * this.tree[nodeIndex].categoryRatings[categoryName]));
      }
      const nodeWeight = categories.reduce((acc, current) => acc + current) / categories.length;
      this.tree[nodeIndex].weight = nodeWeight;

      const findAndCalculateWeight = (nodeId) => {
        let weights = 0;
        let findIndex = null;

        for (let i in this.tree) {
          if (this.tree[i] === nodeId) {
            findIndex = i;
            break;
          }
        }
        const childs = this.tree.filter(item => item.parentId === nodeId);
        if (childs.length === 0) {
          this.tree[findIndex].weight = 0;
          return;
        }
        for (let i in childs) {
          weights += parseFloat(childs[i].weight);
        }
        this.tree[findIndex].weight = weights / childs.length;
        if (this.tree[findIndex].parentId !== null) {
          findAndCalculateWeight(this.tree[findIndex].parentId);
        }
      }

      findAndCalculateWeight(this.tree[nodeIndex].parentId);

    }
  },
  computed: {
    getSortedTree() {
      const getChilds = (parentId) => {
        let list = this.tree.filter((item) => {
          return item.parentId === parentId;
        });
        for (let i in list) {
          list[i].childs = getChilds(list[i].id);
        }
        return list;
      }
      return getChilds(null);
    }
  }
}
</script>


<style lang="scss">
.node-input-btn {
  text-align: center;
}
.rate-stars {
  span {
    padding: 0 5px;
  }
}
</style>