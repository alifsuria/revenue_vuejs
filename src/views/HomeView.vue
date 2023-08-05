<template>
  <div class="d-flex justify-content-between align-items-center p-3">
    <h4><b>Browser Revenue Group</b></h4>
    <button type="button" id="create-new-revenue-group" class="btn" data-bs-toggle="modal" data-bs-target="#exampleModal">
      <span><font-awesome-icon :icon="['fas', 'plus']" /></span><span class="ms-2">Create Revenue Group</span>
    </button>
  </div>
  <div class="container">
    <div v-for="(revenue_group_data,data_index) in data" :key="data_index" class="card revenue-group-item mb-3">
      <div style="background-color: #EBEDFD;">
        <div class="p-3 d-flex justify-content-between align-items-center">
          <div class="card-title mb-0" data-bs-toggle="collapse" :href="`#${revenue_group_data.id}`" aria-expanded="false"
            aria-controls="collapseExample">
            <strong>{{ revenue_group_data.group_name }} <span v-if="revenue_group_data.special_group" class="badge bg-primary">Special Group</span></strong>
          </div>
          <div>
            <button type="button" @click="delete_data(revenue_group_data.id)"
              class="btn btn-sm btn-outline-secondary rounded-circle"><font-awesome-icon
                :icon="['fas', 'trash']" /></button>
          </div>
        </div>
        <div class="px-3 pb-3" style="font-size: 0.8rem;width: 60%">
          {{ revenue_group_data.group_desc }}
        </div>
      </div>

      <div class="collapse p-3" :id="revenue_group_data.id">
        <div class="">
          <div class="">
            <table class="table table-striped table-sm">
              <thead>
                <tr>
                  <th scope="col"><strong>Rule</strong></th>
                  <th scope="col"><strong>Field</strong></th>
                  <th scope="col"><strong>Operator</strong></th>
                  <th scope="col" v-for="colIndex1 in revenue_group_data.max_param" :key="`param_${colIndex1}`">
                    <strong>Parameter {{ colIndex1 }}</strong>
                  </th>
                  <th scope="col"><strong>Revenue</strong></th>
                  <th scope="col"><strong>Action</strong></th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(rule, rowIndex2) in revenue_group_data.rules" :key="rowIndex2">
                  <td>Rule {{ rowIndex2 + 1 }}</td>
                  <td>{{ rule.field == '1' ? 'Field 1' : rule.field == '2' ? 'Field 2':rule.field == '3'?'Field 3':'Field Not Selected' }}</td>
                  <td>{{ rule.operator == '1'?'is not':rule.operator == '2'?'is':rule.operator == '3'?'starts':rule.operator == '4'?'with':'Operator Not Selected' }}</td>
                  <template v-for="parameter in revenue_group_data.rules[rowIndex2].parameter ">
                    <td>{{ parameter.value }}</td>
                  </template>
                  <template
                    v-for="i in revenue_group_data.max_param - revenue_group_data.rules[rowIndex2].parameter.length">
                    <td>&nbsp;</td>
                  </template>
                  <td>
                    {{ rule.revenue }}%
                  </td>
                  <td>
                    <button @click="delete_rules2(data_index,rule.id)" title="Delete Rule?" class="btn btn-sm btn-secondary">
                      <font-awesome-icon :icon="['fas', 'trash']" />
                    </button>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- Modal -->
  <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog modal-lg modal-dialog-centered modal-dialog-scrollable">
      <div class="modal-content">
        <div class="modal-header px-3 py-2">
          <h1 class="modal-title fs-5" id="exampleModalLabel">Create Revenue Group</h1>
          <button type="button" class="btn-close" data-bs-dismiss="modal" @click="closeModal" aria-label="Close"></button>
        </div>
        <!-- <form action="" @submit.prevent="submitForm"> -->
        <div class="modal-body">
          <div class="">
            <!-- <p style="font-size: 1.5rem;">Create Revenue Group</p> -->

            <div class="mb-3">
              <label for="group-name-field" class="form-label">Group Name</label>
              <input type="text" class="form-control" v-model="group_name" id="group-name-field" placeholder="Name">
            </div>
            <div class="mb-3">
              <label for="group-description-field" class="form-label">Group
                Description</label>
              <textarea class="form-control" v-model="group_desc" id="group-description-field"
                placeholder="Add Description" rows="3"></textarea>
            </div>
            <div class="form-check">
              <input class="form-check-input" v-model="special_group" type="checkbox" value="" id="flexCheckChecked">
              <label class="form-check-label" for="flexCheckChecked">
                Special Group
              </label>
            </div>
            <div class="my-5">
              <div class="rule-section-header d-flex justify-content-between">
                <p class="mb-0">Rules</p>
                <button class="btn btn-sm" @click="add_new_rule"
                  style="background-color:#EAEEFE;color:#0D6EFD;border-radius: 1.5rem;"><span><svg width="18" height="18"
                      viewBox="0 0 18 18" fill="none" xmlns="http://www.w3.org/2000/svg">
                      <path style="fill: #0D6EFD;"
                        d="M14.25 9.75H9.75V14.25H8.25V9.75H3.75V8.25H8.25V3.75H9.75V8.25H14.25V9.75Z" fill="#1859FF" />
                    </svg>
                  </span> Add</button>
              </div>
              <div class="rule-item-group my-3">

                <div v-for="(rule_item, index) in rules" class="rule-item my-3 p-3" :data_rule_item="index"
                  :key="rule_item.id" style="border: 1px dashed rgba(0, 0, 0, 0.35); border-radius: 10px;">
                  <div class="d-flex justify-content-between mb-3">
                    <span>Rule {{ index + 1 }}</span>
                    <span @click="delete_rules(rule_item, $event)" style="padding: 0px 7px;cursor: pointer;">
                      <font-awesome-icon icon="fa-solid fa-times" />
                    </span>
                  </div>
                  <div class="data-body" style="background-color: whitesmoke;border-radius: 7px;">
                    <div class="d-flex align-items-start rule-data p-3">
                      <div class="d-flex align-items-center">
                        <span class="me-2">If</span>
                        <div class="mx-2">
                          <select class="form-select form-select-sm" @change="data_update(index, $event, 'field')"
                            style="width: 9rem;" aria-label="Small select example">
                            <option selected>Select Field</option>
                            <option value="1">Field 1</option>
                            <option value="2">Field 2</option>
                            <option value="3">Field 3</option>
                          </select>
                        </div>
                        <div class="mx-2">
                          <select class="form-select form-select-sm" @change="data_update(index, $event, 'operator')"
                            style="width: 12rem;" aria-label="Small select example">
                            <option selected>Select Operator</option>
                            <option value="1">is Not</option>
                            <option value="2">is</option>
                            <option value="3">starts</option>
                            <option value="4">with</option>
                          </select>
                        </div>
                      </div>
                      <section class="parameter-input-field mx-2">
                        <div v-for="parameter_item in rule_item.parameter" class="parameter-field">
                          <div><input type="text" class="form-control form-control-sm" placeholder="Enter Parameter"
                              @input="data_update(parameter_item, $event, 'parameter')">
                          </div>
                          <div class="ms-2"><svg @click="delete_parameter(index, parameter_item)" width="18" height="18"
                              viewBox="0 0 18 18" fill="none" xmlns="http://www.w3.org/2000/svg">
                              <path
                                d="M5.25 8.25V9.75H12.75V8.25H5.25ZM9 1.5C4.86 1.5 1.5 4.86 1.5 9C1.5 13.14 4.86 16.5 9 16.5C13.14 16.5 16.5 13.14 16.5 9C16.5 4.86 13.14 1.5 9 1.5ZM9 15C5.6925 15 3 12.3075 3 9C3 5.6925 5.6925 3 9 3C12.3075 3 15 5.6925 15 9C15 12.3075 12.3075 15 9 15Z"
                                fill="#323232" />
                            </svg>
                          </div>
                        </div>
                        <div class="">
                          <button class="btn btn-sm w-100 add-parameter-btn"  @click="add_new_parameter($event)"><span>
                              <svg width="18" height="18" viewBox="0 0 18 18" fill="none"
                                xmlns="http://www.w3.org/2000/svg">
                                <path
                                  d="M9.75 5.25H8.25V8.25H5.25V9.75H8.25V12.75H9.75V9.75H12.75V8.25H9.75V5.25ZM9 1.5C4.86 1.5 1.5 4.86 1.5 9C1.5 13.14 4.86 16.5 9 16.5C13.14 16.5 16.5 13.14 16.5 9C16.5 4.86 13.14 1.5 9 1.5ZM9 15C5.6925 15 3 12.3075 3 9C3 5.6925 5.6925 3 9 3C12.3075 3 15 5.6925 15 9C15 12.3075 12.3075 15 9 15Z"
                                  fill="blue" />
                              </svg>
                            </span><span class="ms-2">Add Parameter</span></button>
                        </div>
                      </section>
                    </div>
                  </div>
                  <div class="d-flex align-items-center mt-2"><span>then revenue is</span>
                    <div class="ms-2" style="width: 10rem;">
                      <div class="input-group input-group-sm">
                        <input type="text" @keypress="validateKeyPress" @input="revenue_input(index, $event)"
                          class="form-control" placeholder="Enter Amount">
                        <span class="input-group-text" id="basic-addon2">%</span>
                      </div>

                    </div>
                  </div>
                </div>
              </div>


            </div>
          </div>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" id="close-btn" @click="closeModal"
            data-bs-dismiss="modal">Close</button>
          <button type="button" class="btn btn-primary" @click.prevent="submitForm">Save changes</button>
          <!-- <button type="submit" class="btn btn-primary">Btn Dummy</button> -->
        </div>
        <!-- </form> -->
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted, reactive, ref } from 'vue';
import { v4 as uuidv4 } from 'uuid';
const group_name = ref('');
const group_desc = ref('');
const special_group = ref(false);
let data = reactive([])
let rules = ref([]);

