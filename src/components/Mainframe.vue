<template>
    <div class="d-flex justify-content-between align-items-center p-3">
        <h4><b>Browser Revenue Group</b></h4>
        <button type="button" id="create-new-revenue-group" class="btn btn-primary" data-bs-toggle="modal"
            data-bs-target="#exampleModal">
            <span><font-awesome-icon :icon="['fas', 'plus']" /></span><span class="ms-2">Create Revenue Group</span>
        </button>
    </div>
    <slot />



</template>

<script setup>
import { onMounted, reactive, ref } from 'vue';
import { v4 as uuidv4 } from 'uuid';
import { Modal } from 'bootstrap'
// function showModal() {
// var modalElement = document.getElementById('myModal');
// var modal = new bootstrap.Modal(modalElement);
// modal.show();
const modalEl = ref(null);
// const close_button = ref(null);
const group_name = ref('');
const group_desc = ref('');
const special_group = ref(false);
let data = reactive([]);
let rules = reactive([]);

// }

function add_new_rule() {
    rules.push({
        id: uuidv4(),
        field: '',
        operator: '',
        parameter: [],
        revenue:''
    });
    console.log(rules);

}

function add_new_parameter(event) {
    let get_paramater_button_elem = event.target;
    let get_rule_item_id = get_paramater_button_elem.parentElement.closest('.rule-item').getAttribute('data_rule_item');
    rules[get_rule_item_id].parameter.push({ id: uuidv4(), value: '' })
}

function delete_parameter(pos, id) {
    console.log(id)
    let filter = rules[pos].parameter.filter((item) => item.id != id)
    rules[pos].parameter = filter;
    console.log(rules[pos].parameter)
}

function revenue_input(id,event){
    console.log(id)
    rules[id].revenue = event.target.value;
}

const closeModal = () => {
    // reset input
};
onMounted(() => {

})

const submitForm = () => {
    // alert('saeve datea')

    data.push({ group_name: group_name.value, group_desc: group_desc.value, special_group: special_group, rules: rules })
    console.log(data)

    document.querySelector("#close-btn").click()
}
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
</style>
