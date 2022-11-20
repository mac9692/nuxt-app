<template>
  <div>
    <label for="orderName">상품명 : </label>
    <input type="text" id="orderName" v-model="paymentParam.orderName" />
    <br />
    <label for="customerName">회원명 : </label>
    <input type="text" id="customerName" v-model="paymentParam.customerName" />
    <br />
    <label for="amount">가격 : </label>
    <input type="text" id="amount" v-model="paymentParam.amount" />
    <br />
    <label for="orderId">주문 번호 : </label>
    <input type="text" id="orderId" v-model="paymentParam.orderId" />
    <br />
    <label for="successUrl">성공 시 URL : </label>
    <input type="text" id="successUrl" v-model="paymentParam.successUrl" />
    <br />
    <label for="failUrl">실패 시 URL : </label>
    <input type="text" id="failUrl" v-model="paymentParam.failUrl" />
    <br />
    <button @click="pay">결제버튼</button>
  </div>
</template>

<script>
import {loadTossPayments} from "@tosspayments/payment-sdk";

export default {
  name: "index",

  data() {
    return {
      paymentParam: {
        amount: 15000,
        orderId: '8m7-A3IJElnFMdMWne4EL',
        orderName: '토스 티셔츠 외 2건',
        customerName: '박토스',
        successUrl: 'http://localhost:3000/payment/success',
        failUrl: 'http://localhost:3000/payment/fail',
      },
    }
  },

  methods: {
    pay() {
      const clientKey = 'test_ck_LBa5PzR0ArnBa6l0n7GrvmYnNeDM';
      loadTossPayments(clientKey).then(tossPayments => {
        tossPayments.requestPayment('카드', this.paymentParam);
      });
    },
  },
}
</script>

<style scoped>

</style>
