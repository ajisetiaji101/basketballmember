<script lang="ts">
    // Di masa depan, ini bisa dikaitkan dengan Supabase atau Midtrans
</script>

<svelte:head>
    <title>Membership | Basketball Club</title>
</svelte:head>
<!-- https://images.unsplash.com/photo-1627627256672-027a4613d028?q=80&w=1174&auto=format&fit=crop -->

<!-- Hero Membership -->
<section
    class="relative bg-center bg-cover text-white py-24 px-6 text-center"
    style="background-image: url('https://images.unsplash.com/photo-1627627256672-027a4613d028?q=80&w=1174&auto=format&fit=crop'); background-size: cover; background-position: center;"
>
    <div class="bg-black opacity-50 w-full h-full absolute top-0 left-0"></div>
    <h1 class="text-4xl md:text-5xl font-extrabold mb-4 z-10 relative">
        Gabung sebagai Member Resmi
    </h1>
    <p class="text-lg md:text-xl max-w-3xl mx-auto z-10 relative">
        Dapatkan akses eksklusif ke pelatihan, event, merchandise, dan komunitas
        basket terbaik se-Indonesia.
    </p>
</section>

<!-- Paket Membership -->
<section class="py-20 px-6 md:px-16 max-w-7xl mx-auto">
    <h2 class="text-3xl md:text-4xl font-bold text-center mb-12">
        Pilih Paket Membership
    </h2>
    <div class="grid grid-cols-1 md:grid-cols-3 gap-10">
        <!-- Paket 1 -->
        <div
            class="bg-white rounded-xl shadow-lg p-8 border hover:border-blue-500 transition"
        >
            <h3 class="text-2xl font-bold mb-4">Basic</h3>
            <p class="text-gray-600 mb-6">
                Cocok untuk pemula yang ingin mulai berlatih secara rutin.
            </p>
            <ul class="space-y-2 text-gray-700 mb-6">
                <li>✅ Akses latihan mingguan</li>
                <li>✅ Grup WhatsApp komunitas</li>
                <li>❌ Tiket event gratis</li>
            </ul>
            <div class="text-3xl font-bold mb-6">Rp150.000/bulan</div>
            <a
                href="#form"
                class="block bg-blue-600 text-white text-center py-3 rounded-full font-semibold hover:bg-blue-700 transition"
                >Daftar Sekarang</a
            >
        </div>

        <!-- Paket 2 -->
        <div
            class="bg-white rounded-xl shadow-xl p-8 border-4 border-yellow-400 transform scale-105"
        >
            <h3 class="text-2xl font-bold mb-4">Pro</h3>
            <p class="text-gray-600 mb-6">
                Untuk atlet serius yang ingin akses penuh dan peluang
                bertanding.
            </p>
            <ul class="space-y-2 text-gray-700 mb-6">
                <li>✅ Akses latihan harian</li>
                <li>✅ Jersey eksklusif gratis</li>
                <li>✅ Tiket 2 event per tahun</li>
            </ul>
            <div class="text-3xl font-bold mb-6">Rp300.000/bulan</div>
            <a
                href="#form"
                class="block bg-yellow-400 text-black text-center py-3 rounded-full font-semibold hover:bg-yellow-500 transition"
                >Daftar Sekarang</a
            >
        </div>

        <!-- Paket 3 -->
        <div
            class="bg-white rounded-xl shadow-lg p-8 border hover:border-blue-500 transition"
        >
            <h3 class="text-2xl font-bold mb-4">Elite</h3>
            <p class="text-gray-600 mb-6">
                Untuk member yang ingin tampil di tingkat nasional &
                internasional.
            </p>
            <ul class="space-y-2 text-gray-700 mb-6">
                <li>✅ Semua fitur Pro</li>
                <li>✅ Konsultasi pelatih pribadi</li>
                <li>✅ Undangan turnamen khusus</li>
            </ul>
            <div class="text-3xl font-bold mb-6">Rp500.000/bulan</div>
            <a
                href="#form"
                class="block bg-blue-600 text-white text-center py-3 rounded-full font-semibold hover:bg-blue-700 transition"
                >Daftar Sekarang</a
            >
        </div>
    </div>
</section>

<!-- Form CTA -->
<section id="form" class="bg-gray-100 py-20 px-6 md:px-16">
    <h2 class="text-3xl font-bold text-center mb-10">
        Formulir Pendaftaran Awal
    </h2>
    <form class="max-w-2xl mx-auto bg-white p-8 rounded-xl shadow space-y-6">
        <div>
            <label class="block font-semibold mb-2">Nama Lengkap</label>
            <input
                type="text"
                class="w-full px-4 py-3 border rounded focus:outline-none focus:ring-2 focus:ring-blue-500"
            />
        </div>
        <div>
            <label class="block font-semibold mb-2">Email</label>
            <input
                type="email"
                class="w-full px-4 py-3 border rounded focus:outline-none focus:ring-2 focus:ring-blue-500"
            />
        </div>
        <div>
            <label class="block font-semibold mb-2">No WhatsApp</label>
            <input
                type="text"
                class="w-full px-4 py-3 border rounded focus:outline-none focus:ring-2 focus:ring-blue-500"
            />
        </div>
        <div>
            <label class="block font-semibold mb-2">Paket Pilihan</label>
            <select
                class="w-full px-4 py-3 border rounded focus:outline-none focus:ring-2 focus:ring-blue-500"
            >
                <option>Basic</option>
                <option>Pro</option>
                <option>Elite</option>
            </select>
        </div>
        <button
            type="submit"
            class="w-full bg-blue-600 text-white py-3 rounded-full font-bold hover:bg-blue-700 transition"
            >Kirim Pendaftaran</button
        >
    </form>
</section>
