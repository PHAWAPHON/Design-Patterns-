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

### Creational Design Patterns ประกอบไปด้วย

- 1.Factory Method
  คือ รูปแบบ Factory Method กำหนด interface สำหรับการสร้าง Object แต่ให้ Class ย่อยเป็นผู้กำหนดประเภทของ Object ที่จะสร้าง รูปแบบนี้ช่วยเพิ่มความยืดหยุ่นให้กับระบบ ช่วยให้สามารถเปลี่ยนแปลงวิธีการสร้าง Object ได้โดยไม่ต้องแก้ไข code ของ Class ที่นำ 
  ไปใช้งาน
> Usage examples: แพทเทิร์น Factory Method ถูกใช้งานอย่างแพร่หลายในโค้ด Python มันมีประโยชน์มากเมื่อคุณต้องการให้โค้ดของคุณมีความยืดหยุ่นสูง

> Identification: วิธีการของ Factory สามารถระบุได้จากวิธีการสร้างที่สร้างออบเจ็กต์จากคลาสคอนกรีต ในขณะที่คลาสคอนกรีตถูกใช้ในระหว่างการสร้างออบเจ็กต์ ประเภทการคืนค่าของวิธีการ Factory มักจะถูกประกาศเป็นabstract classหรือinterface

- รูปแบบ Factory Method ประกอบด้วยองค์ประกอบต่อไปนี้

  1. Product Interface เป็น interface ที่กำหนด method ที่ต้องมีใน Object ที่ถูกสร้างขึ้นโดย Factory Method (โดยปกติของ OOP จะใช้เป็น abstract class)
 
  2. Concrete Products เป็น Class ที่สืบทอดมาจาก Product Interface และมีการเขียน method ที่ถูกกำหนดใน Product Interface
 
  3. Creator Class เป็น Class ที่มี method สร้าง Object (Factory Method) ซึ่งใช้สร้าง Object ตามประเภทที่ต้องการ

- ตัวอย่าง code
  
```python
from __future__ import annotations
from abc import ABC, abstractmethod


class Creator(ABC):
    """
    คลาส Creator ประกาศวิธีการ factory ที่มีหน้าที่คืนค่าออบเจ็กต์ของคลาส Product 
    โดยทั่วไปแล้วคลาสย่อยของ Creator จะเป็นผู้ให้การดำเนินการของวิธีการนี้
    """

    @abstractmethod
    def factory_method(self):
        """
        สังเกตว่า Creator อาจมีการให้การดำเนินการเริ่มต้นของวิธีการ factory ด้วย
        """
        pass

    def some_operation(self) -> str:
        """
        นอกจากนี้ แม้จะมีชื่อว่า Creator หน้าที่หลักของมันไม่ได้เป็นการสร้างผลิตภัณฑ์
        โดยทั่วไปแล้วมันจะมีตรรกะธุรกิจหลักที่พึ่งพาออบเจ็กต์ Product ที่คืนค่าจากวิธีการ factory
        คลาสย่อยสามารถเปลี่ยนตรรกะธุรกิจนี้โดยอ้อมด้วยการโอเวอร์ไรด์วิธีการ factory และคืนค่า
        ประเภทของผลิตภัณฑ์ที่แตกต่างออกไป
        """

        # เรียกวิธีการ factory เพื่อสร้างออบเจ็กต์ Product
        product = self.factory_method()

        # ตอนนี้ใช้ผลิตภัณฑ์
        result = f"Creator: โค้ดเดียวกันของ Creator ทำงานกับ {product.operation()}"

        return result


"""
Concrete Creators โอเวอร์ไรด์วิธีการ factory เพื่อเปลี่ยนประเภทของผลิตภัณฑ์ที่ได้
"""


class ConcreteCreator1(Creator):
    """
    สังเกตว่าลายเซ็นของวิธียังคงใช้ประเภทผลิตภัณฑ์นามธรรม แม้ว่าผลิตภัณฑ์คอนกรีตจะถูกคืนค่าจากวิธีการนี้
    ด้วยวิธีนี้ Creator สามารถคงความเป็นอิสระจากคลาสผลิตภัณฑ์คอนกรีตได้
    """

    def factory_method(self) -> Product:
        return ConcreteProduct1()


class ConcreteCreator2(Creator):
    def factory_method(self) -> Product:
        return ConcreteProduct2()


class Product(ABC):
    """
    อินเทอร์เฟซ Product ประกาศการดำเนินการที่ผลิตภัณฑ์คอนกรีตทั้งหมดต้องดำเนินการ
    """

    @abstractmethod
    def operation(self) -> str:
        pass


"""
Concrete Products ให้การดำเนินการหลากหลายของอินเทอร์เฟซ Product
"""


class ConcreteProduct1(Product):
    def operation(self) -> str:
        return "{ผลลัพธ์ของ ConcreteProduct1}"


class ConcreteProduct2(Product):
    def operation(self) -> str:
        return "{ผลลัพธ์ของ ConcreteProduct2}"


def client_code(creator: Creator) -> None:
    """
    โค้ดของลูกค้าทำงานกับอินสแตนซ์ของ Concrete Creator แม้ว่าผ่านทางอินเทอร์เฟซฐาน 
    ตราบใดที่ลูกค้ายังคงทำงานกับ Creator ผ่านทางอินเทอร์เฟซฐาน คุณสามารถส่งผ่านคลาสย่อยใด ๆ ของ Creator ก็ได้
    """

    print(f"Client: ฉันไม่รู้จักคลาสของ Creator แต่ยังทำงานได้\n"
          f"{creator.some_operation()}", end="")


if __name__ == "__main__":
    print("App: เริ่มต้นด้วย ConcreteCreator1.")
    client_code(ConcreteCreator1())
    print("\n")

    print("App: เริ่มต้นด้วย ConcreteCreator2.")
    client_code(ConcreteCreator2())
```
- Output
```python
App: Launched with the ConcreteCreator1.
Client: I'm not aware of the creator's class, but it still works.
Creator: The same creator's code has just worked with {Result of the ConcreteProduct1}

App: Launched with the ConcreteCreator2.
Client: I'm not aware of the creator's class, but it still works.
Creator: The same creator's code has just worked with {Result of the ConcreteProduct2}
```