function add_new_rule() {
  rules.value.push({
    id: uuidv4(),
    field: '',
    operator: '',
    parameter: [],
    revenue: '',
    param_count: 0,
  });

}

function delete_rules(rule_id, $event) {
  let filter_item = rules.value.filter((item) => item.id != rule_id.id)
  rules.value.splice(0, rules.value.length, ...filter_item);
}
function delete_rules2(data_pos,rule_id){
  console.log(rule_id)
  console.log(data_pos)
  console.log()
  const indexToRemove = data[data_pos].rules.findIndex(item => item.id === rule_id);
  console.log(indexToRemove)
  if (indexToRemove !== -1) {
    data[data_pos].rules.splice(indexToRemove, 1);
  }
}
function data_update(id, event, type) {
  let get_value = event.target.value
  if (type == 'field') {
    rules.value[id].field = get_value
  } else if (type == 'operator') {
    rules.value[id].operator = get_value
  } else {
    id.value = get_value;
  }
}
function add_new_parameter(event) {
  let get_paramater_button_elem = event.target;
  let get_rule_item_id = get_paramater_button_elem.parentElement.closest('.rule-item').getAttribute('data_rule_item');
  rules.value[get_rule_item_id].parameter.push({ id: uuidv4(), value: '' })
  rules.value[get_rule_item_id].param_count++;
}

