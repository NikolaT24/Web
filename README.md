<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:6a11cb,100:2575fc&height=200&section=header&text=Greeting%20Card%20Email%20Sender&fontSize=30&fontColor=ffffff&animation=fadeIn" />
</p>
<div align="center">
   
# Greeting‑Card Email Sender

A simple web app (front‑end only) that lets you **design custom greeting cards right in the browser and send them as PNG attachments via e‑mail**—either one at a time or in bulk from a CSV file.

---

## ✨ Features

| Page                                   | What you can do                                                                                                                                                           |
| -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [`create‑card.html`](create-card.html) | ✒️ Design a card (text, fonts, stickers, background, size) · 📥 Download as PNG · 📧 Send a single e‑mail · 💾 Export that card as a **1‑row CSV preset**                 |
| [`bulk‑send.html`](bulk-send.html)     | 📂 Import a **CSV** with many recipients · 👀 Preview + paginate · 🎨 Pick one of three ready templates · 📊 Track a live progress‑bar while cards are generated & mailed |
| [`homepage.html`](homepage.html)       | Simple landing page that links to the above                                                                                                                               |

Additional folders:

```
img/         # logos, stickers, decoration PNGs
templates/   # 3 static JPEG templates for the bulk sender
vendor/      # Composer‑installed libs (PHPMailer)
```

---

## 🛠️ Prerequisites

| Software                        | Tested version                                 |
| ------------------------------- | ---------------------------------------------- |
| **XAMPP** (Windows)             | 8.2.12 (PHP 8.2, Apache 2.4.58, OpenSSL 3.1.3) |
| **Composer**                    | 2.7+ (for PHPMailer)                           |
| A mailbox you can SMTP‑login to | *Example: Gmail with an **App password***      |

### PHP extensions that must be **enabled** in `php.ini`

* `openssl`
* `mbstring`

---

## 🚀 Quick Start (Windows + XAMPP)

1. **Clone / copy** this folder into `C:\xampp\htdocs\cards` (or any sub‑folder).
2. Open a terminal **inside that folder** and run:

   ```bash
   composer install      # pulls PHPMailer
   ```
3. Edit **`send-card.php`** *and* **`send_card_email.php`** – fill in your SMTP server, username & password.

   ```php
   $mail->Host       = 'smtp.gmail.com';
   $mail->Username   = 'myaddress@gmail.com';
   $mail->Password   = 'XXXXXXXXXXXX';   // 16‑char app password
   $mail->SMTPSecure = PHPMailer::ENCRYPTION_STARTTLS;
   $mail->Port       = 587;
   ```
4. In the XAMPP Control Panel **start Apache** (MySQL can stay off).
5. Open [http://localhost/cards/](http://localhost/cards/) – you should see the home page.
6. Test‑drive:

   * Single send → *Create a card* → *📧 Изпрати*
   * Bulk send → *Масово изпращане* → upload **`example.csv`** → go through the 3 steps → *Изпрати всички картички*

---

## 📝 CSV format

The bulk sender expects **UTF‑8 CSV** where the *first* row is exactly:

```csv
име,имейл,пожелание
```

Each following row → one recipient:

| Column      | Required | Example                                       |
| ----------- | -------- | --------------------------------------------- |
| `име`       | ✔        | Петър Иванов                                  |
| `имейл`     | ✔        | [peter@example.com](mailto:peter@example.com) |
| `пожелание` | ✔        | Честит рожден ден!                            |

> Use a semicolon `;` as the locale decimal separator? Don’t – stick to comma `,`.

A sample file is provided in **`example.csv`**.

---

## 📑 Endpoints / APIs

| Script                | Consumed by       | Expects JSON                          | Purpose                                       |
| --------------------- | ----------------- | ------------------------------------- | --------------------------------------------- |
| `send-card.php`       | `card-builder.js` | `{to, subject, fileName, mime, data}` | Sends **one** card (PNG base64) as attachment |
| `send_card_email.php` | `bulk-send.js`    | `{email, name, image}`                | Sends a card in the bulk loop                 |

Both scripts rely on *PHPMailer* and output a tiny JSON response:

```json
{"ok": true}
```

or an error message with HTTP status `400 / 500`.

---

## 📜 License

MIT – do whatever you like, just keep the copyright notice.

> © 2025 – Greeting Card Email Sender Team

```
