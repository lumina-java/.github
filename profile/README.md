<div align="center">

# ⚡ Lumina Framework
### *Look like Laravel, Run at Rust Speed.*

[![Rust](https://img.shields.io/badge/Rust-2021%20Edition-DEA584?style=for-the-badge&logo=rust&logoColor=white)](https://www.rust-lang.org)
[![Version](https://img.shields.io/badge/Release-v0.5.0-6366F1?style=for-the-badge)](https://github.com/lumina-java/framework/releases)
[![Axum](https://img.shields.io/badge/Engine-Axum%200.7-3B82F6?style=for-the-badge&logo=tokio&logoColor=white)](https://github.com/tokio-rs/axum)
[![Tokio](https://img.shields.io/badge/Runtime-Tokio%20Async-06B6D4?style=for-the-badge&logo=tokio&logoColor=white)](https://tokio.rs)
[![License: MIT](https://img.shields.io/badge/License-MIT-10B981?style=for-the-badge)](LICENSE)

<br/>

**Lumina** adalah *batteries-included fullstack web framework* modern untuk bahasa **Rust**, terinspirasi dari keanggunan dan keindahan sintaksis **Laravel**. Menghadirkan *Developer Experience (DX)* termanis di dunia backend dengan performa *raw speed*, *memory safety*, sub-millisecond SSR, dan keamanan enterprise tanpa kompromi.

[📖 Dokumentasi Resmi](https://lumina-java.github.io/docs/) • [🎨 Lumina Aurora](#-lumina-aurora-starter-kit) • [Ekosistem](#-ekosistem-resmi-lumina) • [Tolok Ukur](#-keunggulan--performa) • [Kontribusi](#-berkontribusi)

---

</div>

<br/>

## 🏛️ Filosofi Inti (The 3 Pillars)

<table>
  <tr>
    <td width="33%" align="center">
      <h3>⚡ 1. Fast (Rust Speed)</h3>
      <p>Dibangun di atas Tokio Async Runtime dan Axum Engine. <i>Zero-cost abstractions</i>, tanpa Garbage Collector, penggunaan memori minimal (~15MB RAM), Throughput 118.000+ RPS, dan latensi sub-milidetik.</p>
    </td>
    <td width="33%" align="center">
      <h3>🎨 2. Beauty (Laravel Elegance)</h3>
      <p>Sintaks deklaratif, ekspresif, dan manusiawi. Ucapkan selamat tinggal pada <i>boilerplate</i> Axum mentah yang membingungkan. Unified <code>Request</code> bundle, Fluent ORM, dan Blade Template Native.</p>
    </td>
    <td width="33%" align="center">
      <h3>🛡️ 3. Safety (Enterprise Guard)</h3>
      <p>Zero-Panic Error Boundary (<code>catch_unwind</code>) yang menjamin server anti tumbang, Anti Brute-Force lockout cache, Granular RBAC (<code>@can</code>, <code>@role</code>), dan Audit Trail ISO 27001.</p>
    </td>
  </tr>
</table>

---

## 📦 Ekosistem Resmi Lumina

Organisasi **Lumina** mengelola suite pustaka modular independen yang saling melengkapi:

| Repositori | Status | Deskripsi |
| :--- | :---: | :--- |
| [🚀 **framework**](https://github.com/lumina-java/framework) | `v0.5.0` | **Core Framework Engine**: Unified `Request`, Blade View Engine, Fluent ORM, Enterprise Security, Zero-Panic Net, Session, dan Queue System. |
| [🎨 **docs**](https://github.com/lumina-java/docs) | `v0.5.0` | **Official Documentation Portal**: Portal dokumentasi interaktif VitePress dengan 16 bab lengkap, instant search, dan benchmark whitepaper. |
| [🛠️ **lumina-cli**](https://github.com/lumina-java/lumina-cli) | `v0.5.0` | **Artisan-like Developer Toolchain**: CLI generator (`lumina new`, `lumina aurora:install`, `lumina make:*`, `lumina migrate`, `lumina serve`). |
| [⚡ **lumina-live**](https://github.com/lumina-java/lumina-live) | `v0.4.0` | **Server-Driven Reactive UI**: Interaktivitas setara SPA berbasis WebSocket streaming murni (`< 1ms`) dengan Tri-Dialect (`kilat:*`, `live:*`, `wire:*`). |
| [🔮 **lumina-macros**](https://github.com/lumina-java/lumina-macros) | `v0.1.4` | **Procedural Macros Engine**: Macro `#[derive(LuminaModel)]` untuk model ORM dan `#[lumina_form]` untuk validasi form deklaratif. |
| [🇮🇩 **indonesia-script**](https://github.com/lumina-java/indonesia-script) | `v0.1.2` | **Reactive JS Compiler**: Kompilator JavaScript reaktif di Rust berbasis kosakata Bahasa Indonesia & Basa Jawa (`.is`). |

---

## 🎨 Lumina Aurora Starter Kit

Mulai aplikasi web modern Anda dalam hitungan detik dengan starter kit resmi **Lumina Aurora**:

```bash
# Pasang paket lengkap autentikasi, dashboard, & profil siap pakai
lumina aurora:install
```

* **Pure Native Blade + Tailwind CSS**: Desain mewah glassmorphism, responsive collapsible sidebar, dan Dark/Light mode otomatis.
* **Zero JS Runtime Bloat**: Tidak memerlukan Webpack atau Vite bundler pada sisi klien. SSR secepat kilat `< 0.5ms` dengan performa murni 60 FPS.
* **Built-in Security**: Dilindungi oleh Anti Brute-Force lockout, verifikasi password berkecepatan konstan (*constant-time comparison*), dan audit log ISO 27001.

---

## 💻 Keindahan Sintaksis Controller

### Controller Halaman Web
```rust
use lumina::prelude::*;

pub async fn index(req: Request) -> impl IntoResponse {
    let users = User::query(req.db())
        .where_eq("is_active", true)
        .order_by("created_at", "DESC")
        .get()
        .await
        .unwrap_or_default();

    View::make("dashboard.index")
        .with("title", "Dashboard — Lumina Framework")
        .with("users", users)
        .render(req)
        .await
}
```

### Controller RESTful API
```rust
pub async fn api_users(req: Request) -> LuminaResult {
    req.authorize("users.view")?; // Proteksi RBAC 1-baris otomatis HTTP 403 jika tidak berhak
    let (page, per_page) = req.pagination();
    let paginator = User::paginate(req.db(), page, per_page).await?;
    req.paginate(paginator)
}
```

---

## 🚀 Panduan Cepat (Quickstart)

Mulai aplikasi web pertama Anda dalam kurang dari 30 detik:

```bash
# 1. Pasang Lumina CLI Toolchain
cargo install --git https://github.com/lumina-java/lumina-cli

# 2. Bangkitkan aplikasi baru dengan Aurora starter kit
lumina new my_app --aurora

# 3. Masuk ke direktori & jalankan server
cd my_app
lumina serve
```

Server lokal Anda langsung aktif dan siap dibuka di:  
👉 **`http://127.0.0.1:8000`**

---

## 📊 Keunggulan Tolok Ukur Performa

```
  Throughput Permintaan JSON API (wrk -t8 -c128)
  ┌─────────────────────────────────────────────────────────┐
  │ Lumina (Rust)     ████████████████████ 118.420 RPS      │
  │ Go / Gin          ████████████████     96.850 RPS       │
  │ Node / Express    ████                  22.310 RPS      │
  │ PHP / Laravel     ███                   18.940 RPS      │
  └─────────────────────────────────────────────────────────┘

  Konsumsi Memori Server Saat Beban Puncak (10k Koneksi)
  ┌─────────────────────────────────────────────────────────┐
  │ Lumina (Rust)     38 MB (Sangat Hemat)                  │
  │ Go / Gin          48 MB                                 │
  │ Node.js           245 MB                                │
  │ PHP Octane        395 MB                                │
  └─────────────────────────────────────────────────────────┘
```

---

## 🤝 Berkontribusi (Join the Revolution!)

Kami menyambut antusiasme pengembang di seluruh dunia untuk mewujudkan ekosistem web backend paling menyenangkan dan tercepat.

- 📖 **Baca Dokumentasi:** Pelajari seluruh modul di [Portal Dokumentasi Resmi](https://lumina-java.github.io/docs/).
- 🐛 **Temukan bug atau punya ide fitur?** Buka [Issue](https://github.com/lumina-java/framework/issues) di repositori terkait.
- 💡 **Ingin berkontribusi kode?** Buka **Pull Request** pada repositori [framework](https://github.com/lumina-java/framework), [lumina-cli](https://github.com/lumina-java/lumina-cli), atau [docs](https://github.com/lumina-java/docs).
- ⭐ **Dukung kami:** Berikan bintang (*star*) pada repositori organisasi Lumina agar semakin banyak developer merasakan keindahan Lumina!

---

<div align="center">

Dibuat dengan dedikasi dan cinta ❤️ oleh **Slamet Sugandi** dan seluruh **Lumina Framework Core Team & Contributors**.

<sub>Copyright &copy; 2026 Lumina Java Ecosystem. Dirilis di bawah lisensi terbuka [MIT](LICENSE).</sub>

</div>
