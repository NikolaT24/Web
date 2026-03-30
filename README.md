<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:ff512f,50:dd2476,100:6a11cb&height=220&section=header&text=Greeting%20Card%20Email%20Sender&fontSize=42&fontAlignY=35&fontColor=ffffff&animation=fadeIn&desc=Design%20%E2%80%A2%20Export%20%E2%80%A2%20Send&descAlignY=55&descSize=18" />
</p>

<div align="center">

<img src="https://readme-typing-svg.herokuapp.com?font=JetBrains+Mono&size=22&duration=3000&color=FF6EC7&center=true&vCenter=true&width=600&lines=Design+Beautiful+Greeting+Cards;Send+Them+via+Email+in+Seconds;Single+or+Bulk+Sending+with+CSV" />

<br><br>

<img src="https://img.shields.io/badge/Frontend-Web%20App-6a11cb?style=for-the-badge">
<img src="https://img.shields.io/badge/Export-PNG-blue?style=for-the-badge">
<img src="https://img.shields.io/badge/Emails-Automated-ff69b4?style=for-the-badge">

<br><br>

<h3>💌 Create, personalize, and send greeting cards effortlessly</h3>

<p>
A simple <b>front-end web app</b> that lets you design custom greeting cards directly in your browser  
and send them as <b>PNG email attachments</b> — whether individually or in bulk using CSV.
</p>

</div>

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
