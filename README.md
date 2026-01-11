# Kremna Chatbot Platformu

Kremna, şirketlerin kendi müşteri temsilcisi karakterlerini kolayca oluşturup web sitelerine entegre edebileceği, modern ve esnek bir chatbot altyapısı sunar.

## 🚀 Özellikler
- Hızlı ve kolay agent (karakter) oluşturma
- Python + FastAPI ile geliştirildi
- Google Gemini API ile güçlü yapay zeka desteği
- SQLite (lokal) ve PostgreSQL (production) desteği
- Docker ile her ortamda kolay kurulum
- REST API ile kolay entegrasyon
- Web arayüzü ve dashboard desteği (geliştirilebilir)

## 🔧 Kurulum

### 1. Klonla
```bash
git clone https://github.com/kullaniciadi/kremna.git
cd kremna
```

### 2. .env Dosyasını Oluştur
```
GEMINI_API_KEY=buraya_gemini_api_key
DATABASE_URL=
PORT=8080
```

### 3. Docker ile Çalıştır
```bash
docker build -t kremna .
docker run -d -p 8080:8080 --env-file .env --name kremna-app kremna
```

### 4. Lokal Çalıştırmak için (Python)
```bash
pip install -r requirements.txt
cd main
uvicorn main_receiver:app --host 0.0.0.0 --port 8080
```

## 🧑‍💻 API Kullanımı

### Agent Oluşturma
```bash
curl -X POST "http://localhost:8080/agent_config" \
  -H "Content-Type: application/json" \
  -d '{
    "agentId": "trendyol_asistan",
    "persona_title": "Trendyol Müşteri Destek Asistanı",
    "model_instructions": {
      "tone": "Samimi, hızlı ve çözüm odaklı",
      "rules": [
        "Türkçe cevap ver",
        "Sipariş, iade ve kargo konularında yardımcı ol",
        "Kampanya ve indirimler hakkında bilgi ver"
      ],
      "prohibited_topics": [
        "Rakip firmalar hakkında yorum",
        "Kredi kartı bilgisi isteme"
      ]
    },
    "initial_context": {
      "company": "Trendyol",
      "contact_phone": "0 850 258 58 58",
      "working_hours": "7/24 Destek"
    }
  }'
```

### Chat Endpoint
```bash
curl -X POST "http://localhost:8080/chat" \
  -H "Content-Type: application/json" \
  -d '{
    "agent_id": "trendyol_asistan",
    "session_id": "user_001",
    "user_message": "Siparişim ne zaman gelir?"
  }'
```

### Tüm Agentları Listele
```bash
curl http://localhost:8080/agents
```

## 📦 Dosya ile Soru Sorma
```bash
curl -X POST "http://localhost:8080/chat_file" \
  -F "file=@sorular.txt" \
  -F "agent_id=trendyol_asistan" \
  -F "session_id=user_001"
```

## 👥 Katkıda Bulunanlar
- Ahmet (Backend, DevOps)
- Melike (DevOps, QA)
- ...

## 📝 Lisans
MIT

---

Daha fazla bilgi ve örnekler için [ENDPOINTS_GUIDE.md](ENDPOINTS_GUIDE.md) dosyasına bakabilirsiniz.
