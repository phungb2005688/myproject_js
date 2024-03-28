<script>
export default {
    props: {
        users: { type: Object, required: true },
    },
};
</script>
<template>
    <div>
        <div class="d-flex" style="margin-left: 15px; ">
            <strong class="d-flex" style="margin-top: 12px;">Bạn là Admin: <span style="padding-left: 5px;"> {{ users.username }}</span></strong>
            
            <i v-if="users.isAdmin" class="bi bi-check text-success" style="font-size: xx-large;"></i>
            <i v-else class="bi bi-x text-danger" style="font-size: xx-large;"></i>

        </div>
    </div>
</template>