function delete_parameter(pos, id) {
  let filter = rules.value[pos].parameter.filter((item) => item.id != id.id)
  rules.value[pos].parameter = filter;
  rules.value[pos].param_count -= 1;
}

function revenue_input(id, event) {
  let get_value = event.target.value.replace(/[^0-9.]/g, '')
  rules.value[id].revenue = get_value;
}

function validateKeyPress(event) {
  // Allow only digits, decimal point, and certain control keys
  const charCode = (event.which) ? event.which : event.keyCode;
  if (
    charCode !== 46 && // Decimal point
    charCode !== 8 && // Backspace
    charCode !== 0 && // Arrow keys
    charCode !== 37 &&
    charCode !== 39 &&
    (charCode < 48 || charCode > 57) // Digits
  ) {
    event.preventDefault();
  }
}

const closeModal = () => {
  // reset input
  group_name.value = '';
  group_desc.value = '';
  rules.value.length = 0;
};

const delete_data = (data_id) => {
  const indexToRemove = data.findIndex(item => item.id === data_id);
  if (indexToRemove !== -1) {
    data.splice(indexToRemove, 1);
  }
};
const submitForm = () => {
  const maxParameterLength = rules.value.reduce((max, item) => {
    const parameterLength = item.parameter.length;
    return Math.max(max, parameterLength);
  }, 0);

  // Clone the rules array using JSON methods
  const clonedRules = JSON.parse(JSON.stringify(rules.value));

  data.push({
    id: uuidv4(),
    group_name: group_name.value,
    group_desc: group_desc.value,
    special_group: special_group.value,
    rules: clonedRules,
    max_param: maxParameterLength,
  });

  // Clear form inputs and rules array
  group_name.value = '';
  group_desc.value = '';
  rules.value = [];

  document.querySelector("#close-btn").click();
};
</script>


<style lang="scss" scoped>
.parameter-input-field>.parameter-field:not(:first-of-type),
.parameter-input-field>.parameter-field:not(:last-of-type) {
  margin: 0.5rem 0px;
}

.parameter-input-field>.parameter-field:first-of-type {
  margin: 0px 0px 0.5rem 0px;
}

// .parameter-input-field>.parameter-field:last-of-type {
//   margin: 0.5rem 0px 0px 0px;
// }

.parameter-field {
  display: flex;
}

// .create-new-section{
//   width: 25rem;
// }

.card-title {
  position: relative;
  width: 80%;
  cursor: pointer;
}

.card-title:after {
  content: '[Click title to expand]';
  position: absolute;
  right: -10rem;
  font-size: 0.9rem;
  color: grey
}

#create-new-revenue-group {
  background-color: #EBEDFD;
  color: #3859FB;
  border: 1px solid #3859FB;
}

#create-new-revenue-group:hover {
  color: #EBEDFD;
  background-color:#3859FB;
}

.add-parameter-btn{
  background-color: #EBEDFD;
  color: #3859FB;
  border: 1px solid #3859FB;
}
.add-parameter-btn:hover{
  color: #EBEDFD;
  background-color:#3859FB;
}

.add-parameter-btn:hover path{
  fill:#EBEDFD
}
</style>




