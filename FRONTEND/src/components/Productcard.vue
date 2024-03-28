<script>
export default {
	props: {
		products: { type: Object, required: true },
	},
};
</script>
<template>
	<div class="d-flex">
		<div class="p-1 d-fex flex-column">
			<img :src=" products.img[0]" alt="img" width="120">
			<span class="d-block">{{ products.title }}</span>
		</div>
	</div>
</template>
