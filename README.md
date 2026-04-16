# NERVHQ — MAGI

## MAGI Multi-Agent General Intelligence (Triple AI System)

---

## Ollama’yı CORS Açık Başlatma

```bash
OLLAMA_ORIGINS=* ollama serve
```

---

## Modeli Çekme

```bash
ollama pull qwen2.5-coder:7b
```

---

## Arch Linux / systemd Yapılandırması

Arch Linux’ta Ollama genelde bir systemd servisi olarak çalışır. Bu yüzden `OLLAMA_ORIGINS` değişkenini servis seviyesinde tanımlamak gerekir.

### 1. Servis Override Dosyasını Aç

```bash
sudo systemctl edit ollama.service
```

### 2. Ortam Değişkenini Tanımla

Açılan dosyaya şunu ekle:

```ini
[Service]
Environment="OLLAMA_ORIGINS=*"
```

### 3. Değişiklikleri Uygula

```bash
sudo systemctl daemon-reload
sudo systemctl restart ollama
```

---

## Doğrulama

### Environment değişkenini kontrol et:

```bash
systemctl show ollama.service --property=Environment
```

Beklenen çıktı:

```bash
Environment=OLLAMA_ORIGINS=*
```

### Servis dosyasını ve override’ı birlikte görüntüle:

```bash
systemctl cat ollama.service
```

### Hata ayıklama (loglar):

```bash
journalctl -u ollama -b
```

---

## Not

Eğer servis user-level çalışıyorsa:

```bash
systemctl --user edit ollama.service
systemctl --user restart ollama
```
