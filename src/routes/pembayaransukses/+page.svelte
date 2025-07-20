<script lang="ts">
    import checkImage from "$lib/images/check.png";

    let name = "Aji Setiaji";
    let amount = "1000000";
    let method = "QRIS";

    const backToHome = () => {
        window.location.href = "/";
    };
</script>

<div
    class="min-h-screen flex items-center justify-center bg-gradient-to-br from-blue-100 via-white to-blue-200 px-6 py-10"
>
    <div
        class="bg-white max-w-md w-full p-10 rounded-3xl shadow-2xl text-center space-y-6 relative overflow-hidden"
    >
        <div class="flex justify-center">
            <img
                src={checkImage}
                alt="Success"
                class="w-24 h-24 object-contain drop-shadow-lg animate-scale-in"
            />
        </div>

        <h2 class="text-3xl font-bold text-blue-700">Pembayaran Berhasil!</h2>
        <p class="text-gray-600 leading-relaxed">
            Terima kasih, <strong>{name}</strong>.<br />
            Pembayaran sebesar <strong>Rp {amount}</strong><br />
            melalui <strong>{method}</strong> telah diterima.
        </p>

        <div class="border-t border-gray-200 pt-4 text-sm text-gray-500">
            Kode Transaksi: <code>TRX-{Math.floor(Math.random() * 999999)}</code
            >
        </div>

        <button
            on:click={backToHome}
            class="mt-6 w-full py-2 px-4 bg-blue-600 hover:bg-blue-700 text-white font-semibold rounded-xl transition duration-200 shadow-md"
        >
            Kembali ke Beranda
        </button>
    </div>
</div>

<style>
    @keyframes scale-in {
        0% {
            transform: scale(0.5);
            opacity: 0;
        }
        100% {
            transform: scale(1);
            opacity: 1;
        }
    }

    .animate-scale-in {
        animation: scale-in 0.4s ease-out forwards;
    }
</style>
