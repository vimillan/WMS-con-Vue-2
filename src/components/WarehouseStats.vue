<template>
    <div class="center-item gap-3 mb-3">
        <div class="my-2 center-item gap-2 justify-content-between">
            <div class="bg-white shadow rounded-xs center-item gap-3" style="padding: 10px 17px;">
                <div class="ps-2">
                    <small class="text-secondary fs-11">Total productos</small>
                    <div class="fs-20 fw-bold">
                        {{ stats.productos }}
                    </div>
                </div>
                <div class="hw-45 fw-bold bg-primary-op text-primary center p-1 rounded-xs">
                    <i class='bx bx-package icon-lg'></i>
                </div>
            </div>
        </div>
        <div class="my-3 center-item gap-2 justify-content-between">
            <div class="bg-white shadow rounded-xs center-item gap-4" style="padding: 10px 17px;">
                <div class="ps-2">
                    <small class="text-secondary fs-11">Total productos</small>
                    <div class="fs-20 fw-bold">
                        {{ stats.almacen }}
                    </div>
                </div>
                <div class="hw-45 fw-bold bg-primary-op text-primary center p-1 rounded-xs">
                    <i class="bx bx-line-chart icon-lg"></i>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "WarehouseStats",
    props: {
        stats: {
            type: Object,
            required: true
        }
    },
};
</script>