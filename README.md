# การสร้าง API & Deploy on website [Render.com](https://dashboard.render.com/)
### สร้างทดสอบบนเครื่อง ก่อนส่งขึ้น github repo
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
    "api": "node index.js",
    "dev": "nodemon index.js"
  },
  ```
- ### วิธีทดสอบ
  ``` bash
  npm run api
  ```
## Upload to git

- เข้าไปที่เว็บ **[render.com](https://dashboard.render.com/)**

  
![image](data:image/png;base64,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)
