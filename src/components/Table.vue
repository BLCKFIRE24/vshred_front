<template>
	<table class="table">
		<thead class="thead-dark">
			<td>Image</td>
			<td>Name</td>
			<td>Price</td>
			<td>Quanity</td>
			<td>Purchase</td>
		</thead>
		<tbody>
			
			<tr v-for = "(product, index) in products" :key="index">
				<td>
					<img v-if="product.images.url" class="image" :src="product.images.url"/>
				</td>
				<td>{{ product.name }}</td>
				<td>{{ product.price }}</td>
				<td>{{ product.quantity }}</td>
				<td>
					<button @click="addToCart(product)" class='button'>Purchase</button>
				</td>
			</tr>
		</tbody>
	</table> 
</template>


<script>
import Vue from 'vue';
import axios from 'axios'
import VueAxios from 'vue-axios'


const API = 'https://app.vshred.com/api/offers?include=images&per_page=25&page=1'

Vue.use(VueAxios,axios)

export default {
	name:"Table",
	data() {
		return {
			products: [],
			loading:false,
		}
	},

	mounted() {
		Vue.axios.get(API)
		.then((resp) => {
			this.products=resp.data.data;
			console.log(resp.data.data)
		})
	}
}

</script>

<style scoped>
	.image {
		max-width: 50px;

	}
</style>




