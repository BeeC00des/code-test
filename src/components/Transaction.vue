<template>
	<tbody class="text-center text-black w-full">
	<tr class="pb-3 h-10 border-2 ">
		<td class="text-base text-black font-medium">
			<input type="checkbox" class="" /> <span class="px-3">08-Apr-22</span>
			<br />
			<span class="text-xs text-gray-500">8.34pm</span>
		</td>
		<td class="text-base text-black font-medium">
			<span v-if="transaction.customer">
				{{ transaction.customer.name }}
			</span>
			<span v-else>
				{{ transaction.vendor.name }}
			</span>
		</td>
		<td
			:class="transaction.vendor ? 'text-red-500' : ''"
			class="text-base font-medium"
		>
			₦{{ transaction.amount_paid }}
		</td>
		<td>
			{{ transaction.payment_method }}
		</td>
		<td>
			<span v-if="transaction.products.length == 0">-</span>
			<span v-else>
				{{ products().join(", ") }}
			</span>
		</td>
		<td>
			<span v-if="transaction.products.length > 0">
				{{ products().length }}
			</span>
		</td>
	</tr>
	<tr v-for="payment in transaction.paymentHistories" :key="payment" class="h-10">
			<td>
				<small>{{ payment.paymentDate }}</small>
			</td>
			<td class="text-yellow-500">
				<span class="border">{{ payment.status }}</span>
			</td>
			<td class="text-yellow-500">
				{{ payment.amount }}
			</td>
			<td class="text-yellow-500">
				{{ payment.paymentMethod }}
			</td>
		</tr>
	</tbody>
</template>
<script setup>
	const props = defineProps({
		transaction: {
			type: Object,
			required: true,
		},
	});
	function products() {
		const products = props.transaction.products.map((e) => e.name);
		return products;
	}
	function formatDate() {}
	function formatTime() {}
</script>