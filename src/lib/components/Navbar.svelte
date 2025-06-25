<script lang="ts">
    import { onClickOutside } from "$lib/utils/onClickOutside"; // helper (lihat di bawah)
    import { onMount } from "svelte";
    let userName = "Aji Setiaji";
    let dropdownOpen = false;

    let dropdownRef: HTMLDivElement;

    // Tutup dropdown saat klik di luar elemen
    onMount(() => {
        onClickOutside(dropdownRef, () => {
            dropdownOpen = false;
        });
    });

    const logout = () => {
        localStorage.removeItem("user");
        location.href = "/login"; // arahkan ke halaman login
    };
</script>

<header
    class="h-16 bg-white shadow flex items-center justify-between px-6 relative z-10"
>
    <div class="text-lg font-semibold text-gray-800">Dashboard Membership</div>
    <div class="relative" bind:this={dropdownRef}>
        <button
            on:click={() => (dropdownOpen = !dropdownOpen)}
            class="flex items-center space-x-2 focus:outline-none"
        >
            <img
                src="https://ui-avatars.com/api/?name=Admin"
                alt="Avatar"
                class="w-8 h-8 rounded-full"
            />
            <span class="text-gray-700 text-sm">{userName}</span>
            <svg
                class="w-4 h-4 text-gray-500"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
            >
                <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M19 9l-7 7-7-7"
                />
            </svg>
        </button>

        {#if dropdownOpen}
            <div
                class="absolute right-0 mt-2 w-40 bg-white border border-gray-200 rounded-md shadow-lg overflow-hidden"
            >
                <button
                    on:click={logout}
                    class="block w-full text-left px-4 py-2 text-sm text-gray-700 hover:bg-gray-100"
                >
                    Logout
                </button>
            </div>
        {/if}
    </div>
</header>
