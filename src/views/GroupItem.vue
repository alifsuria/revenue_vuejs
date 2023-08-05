<template>
  <div class="card">
    <div class="card-body">
      <div class="d-flex">
        <div>
          <h5 class="card-title">REVENUE GROUP NAME</h5>
          <p class="card-text">With supporting text below as a natural lead-in to additional content.</p>
        </div>
        <div></div>
      </div>
      <div class="">
        <table class="table">
          <thead>
            <tr>
              <th scope="col">#</th>
              <th scope="col">Group Name</th>
              <th scope="col">Group Description</th>
              <th scope="col">Action</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <th scope="row">1</th>
              <td>Group 1</td>
              <td>Group Description awdawdaw</td>
              <td><button title="View Detail" class="btn btn-sm btn-secondary"><font-awesome-icon
                    :icon="['fas', 'arrow-right-to-bracket']" /></button></td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<style>
@media (min-width: 1024px) {
  /* .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  } */
}
</style>


<div class="rule-item my-3 p-3"
style="border: 1px dashed rgba(0, 0, 0, 0.35); border-radius: 10px;">
<div class="d-flex justify-content-between mb-3">
    <span>Rule 1</span>
    <span>
        <font-awesome-icon icon="fa-solid fa-times" />
    </span>
</div>
<div class="data-body" style="background-color: whitesmoke;border-radius: 7px;">
    <div class="d-flex align-items-start rule-data p-3">
        <div class="d-flex align-items-center">
            <span class="me-2">If</span>
            <div class="mx-2">
                <select class="form-select form-select-sm" style="width: 15rem;"
                    aria-label="Small select example">
                    <option selected>Select Field</option>
                    <option value="1">One</option>
                    <option value="2">Two</option>
                    <option value="3">Three</option>
                </select>
            </div>
            <div class="mx-2">
                <select class="form-select form-select-sm" style="width: 15rem;"
                    aria-label="Small select example">
                    <option selected>Select Operator</option>
                    <option value="1">One</option>
                    <option value="2">Two</option>
                    <option value="3">Three</option>
                </select>
            </div>
        </div>
        <section class="parameter-input-field mx-2">
            <div class="parameter-field">
                <div><input type="text" class="form-control form-control-sm"
                        placeholder="Enter Parameter">
                </div>
                <div class="ms-2"><svg width="18" height="18" viewBox="0 0 18 18"
                        fill="none" xmlns="http://www.w3.org/2000/svg">
                        <path
                            d="M9.75 5.25H8.25V8.25H5.25V9.75H8.25V12.75H9.75V9.75H12.75V8.25H9.75V5.25ZM9 1.5C4.86 1.5 1.5 4.86 1.5 9C1.5 13.14 4.86 16.5 9 16.5C13.14 16.5 16.5 13.14 16.5 9C16.5 4.86 13.14 1.5 9 1.5ZM9 15C5.6925 15 3 12.3075 3 9C3 5.6925 5.6925 3 9 3C12.3075 3 15 5.6925 15 9C15 12.3075 12.3075 15 9 15Z"
                            fill="#323232" />
                    </svg>
                </div>
            </div>
        </section>
    </div>
</div>
<div class="d-flex align-items-center mt-2"><span>then revenue is</span>
    <div class="ms-2" style="width: 10rem;"><input type="text"
            class="form-control form-control-sm" placeholder="% Enter Amount"></div>
</div>
</div>