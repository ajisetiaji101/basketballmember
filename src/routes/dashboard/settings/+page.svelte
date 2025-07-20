<script lang="ts">
    import {
        User,
        Lock,
        Bell,
        Shield,
        Trash2,
        Save,
        X,
        Edit,
        Info,
    } from "lucide-svelte"; // Added Info icon for descriptions

    // --- Mock Data for User Settings ---
    // In a real application, this data would be fetched from a backend
    let userName = "Aji Setiaji";
    let userEmail = "aji@example.com";
    let userAvatarUrl = "https://i.pravatar.cc/150?img=8";
    let receiveEmailNotifications = true;
    let receivePushNotifications = false;
    let enableTwoFactorAuth = false;
    let showProfilePublicly = true;

    // --- State for Edit Mode (Optional, but good for UX) ---
    let isEditingProfile = false;
    let isEditingSecurity = false;

    // --- Form Data for Editing (to avoid direct mutation) ---
    let tempUserName = userName;
    let tempUserEmail = userEmail;
    let newPassword = "";
    let confirmNewPassword = "";

    // --- Functions to handle saving/canceling changes ---
    function saveProfile() {
        // Basic validation
        if (!tempUserName.trim() || !tempUserEmail.trim()) {
            alert("Nama dan Email tidak boleh kosong.");
            return;
        }
        if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(tempUserEmail)) {
            alert("Format email tidak valid.");
            return;
        }

        userName = tempUserName;
        userEmail = tempUserEmail;
        isEditingProfile = false;
        alert("Profil berhasil diperbarui!");
    }

    function cancelProfileEdit() {
        tempUserName = userName;
        tempUserEmail = userEmail;
        isEditingProfile = false;
    }

    function changePassword() {
        if (newPassword.length < 6) {
            alert("Kata sandi minimal 6 karakter!");
            return;
        }
        if (newPassword !== confirmNewPassword) {
            alert("Kata sandi baru tidak cocok!");
            return;
        }

        alert("Kata sandi berhasil diubah!");
        newPassword = "";
        confirmNewPassword = "";
        isEditingSecurity = false;
    }

    function cancelPasswordEdit() {
        newPassword = "";
        confirmNewPassword = "";
        isEditingSecurity = false;
    }

    function deleteAccount() {
        // Using a custom modal/dialog is preferred over alert/confirm in production
        if (
            confirm(
                "Apakah Anda yakin ingin menghapus akun Anda? Tindakan ini tidak dapat dibatalkan.",
            )
        ) {
            alert("Akun berhasil dihapus (simulasi)!");
            // In a real app, you'd call an API to delete the account and log out the user
        }
    }
</script>

