# Backend Setup Instructions
### 1. Clone the backend repo
```
git clone https://github.com/Korrawit-aoongern/backend-cw
cd backend-cw
npm install
```

### 2. Create new D1 database
```
npx wrangler d1 create my_db
```

- Would you like Wrangler to add on your behalf? (Y/n) -> Y (เพิ่มให้อัตโนมัติในสเต็ปต่อไป)
- What binding name would you like to use? -> my_db
- For local dev.. -> N

output:
```
🌀 Creating database...
✅ Database created!

database_name = "my_db"
database_id   = "abcd1234-ef56-7890-aaaa-bbbbccccdddd"
```


### 3. Go to wrangler.jsonc
```
"d1_databases": [
  {
    "binding": "my_db",
    "database_name": "my_db",
    "database_id": "PASTE-YOUR-OWN-ID-HERE"
  }
]
```

ต้อง "binding": "my_db" เท่านั้น
ส่วน "database_name": เป็นชื่ออะไรก็ได้

### 4. Run the migrations

```
npx wrangler d1 execute my_db --file=./src/schema.sql --remote
```

### 5. Start the development server
```
npx wrangler dev
```

### 6. Deploy
```
npx wrangler deploy
```

Wrangler will output:
```
https://backend-cw.username.workers.dev
```
นั่นคือ URL ของ backend ของคุณ
สำหรับเชื่อมต่อกับ frontend ในการรัน
```
docker run -p 8080:80 -e API_BASE=https://backend-cw.username.workers.dev yuzuruorensu/cw-crud:v1f
```
