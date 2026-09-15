# Cara jalanin dashboard ini di local (Antigravity / VS Code / terminal biasa)

## 1. Struktur folder
Taruh semua ini dalam SATU folder yang sama:

```
folder-kamu/
├── dashboard.py
├── 11_aspect_best_multitask_model_2.pt   <-- file model kamu, RENAME persis ini
├── logo_rsmc.jpg   (atau logo_rsmc.png)  <-- opsional, kalau nggak ada tetap jalan (pakai emoji 🏥)
└── requirements.txt
```

Nama file model **harus** persis `11_aspect_best_multitask_model_2.pt` karena itu yang di-hardcode di `load_model()`. Kalau nama file model kamu beda, tinggal ganti baris ini di `dashboard.py`:

```python
model.load_state_dict(torch.load('11_aspect_best_multitask_model_2.pt', map_location=device))
```
ganti jadi path/nama file kamu.

## 2. Install dependencies
Buka terminal di folder itu (di Antigravity bisa langsung integrated terminal), lalu:

```bash
python -m venv venv
# aktifkan venv:
# Windows:
venv\Scripts\activate
# Mac/Linux:
source venv/bin/activate

pip install -r requirements.txt
```

Kalau punya GPU NVIDIA dan mau pakai CUDA, install torch versi CUDA dulu sebelum yang lain (cek link resmi pytorch.org sesuai versi CUDA kamu), baru install sisanya.

## 3. Jalankan
Tidak perlu ngrok kalau cuma diakses di komputer sendiri — ngrok itu cuma dipakai di Colab supaya bisa diakses dari luar. Local tinggal:

```bash
streamlit run dashboard.py
```

Nanti otomatis kebuka browser ke `http://localhost:8501`. Kalau nggak kebuka otomatis, buka manual link itu.

## 4. Kalau mau tetap pakai ngrok (misal mau share ke orang lain di luar jaringan)
Baru optional install `pyngrok`, lalu jalankan `ngrok authtoken <token_kamu>` sekali di terminal, tapi ini nggak wajib buat akses local.

## Yang beda dari versi Colab
- Nggak ada lagi `drive.mount`, `shutil.copy` dari Drive — filenya langsung dibaca dari folder lokal.
- Nggak ada `!pip install` (magic command Colab) — pakai `requirements.txt` + `pip install` biasa.
- Nggak ada ngrok tunnel — akses langsung via `localhost:8501`.
- Isi `dashboard.py` sendiri (logic streamlit-nya) sama persis, cuma dipisah jadi file `.py` beneran, bukan string di dalam notebook.
