# Design Patterns คืออะไร ? ? ?
การออกแบบแพทเทิร์นเป็นวิธีการแก้ปัญหาที่พบได้บ่อยในการออกแบบซอฟต์แวร์ เปรียบเสมือนแปลนที่เตรียมไว้ล่วงหน้าที่คุณสามารถปรับแต่งเพื่อแก้ไขปัญหาที่เกิดซ้ำในโค้ดของคุณ

คุณไม่สามารถค้นหาแพทเทิร์นแล้วนำไปใช้ในโปรแกรมของคุณได้ทันทีเหมือนกับฟังก์ชันหรือไลบรารีที่มีอยู่ แพทเทิร์นไม่ใช่โค้ดเฉพาะเจาะจง แต่เป็นแนวคิดทั่วไปในการแก้ปัญหาหนึ่ง ๆ คุณสามารถปฏิบัติตามรายละเอียดของแพทเทิร์นและนำไปปรับใช้ให้เหมาะสมกับสถานการณ์จริงของโปรแกรมของคุณ

Patterns ประกอบด้วยอะไรบ้าง?
ส่วนใหญ่แล้วแพทเทิร์นจะถูกอธิบายอย่างเป็นทางการเพื่อให้ผู้คนสามารถนำไปใช้ในบริบทต่าง ๆ ได้ นี่คือส่วนที่มักจะปรากฏในคำอธิบายของแพทเทิร์น:

- Intent of the pattern จะอธิบายปัญหาและวิธีแก้ไขอย่างสั้น ๆ
- Motivation จะอธิบายปัญหาและวิธีแก้ไขที่แพทเทิร์นสามารถทำได้อย่างละเอียดมากขึ้น
- Structure of classes จะแสดงแต่ละส่วนของแพทเทิร์นและความสัมพันธ์ระหว่างพวกมัน
- Code example ในหนึ่งในภาษาการเขียนโปรแกรมยอดนิยมจะช่วยให้เข้าใจแนวคิดที่อยู่เบื้องหลังแพทเทิร์นได้ง่ายขึ้น
 
## The Catalog of Design Patterns
- Creational patterns
  แพทเทิร์นการสร้างออบเจ็กต์ มีวิธีการสร้างออบเจ็กต์หลากหลายรูปแบบ ซึ่งช่วยเพิ่มความยืดหยุ่นและการนำโค้ดที่มีอยู่กลับมาใช้ใหม่ได้อย่างมีประสิทธิภาพ
- Structural patterns
  แพทเทิร์นโครงสร้าง แพทเทิร์นเหล่านี้อธิบายวิธีการประกอบออบเจ็กต์และคลาสเข้าด้วยกันเป็นโครงสร้างที่ใหญ่ขึ้น ในขณะเดียวกันก็ยังคงความยืดหยุ่นและประสิทธิภาพของโครงสร้างเหล่านี้ไว้
- Behavioral patterns
  แพทเทิร์นเชิงพฤติกรรม แพทเทิร์นเหล่านี้เกี่ยวข้องกับอัลกอริทึมและการกำหนดความรับผิดชอบระหว่างออบเจ็กต์ต่าง ๆ
