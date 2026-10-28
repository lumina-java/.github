<div align="center">

# ⚡ Lumina Framework
### *Look like Laravel, Run at Rust Speed.*

[![Rust](https://img.shields.io/badge/Rust-2021%20Edition-DEA584?style=for-the-badge&logo=rust&logoColor=white)](https://www.rust-lang.org)
[![Axum](https://img.shields.io/badge/Engine-Axum%200.7-3B82F6?style=for-the-badge&logo=tokio&logoColor=white)](https://github.com/tokio-rs/axum)
[![Tokio](https://img.shields.io/badge/Runtime-Tokio%20Async-06B6D4?style=for-the-badge&logo=tokio&logoColor=white)](https://tokio.rs)
[![License: MIT](https://img.shields.io/badge/License-MIT-10B981?style=for-the-badge)](LICENSE)

<br/>

**Lumina** adalah *batteries-included fullstack web framework* modern untuk bahasa **Rust**, terinspirasi dari keanggunan dan keindahan sintaksis **Laravel**. Menghadirkan *Developer Experience (DX)* termanis di dunia backend dengan performa *raw speed*, *memory safety*, dan konkurensi ekstrem tanpa *Garbage Collector*.

[Dokumentasi](#-panduan-cepat-quickstart) • [Ekosistem](#-ekosistem-resmi-lumina) • [Tolok Ukur](#-keunggulan--performa) • [Kontribusi](#-berkontribusi)

---

</div>

<br/>

## 🏛️ Filosofi Inti (The 3 Pillars)

<table>
  <tr>
    <td width="33%" align="center">
      <h3>🎨 Laravel Elegance</h3>
      <p>Sintaks deklaratif, ekspresif, dan manusiawi. Ucapkan selamat tinggal pada <i>boilerplate</i> Axum mentah yang membingungkan. Unified <code>Request</code> bundle, Fluent ORM, dan Blade Template Native.</p>
    </td>
    <td width="33%" align="center">
      <h3>⚡ Rust Raw Speed</h3>
      <p>Dibangun di atas Tokio Async Runtime dan Axum Engine. <i>Zero-cost abstractions</i>, tanpa Garbage Collector, penggunaan memori minimal (~15MB RAM), dan latensi respons sub-milidetik.</p>
    </td>
    <td width="33%" align="center">
      <h3>🔋 Batteries-Included</h3>
      <p>Semua yang Anda butuhkan sudah terintegrasi harmonis: Router, ORM, Migrasi SQLx, WebSocket reaktif, Blade engine, Queue worker, Autentikasi, dan Artisan-like CLI.</p>
    </td>
  </tr>
</table>

---

## 📦 Ekosistem Resmi Lumina

Organisasi **Lumina** mengelola suite pustaka modular independen yang saling melengkapi:

| Repositori | Status | Deskripsi |
| :--- | :---: | :--- |
| [🚀 **framework**](https://github.com/lumina-java/framework) | `v0.4.0` | **Core Framework Engine**: Unified `Request`, Blade View Engine, Fluent ORM, Security, Session, dan Queue System. |
| [⚡ **lumina-live**](https://github.com/lumina-java/lumina-live) | `v0.4.0` | **Server-Driven Reactive UI**: Interaktivitas setara SPA berbasis WebSocket streaming murni (`< 1ms`) dengan Tri-Dialect (`kilat:*`, `live:*`, `wire:*`). |
| [🛠️ **lumina-cli**](https://github.com/lumina-java/lumina-cli) | `v0.4.0` | **Artisan-like Developer Toolchain**: CLI generator (`lumina new`, `lumina make:*`, `lumina migrate`, `lumina serve`). |
| [🔮 **lumina-macros**](https://github.com/lumina-java/lumina-macros) | `v0.1.4` | **Procedural Macros Engine**: Macro `#[derive(LuminaModel)]` untuk model ORM dan `#[lumina_form]` untuk validasi form deklaratif. |
| [🇮🇩 **indonesia-script**](https://github.com/lumina-java/indonesia-script) | `v0.1.2` | **Reactive JS Compiler**: Kompilator JavaScript reaktif di Rust berbasis kosakata Bahasa Indonesia & Basa Jawa (`.is`). |

---

## 💻 Contoh Keindahan Sintaks (Controller & View)

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

# 2. Bangkitkan aplikasi baru
lumina new my_app --db sqlite

# 3. Masuk ke direktori & jalankan server
cd my_app
lumina serve
```

Server lokal Anda langsung aktif dan siap dibuka di:  
👉 **`http://127.0.0.1:8000`**

---

## 📊 Keunggulan & Performa

```
  Penggunaan Memori (Idle)
  ┌─────────────────────────────────────────────────────────┐
  │ Lumina (Rust)     15 MB                                 │
  │ Node.js / Express 65 MB                                 │
  │ PHP / Laravel     45 MB (per worker)                    │
  └─────────────────────────────────────────────────────────┘

  Latensi Routing Rata-Rata (Lokal)
  ┌─────────────────────────────────────────────────────────┐
  │ Lumina (Axum)     0.18 ms (Sub-milidetik)               │
  │ Go / Gin          0.42 ms                               │
  │ Node / Fastify    1.85 ms                               │
  │ PHP FPM           8.20 ms                               │
  └─────────────────────────────────────────────────────────┘
```

---

## 🤝 Berkontribusi (Join the Revolution!)

Kami menyambut antusiasme pengembang di seluruh dunia untuk mewujudkan ekosistem web backend paling menyenangkan dan tercepat.

- 🐛 **Temukan bug atau punya ide fitur?** Buka [Issue](https://github.com/lumina-java/framework/issues) di repositori terkait.
- 💡 **Ingin berkontribusi kode?** Buka **Pull Request** pada repositori [framework](https://github.com/lumina-java/framework), [lumina-live](https://github.com/lumina-java/lumina-live), atau [lumina-cli](https://github.com/lumina-java/lumina-cli).
- ⭐ **Dukung kami:** Berikan bintang (*star*) pada repositori organisasi Lumina agar semakin banyak developer merasakan keindahan Lumina!

---

<div align="center">

Dibuat dengan dedikasi dan cinta ❤️ oleh **Slamet Sugandi** dan seluruh **Lumina Framework Core Team & Contributors**.

<sub>Copyright &copy; 2026 Lumina Java Ecosystem. Dirilis di bawah lisensi terbuka [MIT](LICENSE).</sub>

</div>

