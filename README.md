# 🔳 GEN QR — Advanced QR Code Generator

An advanced Python-based QR Code Generator that allows users to generate **Website QR Codes and UPI Payment QR Codes**, preview and download QR images, and manage QR generation history through an interactive Jupyter Notebook dashboard.

## ✨ Features

- 🌐 **Website QR Generator** — Generate QR codes for valid website URLs.
- 💳 **UPI Payment QR Generator** — Create UPI payment QR codes with an optional payee name, amount, and payment note.
- 🖼️ **QR Code Preview** — View generated QR codes directly inside the Jupyter Notebook.
- 💾 **PNG Image Export** — Save QR codes as PNG images.
- 🗃️ **QR History Management** — Store and retrieve previously generated QR codes.
- 🗑️ **Delete QR Records** — Delete history records and their associated images.
- ⚡ **Flask REST API** — Access QR generation and history features through API endpoints.
- 🛡️ **Input Validation** — Validate website URLs, UPI IDs, and payment amounts.
- 📊 **Interactive Dashboard** — Use Jupyter widgets to generate and manage QR codes without manually calling API endpoints.

## 🛠️ Tech Stack

| Technology | Purpose |
|---|---|
| Python | Core programming language |
| Flask | REST API development |
| SQLite | Store QR generation history |
| qrcode | QR code generation |
| Pillow | QR image processing |
| IPyWidgets | Interactive notebook dashboard |
| Requests | API communication |
| Jupyter Notebook | Development and user interface |

## 📁 Project Structure

```text
GEN_QR/
│
├── Gen_QR.ipynb          # Main project notebook
│
└── GEN_QR_Project/       # Created automatically at runtime
    ├── gen_qr.db         # SQLite database
    └── qr_images/        # Generated QR code PNG files
```

The application creates the project directory, database, and image folder automatically in your home directory when the notebook runs.

## ⚙️ Installation & Setup

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/GEN_QR.git
cd GEN_QR
```

Replace `YOUR_USERNAME` with your GitHub username.

### 2. Install the required libraries

Run this command in your terminal or Anaconda environment:

```bash
pip install Flask "qrcode[pil]" Pillow requests ipywidgets
```

### 3. Launch Jupyter Notebook

```bash
jupyter notebook
```

Open `Gen_QR.ipynb` and run the notebook cells in order.

### 4. Start the application

The notebook initializes the SQLite database, starts the Flask server on `http://127.0.0.1:5000`, and displays the interactive dashboard.

**Note:** Run the server-start cell only once per kernel session.

## 🚀 How to Use

### Generate a Website QR Code

1. Select **Website QR** from the dashboard.
2. Enter a valid URL, such as `https://example.com`.
3. Enter a label for the QR code.
4. Click **Generate QR**.
5. Preview the QR code and check its saved file location.

### Generate a UPI Payment QR Code

1. Select **UPI Payment QR**.
2. Enter a valid UPI ID, such as `name@bank`.
3. Optionally enter the payee name, payment amount in INR, and payment note.
4. Click **Generate QR**.
5. Scan the QR code with a compatible UPI app and verify the recipient and amount before paying.

**Important:** Generating a UPI QR code does not verify the recipient's account or process a payment.

### Manage QR History

- Click **Refresh History** to view previously generated QR codes.
- Enter a history ID and click **Delete Record** to delete the record and its saved image.
- Download generated QR images using the provided download API endpoint.

## 🔌 API Endpoints

The project provides the following Flask API endpoints:

| Method | Endpoint | Description |
|---|---|---|
| GET | `/` | Project status and available endpoints |
| GET | `/api/health` | Check server health |
| POST | `/api/qr/url` | Generate a website QR code |
| POST | `/api/qr/upi` | Generate a UPI payment QR code |
| GET | `/api/history` | Retrieve the latest 100 QR history records |
| GET | `/api/qr/<record_id>/download` | Download a QR image |
| DELETE | `/api/history/<record_id>` | Delete a history record and its image |

### Example: Generate a Website QR

**POST** `/api/qr/url`

```json
{
  "url": "https://example.com",
  "label": "My Website"
}
```

A successful request returns HTTP status `201` with the generated QR code's metadata.

### Example: Generate a UPI QR

**POST** `/api/qr/upi`

```json
{
  "upi_id": "name@bank",
  "payee_name": "Example User",
  "amount": "100",
  "note": "Test Payment"
}
```

The amount and optional fields can be adjusted according to the intended payment details.

## 🗄️ Database

The application uses SQLite to maintain a `qr_history` table containing:

- `id` — Unique record identifier
- `qr_type` — QR category (`url` or `upi`)
- `label` — QR code label
- `payload` — Encoded URL or UPI payment string
- `filename` — Saved PNG filename
- `created_at` — Record creation timestamp

## 🔒 Notes & Limitations

- The Flask server is configured to run locally on `127.0.0.1:5000`.
- Generated QR images are saved locally in PNG format.
- The history API returns up to 100 recent records.
- UPI QR generation does not confirm payment completion.
- The notebook uses local storage, so generated images and database records remain on the machine unless manually shared or backed up.

## 🔮 Future Improvements

- 🎨 Custom QR colors, logos, and styling
- 📱 QR codes for Wi-Fi, contact cards, email, and phone numbers
- 🌐 Web-based interface using HTML, CSS, and JavaScript
- 📈 QR generation analytics and usage statistics
- 📦 Bulk QR code generation
- ☁️ Cloud database and deployment support
- 🔐 Authentication and access control

## 👨‍💻 Author

**Your Name**

GitHub: [YOUR_USERNAME](https://github.com/YOUR_USERNAME)

---

⭐ If you find this project useful, consider giving the repository a star!

*Built with Python, Flask, SQLite, and QR Code technology.*
