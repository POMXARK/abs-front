<script setup>
const page = ref(useRoute().query.page)
const total = ref()
const pageCount = ref()
const abs = ref()

const ordersPrice = [{name: 'По возрастанию', value: 'asc'}, {name: 'По убыванию', value: 'desc'}]
const ordersCreated = [{name: 'По возрастанию', value: 'asc'}, {name: 'По убыванию', value: 'desc'}]

const orderPrice = ref(ordersPrice[0].value)
const orderCreated = ref(ordersCreated[0].value)

const router = useRouter()

const load = async () => {

  console.log('orderPrice.value', orderPrice.value)
  console.log('orderCreated.value', orderCreated.value)

  //  fetch the products
  const uri = `http://127.0.0.1/api/v1/abs?page=${page.value}&sort_by_price=${orderPrice.value}&sort_by_created_at=${orderCreated.value}`
  const {data} = (await useFetch(uri))
  console.log(data._rawValue.data)
  console.log(data._rawValue.meta)

  abs.value = data._rawValue.data
  total.value = data._rawValue.meta.total
  pageCount.value = data._rawValue.meta.last_page - 1
  page.value = data._rawValue.meta.current_page
  console.log(pageCount.value)

  router.push({query: {page: page.value, sort_by_price: orderPrice.value, sort_by_created_at: orderCreated.value}})
}

orderPrice.value = useRoute().query.sort_by_price
orderCreated.value = useRoute().query.sort_by_created_at

load()

definePageMeta({
  layout: "abs",
})

</script>

<template>
  <div>
    <div class="grid grid-cols-2">
      <div>
        Сортировать по цене
        <USelect @click="load" v-model="orderPrice" :options="ordersPrice" option-attribute="name"/>
      </div>
      <div class="ms-4">
        Сортировать по дате создания
        <USelect @click="load" v-model="orderCreated" :options="ordersCreated" option-attribute="name"/>
      </div>
      <br>
    </div>
    <div class="grid grid-cols-4 gap-5">
      <div v-for="ab in abs">
        <AbCard :ab="ab" />
      </div>
    </div>
    <br>
    <UPagination @click="load" v-model="page" :page-count="pageCount" :total="total"

     :to="(page: number, sort_by_price, sort_by_created_at) => ({
      query: { page, sort_by_price, sort_by_created_at },
    })"

    />
  </div>
</template>