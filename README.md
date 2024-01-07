# การสร้าง API & Deploy on website [Render.com](https://dashboard.render.com/)
### สร้างทดสอบบนเครื่อง ก่อนส่งขึ้น github repo [ที่มาของข้อมูล](https://chrisdevcode.hashnode.dev/how-to-create-and-deploy-a-json-server)
- ขั้นตอนแรกสร้างโฟล์เดอร์เก็บตัว API
- ทำการ ติดตั้ง NodeJS, Json-Server, Cors and Nodemon
  ``` bash
  npm init -y
  ```
  ``` bash
  npm install json-server json-serve cors
  ```
  ``` bash
  npm install -D nodemon
  ```
- จากนั้นสร้างไฟล์ ```index.js``` .
  
- นำ code เข้าไปวาง
  ``` javascript
  const jsonServer = require('json-server')
  const cors = require('cors')
  const path = require('path')
  
  const server = jsonServer.create()
  const router = jsonServer.router(path.join(__dirname, 'db.json'))
  const middlewares = jsonServer.defaults()
  
  server.use(cors())
  server.use(jsonServer.bodyParser)
  server.use(middlewares)
  server.use(router)
  
  const PORT = 8000
  
  server.listen(PORT, () => {
    console.log(`JSON Server is running on http://localhost:${PORT}`)
  })
  ```
- จากนั้นสร้างไฟล์ ```db.json```. เพื่อเก็บข้อมูล **API** เรา
  ``` json
  {
    "todos": [
      {
        "todo": "Do something nice for someone I care about",
        "completed": false,
        "userId": 1,
        "id": 1
      },
      {
        "todo": "Memorize the fifty states and their capitals",
        "completed": false,
        "userId": 1,
        "id": 2
      },
      {
        "todo": "Watch a classic movie",
        "completed": true,
        "userId": 1,
        "id": 3
      },
      {
        "todo": "Contribute code or a monetary donation to an open-source software project",
        "completed": false,
        "userId": 1,
        "id": 4
      },
      {
        "todo": "Solve a Rubik's cube",
        "completed": true,
        "userId": 1,
        "id": 5
      }
    ]
  }
  ```
- จากนั้นไปที่ไฟล์ ```package.json``` แล้วไปแก้ไขตรง ```"scripts"```
  ``` json
  "scripts": {
    "start": "node index.js",
    "dev": "nodemon index.js"
  },
  ```
- ### วิธีทดสอบ
  ``` bash
  npm run start
  ```

## ถ้า Error : Module JSON-SERVER
- ลองตรวจสอบที่ไฟล์ ```package.json``` ว่าข้างในเป็นแบบนี้มัย
  ```json
      "json-server": "^1.0.0-alpha.11"
  ```
- ถ้าใช่ ให้เปลี่ยนเป็น
  ```json
      "json-server": "^0.17.4"
  ```
- แล้วสั่ง
  ``` bash
  npm install json-server
  ```
- แล้วลอง
  ``` bash
  npm run start
  ```

  หวังว่าจะไม่เจอ Error อะไร สาธุ...!

## Upload to Github

### ในการอัพ **git** มันมีหลายวิธีแต่ ณ จุดนี้ขอยกตัวอย่างเป็นผ่าน **terminal**

``` bash
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/myUsers/NameRepo.git
git push -u origin main
```

## Upload to Render

### เข้าไปที่เว็บ **[render.com](https://dashboard.render.com/)**
- คลิก **New +**
  
![image](https://lh3.googleusercontent.com/u/0/drive-viewer/AEYmBYTI3cdCtr4P5dL40ZcRZJ5Q5xvvSuiTjsX1vLHnCbUai6G1wz_u8Ppjsol4sF4XZxXv9_37kAMLJwL3EYyn32ZblOiE4A=w1177-h970)

- เลือก Web Service

![image](https://lh3.googleusercontent.com/u/0/drive-viewer/AEYmBYT4FsSvskRfFih8bgjkzFnj0p5pT63d7NfjeEYeK3_BL-3C9MWorKjx-JsglF4PGyEapdmVWNnQ5TlR3dKntEjqoe_e-Q=w1177-h970)

- เลือก **Build and deploy from a Git repository** แล้วกด **Next**

![image](https://lh3.googleusercontent.com/u/0/drive-viewer/AEYmBYRutjCTwM2nZ6NUA_huRb6NdIlIRq37ntdmN3VW8YWWbzaK4HfDyrkREAcL6H5rfRk88JbfFmk7pNQYhwiJnATfXZ1mPQ=w1177-h970)

- เลือก **Repo** ตัวที่เราสร้างไว้ใน git แล้วกด **Connect**

![image](https://lh3.googleusercontent.com/u/0/drive-viewer/AEYmBYSctnoZqsUrTbe2ho5t6vtE9FDV9vAzxofWqR7n6MXNFGUVjW8SNJEo8A10Kj3rTixmgHNarndrNA2aNLaajvWW4aBf=w1177-h970)

- ตรง **Start Command** ให้เราพิมพ์ ``` node index.js  ```

![image](https://lh3.googleusercontent.com/u/0/drive-viewer/AEYmBYS9e4CPCeMY07T-Usb8MOKl6gtvq_mPvMAg1c9Xo6gL2gAg0iD0GlGg7QFUik39NcgSwpxSo9WOrF0Sh-erTD0JKymaKQ=w1177-h970)

- จากนั้นกด Create Web Service ได้เลย

![image](https://lh3.googleusercontent.com/u/0/drive-viewer/AEYmBYTmK44Ly_F6-4yiYpKxFi9b6hzO5ptMhGAg8htCL9-8eQV96vB7eHLic_2mYBvtOe86DInOOBjoZZ8hvtDtCU2ttlbjow=w1177-h970)

- เสร็จแล้วเราจะได้ ``` url ``` มาเป็นอันใช้งานได้ (รอ deploy เสร็จก่อนค่อยนำไปใช้งาน)

![image](https://lh3.googleusercontent.com/u/0/drive-viewer/AEYmBYSUnZS652nTf_Y73YOJmbvY6KAGpLMnSudsUdg0VIrvTTpLlhnz9Wudmb0NzcPgjvYr8xLbwaJ1rPLcPs-pwUXoGIn_OQ=w1177-h970)