<section class="min-h-screen bg-gray-50 py-16 px-4 sm:px-6 lg:px-8">
    <div class="max-w-4xl mx-auto bg-white rounded-3xl shadow-2xl p-8 sm:p-10">
        <header class="text-center mb-12">
            <h1
                class="text-5xl font-extrabold text-gray-900 mb-4 tracking-tight flex items-center justify-center gap-3"
            >
                <User class="w-12 h-12 text-blue-600" /> Pengaturan Akun
            </h1>
            <p class="text-lg text-gray-700 max-w-2xl mx-auto">
                Sesuaikan pengalaman Anda dan kelola detail akun Anda di satu
                tempat.
            </p>
        </header>

        <div class="space-y-12">
            <!-- Profile Settings Section -->
            <div class="py-10 border-b border-gray-100">
                <div class="flex justify-between items-center mb-6">
                    <h2
                        class="text-3xl font-bold text-gray-800 flex items-center gap-3"
                    >
                        <User class="w-8 h-8 text-blue-500" /> Informasi Profil
                    </h2>
                    {#if !isEditingProfile}
                        <button
                            on:click={() => {
                                isEditingProfile = true;
                                tempUserName = userName;
                                tempUserEmail = userEmail;
                            }}
                            class="text-blue-600 hover:text-blue-800 font-semibold flex items-center gap-2 px-4 py-2 rounded-lg transition-colors duration-200"
                        >
                            <Edit class="w-5 h-5" /> Edit
                        </button>
                    {/if}
                </div>

                <div
                    class="flex flex-col sm:flex-row items-center sm:items-start gap-8"
                >
                    <div class="flex-shrink-0">
                        <img
                            src={userAvatarUrl}
                            alt="Foto Profil"
                            class="w-28 h-28 rounded-full object-cover border-4 border-blue-200 shadow-md"
                        />
                    </div>
                    <div class="flex-1 space-y-5 w-full">
                        {#if isEditingProfile}
                            <div>
                                <label
                                    for="name"
                                    class="block text-sm font-medium text-gray-700 mb-2"
                                    >Nama Lengkap</label
                                >
                                <input
                                    type="text"
                                    id="name"
                                    bind:value={tempUserName}
                                    class="w-full px-4 py-2.5 border border-gray-300 rounded-lg focus:ring-blue-500 focus:border-blue-500 text-base"
                                />
                            </div>
                            <div>
                                <label
                                    for="email"
                                    class="block text-sm font-medium text-gray-700 mb-2"
                                    >Alamat Email</label
                                >
                                <input
                                    type="email"
                                    id="email"
                                    bind:value={tempUserEmail}
                                    class="w-full px-4 py-2.5 border border-gray-300 rounded-lg focus:ring-blue-500 focus:border-blue-500 text-base"
                                />
                            </div>
                            <div class="flex flex-col sm:flex-row gap-3 mt-4">
                                <button
                                    on:click={saveProfile}
                                    class="flex-1 bg-blue-600 hover:bg-blue-700 text-white font-semibold py-2.5 rounded-lg transition-colors duration-200 flex items-center justify-center gap-2"
                                >
                                    <Save class="w-5 h-5" /> Simpan Perubahan
                                </button>
                                <button
                                    on:click={cancelProfileEdit}
                                    class="flex-1 bg-gray-200 hover:bg-gray-300 text-gray-800 font-semibold py-2.5 rounded-lg transition-colors duration-200 flex items-center justify-center gap-2"
                                >
                                    <X class="w-5 h-5" /> Batal
                                </button>
                            </div>
                        {:else}
                            <div class="bg-gray-50 p-4 rounded-lg">
                                <p
                                    class="text-sm font-medium text-gray-500 mb-1"
                                >
                                    Nama
                                </p>
                                <p class="text-lg font-semibold text-gray-900">
                                    {userName}
                                </p>
                            </div>
                            <div class="bg-gray-50 p-4 rounded-lg">
                                <p
                                    class="text-sm font-medium text-gray-500 mb-1"
                                >
                                    Email
                                </p>
                                <p class="text-lg font-semibold text-gray-900">
                                    {userEmail}
                                </p>
                            </div>
                        {/if}
                    </div>
                </div>
            </div>

            <!-- Security Settings Section -->
            <div class="py-10 border-b border-gray-100">
                <div class="flex justify-between items-center mb-6">
                    <h2
                        class="text-3xl font-bold text-gray-800 flex items-center gap-3"
                    >
                        <Lock class="w-8 h-8 text-purple-500" /> Keamanan Akun
                    </h2>
                    {#if !isEditingSecurity}
                        <button
                            on:click={() => {
                                isEditingSecurity = true;
                                newPassword = "";
                                confirmNewPassword = "";
                            }}
                            class="text-blue-600 hover:text-blue-800 font-semibold flex items-center gap-2 px-4 py-2 rounded-lg transition-colors duration-200"
                        >
                            <Edit class="w-5 h-5" /> Ubah Kata Sandi
                        </button>
                    {/if}
                </div>

                {#if isEditingSecurity}
                    <div class="space-y-4 mb-6">
                        <div>
                            <label
                                for="new-password"
                                class="block text-sm font-medium text-gray-700 mb-2"
                                >Kata Sandi Baru</label
                            >
                            <input
                                type="password"
                                id="new-password"
                                bind:value={newPassword}
                                class="w-full px-4 py-2.5 border border-gray-300 rounded-lg focus:ring-purple-500 focus:border-purple-500 text-base"
                            />
                        </div>
                        <div>
                            <label
                                for="confirm-password"
                                class="block text-sm font-medium text-gray-700 mb-2"
                                >Konfirmasi Kata Sandi Baru</label
                            >
                            <input
                                type="password"
                                id="confirm-password"
                                bind:value={confirmNewPassword}
                                class="w-full px-4 py-2.5 border border-gray-300 rounded-lg focus:ring-purple-500 focus:border-purple-500 text-base"
                            />
                        </div>
                        <div class="flex flex-col sm:flex-row gap-3 mt-4">
                            <button
                                on:click={changePassword}
                                class="flex-1 bg-purple-600 hover:bg-purple-700 text-white font-semibold py-2.5 rounded-lg transition-colors duration-200 flex items-center justify-center gap-2"
                            >
                                <Save class="w-5 h-5" /> Simpan Kata Sandi
                            </button>
                            <button
                                on:click={cancelPasswordEdit}
                                class="flex-1 bg-gray-200 hover:bg-gray-300 text-gray-800 font-semibold py-2.5 rounded-lg transition-colors duration-200 flex items-center justify-center gap-2"
                            >
                                <X class="w-5 h-5" /> Batal
                            </button>
                        </div>
                    </div>
                {/if}

                <div class="flex items-center justify-between mb-2">
                    <span class="text-lg text-gray-700"
                        >Otentikasi Dua Faktor (2FA)</span
                    >
                    <label
                        class="relative inline-flex items-center cursor-pointer"
                    >
                        <input
                            type="checkbox"
                            bind:checked={enableTwoFactorAuth}
                            class="sr-only peer"
                        />
                        <div
                            class="w-11 h-6 bg-gray-200 peer-focus:outline-none peer-focus:ring-4 peer-focus:ring-purple-300 rounded-full peer peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:left-[2px] after:bg-white after:border after:border-gray-300 after:rounded-full after:h-5 after:w-5 after:transition-all peer-checked:bg-purple-600"
                        ></div>
                    </label>
                </div>
                <p class="text-sm text-gray-500 flex items-center gap-1">
                    <Info class="w-4 h-4" /> Tambahkan lapisan keamanan ekstra ke
                    akun Anda.
                </p>
            </div>

            <!-- Notification Settings Section -->
            <div class="py-10 border-b border-gray-100">
                <h2
                    class="text-3xl font-bold text-gray-800 mb-6 flex items-center gap-3"
                >
                    <Bell class="w-8 h-8 text-orange-500" /> Preferensi Notifikasi
                </h2>
                <div class="space-y-6">
                    <div>
                        <div class="flex items-center justify-between mb-2">
                            <span class="text-lg text-gray-700"
                                >Notifikasi Email</span
                            >
                            <label
                                class="relative inline-flex items-center cursor-pointer"
                            >
                                <input
                                    type="checkbox"
                                    bind:checked={receiveEmailNotifications}
                                    class="sr-only peer"
                                />
                                <div
                                    class="w-11 h-6 bg-gray-200 peer-focus:outline-none peer-focus:ring-4 peer-focus:ring-orange-300 rounded-full peer peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:left-[2px] after:bg-white after:border after:border-gray-300 after:rounded-full after:h-5 after:w-5 after:transition-all peer-checked:bg-orange-600"
                                ></div>
                            </label>
                        </div>
                        <p
                            class="text-sm text-gray-500 flex items-center gap-1"
                        >
                            <Info class="w-4 h-4" /> Terima pembaruan penting dan
                            promosi melalui email.
                        </p>
                    </div>

                    <div>
                        <div class="flex items-center justify-between mb-2">
                            <span class="text-lg text-gray-700"
                                >Notifikasi Push</span
                            >
                            <label
                                class="relative inline-flex items-center cursor-pointer"
                            >
                                <input
                                    type="checkbox"
                                    bind:checked={receivePushNotifications}
                                    class="sr-only peer"
                                />
                                <div
                                    class="w-11 h-6 bg-gray-200 peer-focus:outline-none peer-focus:ring-4 peer-focus:ring-orange-300 rounded-full peer peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:left-[2px] after:bg-white after:border after:border-gray-300 after:rounded-full after:h-5 after:w-5 after:transition-all peer-checked:bg-orange-600"
                                ></div>
                            </label>
                        </div>
                        <p
                            class="text-sm text-gray-500 flex items-center gap-1"
                        >
                            <Info class="w-4 h-4" /> Dapatkan notifikasi instan langsung
                            di perangkat Anda.
                        </p>
                    </div>
                </div>
            </div>

            <!-- Privacy Settings Section -->
            <div class="py-10 border-b border-gray-100">
                <h2
                    class="text-3xl font-bold text-gray-800 mb-6 flex items-center gap-3"
                >
                    <Shield class="w-8 h-8 text-green-500" /> Pengaturan Privasi
                </h2>
                <div class="space-y-4">
                    <div class="flex items-center justify-between mb-2">
                        <span class="text-lg text-gray-700">Profil Publik</span>
                        <label
                            class="relative inline-flex items-center cursor-pointer"
                        >
                            <input
                                type="checkbox"
                                bind:checked={showProfilePublicly}
                                class="sr-only peer"
                            />
                            <div
                                class="w-11 h-6 bg-gray-200 peer-focus:outline-none peer-focus:ring-4 peer-focus:ring-green-300 rounded-full peer peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:left-[2px] after:bg-white after:border after:border-gray-300 after:rounded-full after:h-5 after:w-5 after:transition-all peer-checked:bg-green-600"
                            ></div>
                        </label>
                    </div>
                    <p class="text-sm text-gray-500 flex items-center gap-1">
                        <Info class="w-4 h-4" /> Izinkan profil Anda terlihat oleh
                        pengguna lain.
                    </p>
                </div>
            </div>

            <!-- Danger Zone / Account Actions -->
            <div class="pt-10">
                <!-- No border-b for the last section -->
                <h2
                    class="text-3xl font-bold text-gray-800 mb-6 flex items-center gap-3"
                >
                    <Trash2 class="w-8 h-8 text-red-500" /> Zona Bahaya
                </h2>
                <p class="text-gray-700 mb-6">
                    Tindakan ini tidak dapat dibatalkan. Harap berhati-hati
                    sebelum melanjutkan.
                </p>
                <button
                    on:click={deleteAccount}
                    class="bg-red-600 hover:bg-red-700 text-white font-bold py-3 px-6 rounded-lg text-lg transition-colors duration-200 flex items-center gap-2 shadow-md hover:shadow-lg"
                >
                    <Trash2 class="w-5 h-5" /> Hapus Akun Saya
                </button>
            </div>
        </div>
    </div>
</section>