- 2.Singleton
- องค์ประกอบ Singleton
  รูปแบบ Singleton รับประกันว่ามีเพียง instance เดียวของ class เท่านั้นในระบบ รูปแบบนี้มักใช้สำหรับ class ที่ต้องการจัดการทรัพยากรระบบทั่วไป หรือ class ที่ต้องการให้แน่ใจว่ามีสถานะที่สอดคล้องกันตลอดทั้งระบบ (เกิดขึ้นเพียงครั้งเดียวในระบบเท่านั้น)

- ตัวอย่าง code
```python
class SingletonMeta(type):
    """
    คลาส Singleton สามารถถูกนำมาใช้ในวิธีที่ต่างกันใน Python วิธีการบางอย่างที่เป็นไปได้คือ: 
    base class, decorator, metaclass เราจะใช้ metaclass เพราะเหมาะสมที่สุดสำหรับจุดประสงค์นี้
    """

    _instances = {}

    def __call__(cls, *args, **kwargs):
        """
        การเปลี่ยนแปลงที่อาจเกิดขึ้นกับค่า argument ของ `__init__` จะไม่ส่งผลต่อ
        อินสแตนซ์ที่คืนค่า
        """
        if cls not in cls._instances:
            instance = super().__call__(*args, **kwargs)
            cls._instances[cls] = instance
        return cls._instances[cls]


class Singleton(metaclass=SingletonMeta):
    def some_business_logic(self):
        """
        สุดท้าย singleton ควรกำหนด business logic บางอย่างที่สามารถ
        ถูกดำเนินการบนอินสแตนซ์ของมัน
        """

        # ...


if __name__ == "__main__":
   

    s1 = Singleton()
    s2 = Singleton()

    if id(s1) == id(s2):
        print("Singleton works, both variables contain the same instance.")
    else:
        print("Singleton failed, variables contain different instances.")
```

- Output
```python
Singleton works, both variables contain the same instance.
```
- 3. รูปแบบ Abstract Factory
- องค์ประกอบ Abstract Factory
  รูปแบบ Abstract Factory ขยายแนวคิดของ Factory Method ไปอีกขั้น ช่วยให้สามารถสร้างกลุ่มของ Object ที่เกี่ยวข้องกันโดยไม่ต้องระบุ Class ที่เป็นรูปธรรม (ไม่ต้องกำหนดว่า Class ทำงานยังไง) ก็สามารถสร้างเป็นกลุ่มสำหรับการใช้งานร่วมกันได้ รูปแบบนี้เหมาะสำหรับการสร้างระบบที่มี Object ที่เกี่ยวข้องกันจำนวนมาก (คือ ไม่เหมือนกัน แต่ผลลัพธ์ปลายทางการใช้งานเหมือนกัน)

