# Flex, Inline Flex?

<br>

<div class="border-1 border-dashed border-red border-2">
    <div class="flex bg-green-100 p-4 h-30 gap-3 self-center">
        <div class="flex-item">flex item</div>
        <div class="flex-item">flex item</div>
        <div class="flex-item">flex item</div>
        <div class="flex-item">flex item</div>
    </div>
</div>
<div class="text-center text-gray-500">display: flex</div>

<div class="border-1 border-dashed border-red border-2 mt-8">
    <div class="inline-flex bg-green-100 p-4 h-30 gap-3 self-center">
        <div class="flex-item">flex item</div>
        <div class="flex-item">flex item</div>
        <div class="flex-item">flex item</div>
        <div class="flex-item">flex item</div>
    </div>
</div>
<div class="text-center text-gray-500">display: inline-flex</div>

<style>
    .flex-item {
        @apply bg-white
            p-2
            flex-1;
    }
</style>