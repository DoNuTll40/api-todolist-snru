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
