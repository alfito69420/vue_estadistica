<template>
    <div class="flex-1 overflow-y-auto p-4">
        <div class="flex flex-col space-y-2">
            <!-- Messages go here -->
            <!-- Example Message -->
            <ChatBubble :its-mine="true" :message="`hola mundo`" />
            <ChatBubble :its-mine="false" :message="`hola mundo 2`" />
        </div>
    </div>
</template>

<script setup lang="ts">
import ChatBubble from '@/components/chat/ChatBubble.vue';
</script>