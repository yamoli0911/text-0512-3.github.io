
<template>
  <div class="modal fade" ref="modal" tabindex="-1">
    <div class="modal-dialog modal-dialog-centered modal">
      <div class="modal-content background-transparent">
        <div class="modal-header bg-primary text-center p-3">
          <h4 class="modal-title text-white">新增優惠券</h4>
        </div>
        <div class="modal-body bg-white p-6">
          <div class="row">
            <div class="mb-3 col">
              <label for="title" class="form-label">名稱</label>
              <input id="title" type="text" min="0" class="form-control" placeholder="請輸入名稱"
              v-model.trim="tempModalData.title">
            </div>
            <div class="mb-3 col">
              <label for="code" class="form-label">優惠碼</label>
              <input id="code" type="text" min="0" class="form-control" placeholder="請輸入優惠碼"
              v-model.trim="tempModalData.code">
            </div>
          </div>
          <div class="row">
            <div class="mb-3 col">
              <label for="percent" class="form-label">折扣百分比</label>
              <input id="percent" type="text" min="0" class="form-control" placeholder="請輸入折扣百分比"
              v-model.number="tempModalData.percent">
            </div>
            <div class="mb-3 col">
              <label for="due_date" class="form-label">到期日</label>
              <input id="due_date" type="date" min="0" class="form-control" placeholder="到期日"
              v-model="due_date">
            </div>
          </div>
          <!-- ToggleSwitch -->
          <p class="fw-bold fs-4 mb-2">是否啟用</p>
          <label class="switch">
            <input type="checkbox"
            v-model="tempModalData.is_enabled"
            :true-value="1" :false-value="0">
            <span class="slider"></span>
          </label>
          <!-- ToggleSwitch -->
        </div>
        <div class="modal-footer bg-white w-100">
          <button type="button" class="btn btn-outline-primary" data-bs-dismiss="modal">取消</button>
          <button type="button" class="btn btn-primary text-white" @click="$emit('update-Coupons',tempModalData,isCreateNew)">
              {{ isCreateNew?'確定新增':'確定修改' }}</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import BsModal from 'bootstrap/js/dist/modal';

export default {

  props: ['isCreateNew','temp'],
  data () {
    return {
      due_date: '',
       tempModalData: {},
      modal: ''
    }
  },
   watch: {
    temp: {
      handler () {
        this.tempModalData = JSON.parse(JSON.stringify(this.temp))
      },
      deep: true
    },
    due_date () {
      //  Math.floor = 小於等於所給數字的最大整數。
      this.tempModalData.due_date = Math.floor(new Date(this.due_date) / 1000)
    }
  },
   methods: {
    openModal () {
      this.modal.show()
    },
    hideModal () {
      this.modal.hide()
    }
  },
  mounted () {
    this.modal = new BsModal(this.$refs.modal)
  }
}
</script>