-ความแตกต่างระหว่าง Abstract Factory และ Factory Method อยู่ที่ “ระดับของความสัมพันธ์” ในการสร้าง Object

- Factory Method เป็นรูปแบบที่ใช้สร้าง Object ของ Class เดียว โดยมี method ใน Class เดียวเป็นตัวกำหนดว่าจะสร้าง Object ประเภทใดออกมาใน Factory นั้น (ดังตัวอย่างที่เราเห็นในก่อนหน้านี้)
Abstract Factory เป็นรูปแบบที่ใช้สร้าง Object จากกลุ่มของ Class ที่เกี่ยวข้องกัน โดยมี method ที่ถูกกำหนดใน interface เพื่อสร้าง Object ในกลุ่มออกมา (เทียบได้กับการสร้างหลายๆ Factory มารวมไว้ Factory เดียวกัน แต่ Factory หลายๆ Factory นั้นยังเป็นประเภทเดียวกันอยู่ แต่สามารถสร้างจาก Abstract Factory ตัวเดียวออกมาได้)
รูปแบบ Abstract Factory เหมาะสำหรับการสร้างระบบที่ต้องการสร้างกลุ่มของ Object ที่เกี่ยวข้องกัน และมีความยืดหยุ่นในการเปลี่ยนแปลง Class ที่ใช้ในการสร้าง Object ได้

- รูปแบบ Abstract Factory ประกอบด้วยองค์ประกอบต่อไปนี้

- Abstract Factory เป็น interface ที่กำหนดวิธีสร้าง Object ในกลุ่มที่เกี่ยวข้องกันโดยใช้ method ตามประเภทของ Object
- Concrete Factory เป็น Class ที่สืบทอดมาจาก Abstract Factory และมีการสร้าง Object ในกลุ่มที่เกี่ยวข้อง
- Abstract Product เป็น interface ที่กำหนดวิธีการใช้งานของ Object ในกลุ่มที่เกี่ยวข้อง
- Concrete Product เป็น Class ที่สืบทอดมาจาก Abstract Product และมีการกำหนดวิธีการใช้งานของ Object ในกลุ่มที่เกี่ยวข้อง

