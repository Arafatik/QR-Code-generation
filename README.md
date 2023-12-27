# QR-Code-generation
# Creation REST API on Node.js and Express to generate QR-code for any link

## STEP 1. Create a new npm project
```
mkdir qr-api
cd qr-api
npm init -y
```

## STEP 2. Installing express and qrcode
```
npm install express qrcode
```

## STEP 3. API Code
```
const express = require("express");
const QRcode = require("qrcode");

const app = express();
const PORT = 3000;

app.get("/generate", async (req, res) => {
  const url = req.query.url;

  if (!url) {
    return res.status(400).send("URL не указан.");
  }

  try {
    const qr = await QRcode.toDataURL(url);
    res.send(`<img src="${qr}" />`);
  } catch (err) {
    res.status(500).send("Ошибка при создании QR-кода.");
  }
});

app.listen(PORT, () => {
  console.log(`Сервер запущен по адресу http://localhost:${PORT}`);
});
```

## STEP 4. Starting the server
```
node index.js
```

## STEP 5. Checking that everything is working

![image](https://github.com/Arafatik/QR-Code-generation/assets/94862857/07075da9-5270-4de6-abee-5665811ef527)
