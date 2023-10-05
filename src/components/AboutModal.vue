<!-- eslint-disable vue/multi-word-component-names -->
<template>
    <!-- Modal -->
    <div class="modal fade" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true"
     ref="modal">
        <div class="modal-dialog">
            <img src="../assets/jeju.png" id="jejuImg01" class="card-img-top" alt="濟洲島">
        </div>
    </div>
    <!-- <div class="modal fade" tabindex="-1" aria-labelledby="exampleModalLabel01" aria-hidden="true"
     ref="modal">
        <div class="modal-dialog">
            <img src="../assets/萬聖節(櫻花).png" class="card-img-top" alt="萬聖節(櫻花)">
        </div>
    </div> -->
</template>

<script>
import Modal from 'bootstrap/js/dist/modal';

export default {
    data() {
        return {
            modal: {}
        }
    },
    methods: {
      showModal() {
        this.modal.show();
      },
      hideModal() {
        this.modal.hide();
      },
    },
    mounted() {
        this.modal  = new Modal(this.$refs.modal);
        
        
    }
};
  </script>