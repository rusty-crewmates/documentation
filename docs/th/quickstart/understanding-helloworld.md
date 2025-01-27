# อธิบาย Hello World

ใน [คู่มือเริ่มต้นฉบับย่อของ Hello World](helloworld-localhost.md) เราได้สาธิตวิธีการคำสั่งง่ายๆ เพื่อได้ให้เห็นตัวอย่างของการใช้งาน สิ่งนี้จะช่วยให้คุณมั่นใจได้ว่าคุณเตรียมการได้พร้อม และสามารถรัน query อย่างง่ายเพื่อได้รับข้อมูลจาก SubQuery ในที่นี้ เราจะลงรายละเอียดมากขึ้นว่าแต่ละคำสั่งเหล่านั้นมีความหมายว่าอย่างไร

## subql init

คำสั่งแรกที่เราเรียกใช้คือ `subql init subqlHelloWorld`

สิ่งนี้ช่วยจัดการงานส่วนที่ยาก และสร้างไฟล์ทั้งหมดให้คุณ ตามที่ระบุไว้ใน [เอกสารทางการ](quickstart.md#configure-and-build-the-starter-project) คุณจะต้องทำงานกับไฟล์ต่อไปนี้เป็นหลัก:

- Manifest ใน `project.yaml`
- GraphQL Schema ใน `schema.graphql`
- Mapping functions ในไดเรกทอรี `src/mappings/`

![key subql files](/assets/img/main_subql_files.png)

ไฟล์เหล่านี้เป็นส่วนหลักที่เราจะใช้งาน ดังนั้น เราจะเจาะลึกเนื้อหาของไฟล์เหล่านั้นมากขึ้นในบทความถัดๆไป ในตอนนี้ ให้ผู้ใช้ทำความเข้าใจว่า schema ประกอบด้วยคำอธิบายของข้อมูลที่ผู้ใช้สามารถ request ได้จาก SubQuery API, ไฟล์ yaml ของโครงการซึ่งมีพารามิเตอร์ประเภท "configuration" และแน่นอนว่ามี mappingHandlers ที่มี typescript ซึ่งมีฟังก์ชันสำหรับแปลงข้อมูล

## yarn install

สิ่งต่อไปที่เราทำคือ `yarn install` `npm install` ก็สามารถใช้ได้เช่นกัน

> สรุปที่มาสั้นๆ Node Package Manager หรือ npm เปิดตัวครั้งแรกในปี 2010 และเป็นตัวจัดการแพ็คเกจที่ได้รับความนิยมอย่างมากในหมู่นักพัฒนา JavaScript ซี่งเป็นแพ็คเกจเริ่มต้นที่ติดตั้งโดยอัตโนมัติทุกครั้งที่คุณติดตั้ง Node.js บนระบบของคุณ Yarn เปิดตัวครั้งแรกโดย Facebook ในปี 2559 โดยมีจุดประสงค์เพื่อแก้ไขข้อบกพร่องด้านประสิทธิภาพและความปลอดภัยบางประการในการทำงานกับ npm (ในขณะนั้น)

สิ่งที่ yarn ทำคือดูที่ไฟล์ `package.json` และดาวน์โหลด dependencies อื่นๆ เมื่อดูที่ไฟล์ `package.json` ดูเหมือนว่าจะไม่ได้มี dependencies มากนัก แต่เมื่อคุณเรียกใช้คำสั่ง คุณจะสังเกตเห็นว่ามีการเพิ่มไฟล์เข้ามา 18,983 ไฟล์ เนื่องจากแต่ละ dependency จะมี dependencies ของตนเองด้วย

![key subql files](/assets/img/dependencies.png)

## yarn codegen

จากนั้นเราก็รัน `yarn codegen` หรือ `npm run-script codegen` สิ่งนี้เป็นการดึง schema ของ GraphQL (ใน `schema.graphql`) และสร้างไฟล์โมเดล typescript ที่เกี่ยวข้องขึ้นมา (ดังนั้นไฟล์ที่ได้รับจะเป็นสกุล .ts) คุณไม่ควรเปลี่ยนไฟล์ที่สร้างขึ้นเหล่านี้ แต่ควรเปลี่ยนที่ไฟล์ต้นทาง `schema.graphql` แทน

![key subql files](/assets/img/typescript.png)

## yarn build

จากนั้นรันคำสั่ง `yarn build` หรือ `npm run-script build` สิ่งนี้น่าจะเรื่องที่คุ้นเคยสำหรับโปรแกรมเมอร์ที่มีประสบการณ์ โดยจะเป็นการสร้างโฟลเดอร์แบบกระจาย (distribution folder) สำหรับทำสิ่งต่างๆ เช่นการเพิ่มประสิทธิภาพโค้ดที่เตรียมสำหรับการ deploy

![key subql files](/assets/img/distribution_folder.png)

## docker-compose

ขั้นตอนสุดท้ายคือการรวมคำสั่ง docker `docker-compose pull && docker-compose up` (สามารถเรียกใช้แยกกันได้) คำสั่ง `pull` จะดึงอิมเมจที่จำเป็นทั้งหมดจาก Docker Hub และคำสั่ง `up` จะเริ่มต้นการทำงานของคอนเทนเนอร์

```shell
> docker-compose pull
Pulling postgres        ... done
Pulling subquery-node   ... done
Pulling graphql-engine  ... done
```

เมื่อคอนเทนเนอร์เริ่มทำงาน คุณจะเห็นเทอร์มินัลแสดงข้อความจำนวนมากที่แสดงสถานะของโหนดและ GraphQL engine และเมื่อคุณเห็น:

```
subquery-node_1   | 2021-06-06T02:04:25.490Z <fetch> INFO fetch block [1, 100]
```

เป็นการบอกให้คุณรู้ว่าโหนด SubQuery ได้เริ่มการซิงโครไนซ์แล้ว

## สรุป

เมื่อคุณได้ทราบข้อมูลเชิงลึกเกี่ยวกับสิ่งที่เกิดขึ้นเบื้องหลังแล้ว คำถามก็คือ จะต้องดูที่ไหนต่อ? หากคุณรู้สึกมั่นใจ คุณสามารถเรียนรู้เกี่ยวกับวิธีการ[สร้างโปรเจกต์](../create/introduction.md)และเรียนรู้เพิ่มเติมเกี่ยวกับไฟล์หลักทั้งสามไฟล์ นั่นคือ ไฟล์ manifest, the GraphQL schema, และ ไฟล์ the mappings

นอกจากนี้ สามารถไปที่บทช่วยสอนของเรา ซึ่งจะดูว่าเราสามารถเรียกใช้ตัวอย่าง Hello World นี้บนโครงสร้างพื้นฐานที่โฮสต์บน SubQuery ได้อย่างไร เราจะดูการแก้ไขบล็อกเริ่มต้น และจะเจาะลึกถึงการรันโปรเจกต์ SubQuery โดยเรียกใช้จากสิ่งที่พร้อมใช้งาน และโปรเจกต์โอเพ่นซอร์สต่างๆ
