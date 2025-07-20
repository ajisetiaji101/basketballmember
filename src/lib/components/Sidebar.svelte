<script lang="ts">
    import {
        Home,
        FileText,
        Image,
        File,
        Settings,
        User,
        PersonStanding,
        Info,
        Club,
        ClubIcon,
    } from "lucide-svelte";
    import { page } from "$app/stores";
    import { derived } from "svelte/store";

    const menus = [
        { name: "Dashboard", icon: Home, path: "/dashboard" },
        { name: "Profile", icon: User, path: "/dashboard/profile" },
        { name: "Pembayaran", icon: FileText, path: "/dashboard/pembayaran" },
        { name: "Event", icon: Image, path: "/dashboard/events" },
        { name: "Member", icon: PersonStanding, path: "/dashboard/members" },
        { name: "Subscription", icon: Info, path: "/dashboard/subscriptions" },
        { name: "Settings", icon: Settings, path: "/dashboard/settings" },
        { name: "Tim", icon: ClubIcon, path: "/dashboard/tim" },
    ];

    const currentPath = derived(page, ($page) => $page.url.pathname);
</script>

<aside
    class="w-64 bg-gray-900 text-white flex flex-col transition-all duration-300"
>
    <!-- Logo / Brand -->
    <div class="px-6 py-5 border-b border-gray-800">
        <span class="text-2xl font-bold text-white">🏀 </span>
        <span class="ml-2 text-lg font-semibold">Basketball Club</span>
    </div>

    <!-- Navigation -->
    <nav class="flex-1 px-4 py-6 space-y-1">
        {#each menus as { name, icon: Icon, path }}
            <a
                href={path}
                class="group flex items-center px-4 py-2 rounded-lg hover:bg-gray-800 transition
              {$currentPath === path ? 'bg-gray-800' : ''}"
            >
                <Icon
                    class="w-5 h-5 mr-3 text-gray-400 group-hover:text-white"
                />
                <span class="text-sm">{name}</span>
            </a>
        {/each}
    </nav>

    <!-- Footer / Collapse (Optional) -->
    <div class="px-4 py-4 border-t border-gray-800 text-sm text-gray-500">
        <span>&copy; 2025 WP Clone</span>
    </div>
</aside>
