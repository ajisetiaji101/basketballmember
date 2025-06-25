<script lang="ts">
    import Sidebar from "$lib/components/Sidebar.svelte";
    import Navbar from "$lib/components/Navbar.svelte";
</script>

<div class="flex h-screen">
    <Sidebar />
    <div class="flex-1 flex flex-col">
        <Navbar />
        <main class="flex-1 p-6 bg-gray-100 overflow-auto">
            <slot />
        </main>
    </div>
</div>
