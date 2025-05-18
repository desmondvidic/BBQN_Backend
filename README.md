# FastAPI Knowledge Base Query API

This project is a lightweight and efficient FastAPI-based API to query a structured knowledge base (stored as JSON) using fuzzy text matching. It supports city and location-based filtering, token counting, and truncation for integration with token-limited environments like Retell.

---

## 🔧 Features

- Query knowledge base using `city`, `location`, and `query`.
- Fuzzy matching using RapidFuzz.
- Token count limiter (up to 800 tokens).
- Supports fallback truncation if tokens exceed the limit.
- Easy integration with Postman or Replit.

---

## 📁 Project Structure

```
.
├── main.py                  # FastAPI app
├── app/
│   ├── __init__.py
│   ├── utils.py             # Core logic (fuzzy filter, tokenizer)
│   └── kb_store.json        # Your knowledge base (chunked JSON)
├── requirements.txt         # Python dependencies
```

---

## 📦 Installation

```bash
pip install -r requirements.txt
```

Dependencies include:
```
fastapi
uvicorn
pydantic
rapidfuzz
transformers
```
---

## 🚀 Running the API

```bash
uvicorn main:app --reload
```

---

## 📬 Example API Call

```bash
GET /kb/query?city=Delhi&query=starter&location=Indiranagar
```

**Returns:**
- `answer`: the relevant chunk from the KB.
- `tokens_used`: token count for the chunk.
- `has_more`: true if the chunk was truncated.

---

## 🧠 How It Works

- Uses RapidFuzz to match `query` against text content (`chunk`) with a default threshold of 65.
- Matches `location` against both `location` and `city` fields to avoid location mismatches.
- If tokens > 800, chunk is truncated by characters (3000 chars default).

---

## 🧪 Testing with Postman

Use the following URL structure locally:

```
http://127.0.0.1:8000/kb/query?city=Delhi&query=starter&location=Indiranagar
```

For Replit or deployment, replace with your hosted URL.

---

## 📝 Notes

- Ensure `kb_store.json` is clean, with fields: `city`, `location`, `category`, `chunk`.
- Use the `count_tokens` method from `utils.py` to calculate token usage with GPT2 tokenizer.

---

## 📃 License

MIT License
