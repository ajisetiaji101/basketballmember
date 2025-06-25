<script lang="ts">
    let username = "";
    let password = "";
    let errorMsg = "";

    const handleLogin = () => {
        if (username === "admin" && password === "123") {
            localStorage.setItem(
                "user",
                JSON.stringify({ username, role: "admin" }),
            );
            location.href = "/";
        } else {
            errorMsg = "Username atau password salah!";
        }
    };
</script>

<div class="min-h-screen flex flex-col md:flex-row">
    <!-- LEFT COLUMN -->
    <div
        class="hidden md:flex md:w-1/2 bg-cover bg-center relative text-white items-center justify-center px-10"
        style="background-image: url('https://images.unsplash.com/photo-1682486519525-a2c2d1c65b8b?q=80&w=1170&auto=format&fit=crop');"
    >
        <div
            class="bg-black opacity-50 w-full h-full absolute top-0 left-0"
        ></div>
        <div class="z-10 text-center">
            <h1 class="text-4xl md:text-5xl font-bold mb-4">Basketball Club</h1>
            <p class="text-lg md:text-xl text-gray-200">
                Bergabung dan menangkan pertandingan bersama tim terbaik!
            </p>
        </div>
    </div>

    <!-- RIGHT COLUMN -->
    <div
        class="w-full md:w-1/2 flex items-center justify-center p-8 sm:p-12 bg-gray-50"
    >
        <div class="w-full max-w-md animate-fade-in">
            <h2
                class="text-3xl sm:text-4xl font-bold mb-6 text-gray-800 text-center"
            >
                Login Akun Anda
            </h2>

            {#if errorMsg}
                <div
                    class="mb-6 bg-red-100 border border-red-400 text-red-700 px-4 py-3 rounded relative"
                    role="alert"
                >
                    <strong class="font-bold">Error!</strong>
                    <span class="block sm:inline"> {errorMsg} </span>
                </div>
            {/if}

            <form on:submit|preventDefault={handleLogin} class="space-y-5">
                <div>
                    <label
                        for="username"
                        class="block text-gray-700 text-sm font-medium mb-2"
                        >Username</label
                    >
                    <input
                        type="text"
                        id="username"
                        bind:value={username}
                        class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-blue-500 focus:border-blue-500 transition shadow-sm"
                        placeholder="Masukkan username Anda"
                        required
                    />
                </div>

                <div>
                    <label
                        for="password"
                        class="block text-gray-700 text-sm font-medium mb-2"
                        >Password</label
                    >
                    <input
                        type="password"
                        id="password"
                        bind:value={password}
                        class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-blue-500 focus:border-blue-500 transition shadow-sm"
                        placeholder="Masukkan password Anda"
                        required
                    />
                </div>

                <button
                    type="submit"
                    class="w-full bg-blue-600 hover:bg-blue-700 text-white font-semibold py-3 rounded-lg transition duration-300 hover:shadow-md transform hover:-translate-y-0.5"
                >
                    Login
                </button>
            </form>

            <p class="mt-6 text-sm text-center text-gray-500">
                Belum punya akun?
                <a
                    href="/membership"
                    class="text-blue-600 hover:text-blue-800 font-semibold hover:underline ml-1"
                    >Daftar Sekarang</a
                >
            </p>
        </div>
    </div>
</div>

<style>
    @keyframes fade-in {
        from {
            opacity: 0;
            transform: translateY(20px);
        }
        to {
            opacity: 1;
            transform: translateY(0);
        }
    }
    .animate-fade-in {
        animation: fade-in 0.8s ease-out forwards;
    }
</style>