- ตัวอย่าง code
```python
from __future__ import annotations
from abc import ABC, abstractmethod


class AbstractFactory(ABC):
    """
    อินเทอร์เฟซ Abstract Factory ประกาศชุดของเมธอดที่คืนค่าผลิตภัณฑ์นามธรรมที่แตกต่างกัน 
    ผลิตภัณฑ์เหล่านี้เรียกว่าครอบครัว (family) และมีความเกี่ยวข้องกันด้วยธีมหรือแนวคิดระดับสูง 
    ผลิตภัณฑ์ของครอบครัวหนึ่งมักสามารถทำงานร่วมกันได้ 
    ครอบครัวของผลิตภัณฑ์อาจมีหลายเวอร์ชัน แต่ผลิตภัณฑ์ของเวอร์ชันหนึ่งจะไม่สามารถใช้งานร่วมกับผลิตภัณฑ์ของเวอร์ชันอื่นได้
    """
    @abstractmethod
    def create_product_a(self) -> AbstractProductA:
        pass

    @abstractmethod
    def create_product_b(self) -> AbstractProductB:
        pass


class ConcreteFactory1(AbstractFactory):
    """
    Concrete Factories ผลิตครอบครัวของผลิตภัณฑ์ที่อยู่ในเวอร์ชันเดียวกัน
    โรงงานรับประกันว่าผลิตภัณฑ์ที่ได้จะสามารถใช้งานร่วมกันได้ 
    สังเกตว่าลายเซ็นของเมธอดใน Concrete Factory คืนค่าผลิตภัณฑ์นามธรรม 
    ในขณะที่ภายในเมธอดจะสร้างผลิตภัณฑ์คอนกรีต
    """

    def create_product_a(self) -> AbstractProductA:
        return ConcreteProductA1()

    def create_product_b(self) -> AbstractProductB:
        return ConcreteProductB1()


class ConcreteFactory2(AbstractFactory):
    """
    โรงงานคอนกรีตแต่ละแห่งมีผลิตภัณฑ์เวอร์ชันที่สอดคล้องกัน
    """

    def create_product_a(self) -> AbstractProductA:
        return ConcreteProductA2()

    def create_product_b(self) -> AbstractProductB:
        return ConcreteProductB2()


class AbstractProductA(ABC):
    """
    ผลิตภัณฑ์ที่แตกต่างกันของครอบครัวผลิตภัณฑ์ควรมีอินเทอร์เฟซฐาน 
    เวอร์ชันทั้งหมดของผลิตภัณฑ์ต้องใช้งานอินเทอร์เฟซนี้
    """

    @abstractmethod
    def useful_function_a(self) -> str:
        pass


"""
Concrete Products ถูกสร้างขึ้นโดย Concrete Factories ที่สอดคล้องกัน
"""


class ConcreteProductA1(AbstractProductA):
    def useful_function_a(self) -> str:
        return "The result of the product A1."


class ConcreteProductA2(AbstractProductA):
    def useful_function_a(self) -> str:
        return "The result of the product A2."


class AbstractProductB(ABC):
    """
    นี่คืออินเทอร์เฟซฐานของผลิตภัณฑ์อีกตัว 
    ผลิตภัณฑ์ทั้งหมดสามารถทำงานร่วมกันได้ แต่การทำงานร่วมกันอย่างถูกต้องสามารถทำได้ระหว่างผลิตภัณฑ์ของเวอร์ชันเดียวกันเท่านั้น
    """
    @abstractmethod
    def useful_function_b(self) -> str:
        """
        ผลิตภัณฑ์ B สามารถทำสิ่งของมันเองได้...
        """
        pass

    @abstractmethod
    def another_useful_function_b(self, collaborator: AbstractProductA) -> str:
        """
        ...แต่ยังสามารถร่วมมือกับผลิตภัณฑ์ A ได้ด้วย

        Abstract Factory ทำให้มั่นใจว่าผลิตภัณฑ์ทั้งหมดที่สร้างขึ้นเป็นของเวอร์ชันเดียวกันและดังนั้นจึงสามารถทำงานร่วมกันได้
        """
        pass


"""
Concrete Products ถูกสร้างขึ้นโดย Concrete Factories ที่สอดคล้องกัน
"""


class ConcreteProductB1(AbstractProductB):
    def useful_function_b(self) -> str:
        return "The result of the product B1."

    """
    เวอร์ชัน Product B1 สามารถทำงานได้อย่างถูกต้องกับเวอร์ชัน Product A1 เท่านั้น
    อย่างไรก็ตาม มันยอมรับอินสแตนซ์ใด ๆ ของ AbstractProductA เป็นอาร์กิวเมนต์
    """

    def another_useful_function_b(self, collaborator: AbstractProductA) -> str:
        result = collaborator.useful_function_a()
        return f"The result of the B1 collaborating with the ({result})"


class ConcreteProductB2(AbstractProductB):
    def useful_function_b(self) -> str:
        return "The result of the product B2."

    def another_useful_function_b(self, collaborator: AbstractProductA) -> str:
        """
        เวอร์ชัน Product B2 สามารถทำงานได้อย่างถูกต้องกับเวอร์ชัน Product A2 เท่านั้น
        อย่างไรก็ตาม มันยอมรับอินสแตนซ์ใด ๆ ของ AbstractProductA เป็นอาร์กิวเมนต์
        """
        result = collaborator.useful_function_a()
        return f"The result of the B2 collaborating with the ({result})"


def client_code(factory: AbstractFactory) -> None:
    """
    โค้ดของลูกค้าทำงานกับโรงงานและผลิตภัณฑ์ผ่านทางประเภทนามธรรมเท่านั้น: AbstractFactory และ AbstractProduct
    สิ่งนี้ช่วยให้คุณส่งผ่านคลาสย่อยของโรงงานหรือผลิตภัณฑ์ใด ๆ ให้กับโค้ดของลูกค้าโดยไม่ทำให้โค้ดพัง
    """
    product_a = factory.create_product_a()
    product_b = factory.create_product_b()

    print(f"{product_b.useful_function_b()}")
    print(f"{product_b.another_useful_function_b(product_a)}", end="")


if __name__ == "__main__":
    """
    โค้ดของลูกค้าสามารถทำงานกับคลาสโรงงานคอนกรีตใด ๆ ก็ได้
    """
    print("Client: Testing client code with the first factory type:")
    client_code(ConcreteFactory1())

    print("\n")

    print("Client: Testing the same client code with the second factory type:")
    client_code(ConcreteFactory2())
```
- Output

```python
Client: Testing client code with the first factory type:
The result of the product B1.
The result of the B1 collaborating with the (The result of the product A1.)

Client: Testing the same client code with the second factory type:
The result of the product B2.
The result of the B2 collaborating with the (The result of the product A2.)
``` 
