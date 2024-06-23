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

- 4.รูปแบบ Builder
- องค์ประกอบ Builder Pattern
รูปแบบ Builder เป็นการแยกส่วนการสร้าง Object ที่ซับซ้อนออกจาก instance ช่วยให้สามารถสร้าง Object เดียวกันด้วยวิธีการที่แตกต่างกันได้ pattern นี้จะช่วยทำให้เราสามารถรวมคำสั่งการสร้างและจัดการคำสั่งการสร้างไว้ภายใน object ได้ ส่งผลทำให้ตอนเรียกใช้งานการสร้าง Object นั้น code มีความซับซ้อนน้อยลงจากการห่อหุ้มคำสั่ง build เหล่านี้เอาไว้

- รูปแบบ Builder ประกอบด้วยองค์ประกอบต่อไปนี้

- Product เป็น Object ที่ต้องการสร้างโดย Builder และมีการกำหนดวิธีการใช้งานของ Object
- Builder เป็น interface ที่กำหนดวิธีการสร้าง Product แต่ละตัว ซึ่งประกอบด้วย method ต่าง ๆ ที่ใช้ในกระบวนการสร้าง Product ตามลำดับที่กำหนด
- Concrete Builder เป็น Class ที่สืบทอดมาจาก Builder และมีการแลกเปลี่ยนข้อมูลกับ Product ที่กำลังสร้างขึ้น
- Director เป็น Class ที่ใช้ในการควบคุมกระบวนการสร้าง Product โดยใช้ Builder เพื่อสร้าง Product ตามลำดับที่กำหนด

- ตัวอย่าง code
```python from __future__ import annotations
from abc import ABC, abstractmethod
from typing import Any


class Builder(ABC):
    """
    อินเทอร์เฟซ Builder กำหนดเมธอดสำหรับการสร้างส่วนต่างๆ ของออบเจ็กต์ Product
    """

    @property
    @abstractmethod
    def product(self) -> None:
        pass

    @abstractmethod
    def produce_part_a(self) -> None:
        pass

    @abstractmethod
    def produce_part_b(self) -> None:
        pass

    @abstractmethod
    def produce_part_c(self) -> None:
        pass


class ConcreteBuilder1(Builder):
    """
    คลาส Concrete Builder ทำตามอินเทอร์เฟซ Builder และให้การนำไปใช้เฉพาะของขั้นตอนการสร้าง
    โปรแกรมของคุณอาจมี Builder หลายรูปแบบที่นำไปใช้ต่างกัน
    """

    def __init__(self) -> None:
        """
        อินสแตนซ์ใหม่ของ Builder ควรมีออบเจ็กต์ Product ว่างเปล่าที่ใช้ในการประกอบต่อไป
        """
        self.reset()

    def reset(self) -> None:
        self._product = Product1()

    @property
    def product(self) -> Product1:
        """
        Concrete Builders ควรมีเมธอดของตัวเองสำหรับการดึงผลลัพธ์
        นั่นเป็นเพราะ Builder ประเภทต่างๆ อาจสร้างผลิตภัณฑ์ที่ไม่เหมือนกันโดยสิ้นเชิงที่ไม่ตามอินเทอร์เฟซเดียวกัน
        ดังนั้นเมธอดเหล่านี้จึงไม่สามารถประกาศในอินเทอร์เฟซ Builder พื้นฐานได้
        (อย่างน้อยในภาษาโปรแกรมที่พิมพ์แบบคงที่)

        โดยปกติหลังจากคืนผลลัพธ์สุดท้ายให้กับลูกค้า อินสแตนซ์ Builder จะต้องพร้อมที่จะเริ่มสร้างผลิตภัณฑ์อื่น
        นั่นเป็นเหตุผลที่มักเรียกเมธอด reset ที่ส่วนท้ายของเมธอด `getProduct` 
        อย่างไรก็ตาม พฤติกรรมนี้ไม่บังคับ คุณสามารถทำให้ Builder ของคุณรอการเรียก reset อย่างชัดเจนจากโค้ดของลูกค้าก่อนที่จะลบผลลัพธ์ก่อนหน้า
        """
        product = self._product
        self.reset()
        return product

    def produce_part_a(self) -> None:
        self._product.add("PartA1")

    def produce_part_b(self) -> None:
        self._product.add("PartB1")

    def produce_part_c(self) -> None:
        self._product.add("PartC1")


class Product1():
    """
    ควรใช้แพทเทิร์น Builder ก็ต่อเมื่อผลิตภัณฑ์ของคุณมีความซับซ้อนและต้องการการกำหนดค่าที่กว้างขวาง

    ต่างจากแพทเทิร์นการสร้างอื่นๆ Builders คอนกรีตต่างๆ สามารถสร้างผลิตภัณฑ์ที่ไม่เกี่ยวข้องกันได้
    กล่าวอีกนัยหนึ่ง ผลลัพธ์ของ Builders ต่างๆ อาจไม่ตามอินเทอร์เฟซเดียวกันเสมอไป
    """

    def __init__(self) -> None:
        self.parts = []

    def add(self, part: Any) -> None:
        self.parts.append(part)

    def list_parts(self) -> None:
        print(f"Product parts: {', '.join(self.parts)}", end="")


class Director:
    """
    Director รับผิดชอบเฉพาะการดำเนินการขั้นตอนการสร้างตามลำดับที่กำหนดเท่านั้น
    มันมีประโยชน์เมื่อผลิตผลิตภัณฑ์ตามลำดับหรือการกำหนดค่าที่เฉพาะเจาะจง
    จริงๆ แล้วคลาส Director เป็นตัวเลือก เนื่องจากลูกค้าสามารถควบคุม Builders ได้โดยตรง
    """

    def __init__(self) -> None:
        self._builder = None

    @property
    def builder(self) -> Builder:
        return self._builder

    @builder.setter
    def builder(self, builder: Builder) -> None:
        """
        Director ทำงานกับอินสแตนซ์ของ Builder ใดๆ ที่โค้ดของลูกค้าส่งมาให้
        ด้วยวิธีนี้ โค้ดของลูกค้าอาจเปลี่ยนประเภทของผลิตภัณฑ์ที่ประกอบใหม่ได้
        """
        self._builder = builder

    """
    Director สามารถสร้างผลิตภัณฑ์หลายเวอร์ชันโดยใช้ขั้นตอนการสร้างเดียวกัน
    """

    def build_minimal_viable_product(self) -> None:
        self.builder.produce_part_a()

    def build_full_featured_product(self) -> None:
        self.builder.produce_part_a()
        self.builder.produce_part_b()
        self.builder.produce_part_c()


if __name__ == "__main__":
    """
    โค้ดของลูกค้าสร้างออบเจ็กต์ Builder ส่งให้กับ Director และเริ่มกระบวนการสร้าง 
    ผลลัพธ์สุดท้ายจะถูกดึงจากออบเจ็กต์ Builder
    """

    director = Director()
    builder = ConcreteBuilder1()
    director.builder = builder

    print("Standard basic product: ")
    director.build_minimal_viable_product()
    builder.product.list_parts()

    print("\n")

    print("Standard full featured product: ")
    director.build_full_featured_product()
    builder.product.list_parts()

    print("\n")

    # จำไว้ว่าแพทเทิร์น Builder สามารถใช้ได้โดยไม่มีคลาส Director
    print("Custom product: ")
    builder.produce_part_a()
    builder.produce_part_b()
    builder.product.list_parts()
```

- Output
```python
Standard basic product: 
Product parts: PartA1

Standard full featured product: 
Product parts: PartA1, PartB1, PartC1

Custom product: 
Product parts: PartA1, PartB1
```

- 5. รูปแบบ Prototype
- รูปแบบ Prototype เป็นวิธีการออกแบบ Software ที่ช่วยให้สร้าง Object ใหม่โดยการคัดลอก Object ที่มีอยู่ออกมาได้ (ตามชื่อ Prototype นั้นเลย) เพื่อเป็นการประหยัดกระบวนการสร้าง object ที่อาจจะต้องค่อยๆใส่ข้อมูลทีละชุดเข้าไปจากการสร้าง instance ใหม่ เราสามารถใช้ pattern นี้ในการสร้าง object ที่หน้าตาเหมือนกันออกมาได้เลย

- รูปแบบ Prototype ประกอบด้วยองค์ประกอบต่อไปนี้

- Prototype เป็น Object ต้นแบบที่ใช้ในการคัดลอกและสร้าง Object ใหม่ มักใช้ในรูปแบบของ instance ที่มีคุณสมบัติเดียวกันกับวัตถุต้นแบบ
- Concrete Prototype เป็น Class ที่สืบทอดมาจาก Prototype และมีการ clone และสร้าง Object ใหม่จากต้นแบบ
- Client เป็น Class หรือ Module ที่ใช้ในการ เรียกใช้งาน Object ต้นแบบและสร้าง Object ใหม่จากต้นแบบ (เป็นคนที่หยิบ Object หลัง Clone ไปใช้)

- ตัวอย่าง code
```python
import copy


class SelfReferencingEntity:
    def __init__(self):
        self.parent = None

    def set_parent(self, parent):
        self.parent = parent


class SomeComponent:
    """
    Python มีอินเทอร์เฟซ Prototype ของตัวเองผ่านฟังก์ชัน `copy.copy` และ `copy.deepcopy`
    คลาสใด ๆ ที่ต้องการการใช้งานที่กำหนดเองต้อง override ฟังก์ชันสมาชิก `__copy__` และ `__deepcopy__`
    """

    def __init__(self, some_int, some_list_of_objects, some_circular_ref):
        self.some_int = some_int
        self.some_list_of_objects = some_list_of_objects
        self.some_circular_ref = some_circular_ref

    def __copy__(self):
        """
        สร้าง shallow copy เมธอดนี้จะถูกเรียกเมื่อมีการเรียก `copy.copy` 
        ด้วยออบเจ็กต์นี้และค่าที่คืนจะเป็น shallow copy ใหม่
        """

        # สร้างสำเนาของออบเจ็กต์ nested ก่อน
        some_list_of_objects = copy.copy(self.some_list_of_objects)
        some_circular_ref = copy.copy(self.some_circular_ref)

        # โคลนออบเจ็กต์ตัวเองโดยใช้สำเนาของออบเจ็กต์ nested ที่เตรียมไว้
        new = self.__class__(
            self.some_int, some_list_of_objects, some_circular_ref
        )
        new.__dict__.update(self.__dict__)

        return new

    def __deepcopy__(self, memo=None):
        """
        สร้าง deep copy เมธอดนี้จะถูกเรียกเมื่อมีการเรียก `copy.deepcopy` 
        ด้วยออบเจ็กต์นี้และค่าที่คืนจะเป็น deep copy ใหม่

        อาร์กิวเมนต์ `memo` ใช้ทำอะไร? Memo เป็นดิกชันนารีที่ไลบรารี `deepcopy` 
        ใช้เพื่อป้องกันการคัดลอกแบบวนซ้ำไม่รู้จบในกรณีของ circular references 
        ส่งมันไปยังการเรียก `deepcopy` ทั้งหมดใน implementation ของ `__deepcopy__` 
        เพื่อป้องกันการวนซ้ำไม่รู้จบ
        """
        if memo is None:
            memo = {}

        # สร้างสำเนาของออบเจ็กต์ nested ก่อน
        some_list_of_objects = copy.deepcopy(self.some_list_of_objects, memo)
        some_circular_ref = copy.deepcopy(self.some_circular_ref, memo)

        # โคลนออบเจ็กต์ตัวเองโดยใช้สำเนาของออบเจ็กต์ nested ที่เตรียมไว้
        new = self.__class__(
            self.some_int, some_list_of_objects, some_circular_ref
        )
        new.__dict__ = copy.deepcopy(self.__dict__, memo)

        return new


if __name__ == "__main__":

    list_of_objects = [1, {1, 2, 3}, [1, 2, 3]]
    circular_ref = SelfReferencingEntity()
    component = SomeComponent(23, list_of_objects, circular_ref)
    circular_ref.set_parent(component)

    shallow_copied_component = copy.copy(component)

    # เปลี่ยนแปลง list ใน shallow_copied_component และดูว่ามันเปลี่ยนแปลงใน component หรือไม่
    shallow_copied_component.some_list_of_objects.append("another object")
    if component.some_list_of_objects[-1] == "another object":
        print(
            "Adding elements to `shallow_copied_component`'s "
            "some_list_of_objects adds it to `component`'s "
            "some_list_of_objects."
        )
    else:
        print(
            "Adding elements to `shallow_copied_component`'s "
            "some_list_of_objects doesn't add it to `component`'s "
            "some_list_of_objects."
        )

    # เปลี่ยนแปลง set ใน list ของ objects
    component.some_list_of_objects[1].add(4)
    if 4 in shallow_copied_component.some_list_of_objects[1]:
        print(
            "Changing objects in the `component`'s some_list_of_objects "
            "changes that object in `shallow_copied_component`'s "
            "some_list_of_objects."
        )
    else:
        print(
            "Changing objects in the `component`'s some_list_of_objects "
            "doesn't change that object in `shallow_copied_component`'s "
            "some_list_of_objects."
        )

    deep_copied_component = copy.deepcopy(component)

    # เปลี่ยนแปลง list ใน deep_copied_component และดูว่ามันเปลี่ยนแปลงใน component หรือไม่
    deep_copied_component.some_list_of_objects.append("one more object")
    if component.some_list_of_objects[-1] == "one more object":
        print(
            "Adding elements to `deep_copied_component`'s "
            "some_list_of_objects adds it to `component`'s "
            "some_list_of_objects."
        )
    else:
        print(
            "Adding elements to `deep_copied_component`'s "
            "some_list_of_objects doesn't add it to `component`'s "
            "some_list_of_objects."
        )

    # เปลี่ยนแปลง set ใน list ของ objects
    component.some_list_of_objects[1].add(10)
    if 10 in deep_copied_component.some_list_of_objects[1]:
        print(
            "Changing objects in the `component`'s some_list_of_objects "
            "changes that object in `deep_copied_component`'s "
            "some_list_of_objects."
        )
    else:
        print(
            "Changing objects in the `component`'s some_list_of_objects "
            "doesn't change that object in `deep_copied_component`'s "
            "some_list_of_objects."
        )

    print(
        f"id(deep_copied_component.some_circular_ref.parent): "
        f"{id(deep_copied_component.some_circular_ref.parent)}"
    )
    print(
        f"id(deep_copied_component.some_circular_ref.parent.some_circular_ref.parent): "
        f"{id(deep_copied_component.some_circular_ref.parent.some_circular_ref.parent)}"
    )
    print(
        "^^ This shows that deepcopied objects contain same reference, they "
        "are not cloned repeatedly."
    )

```
- Output
```python
Adding elements to `shallow_copied_component`'s some_list_of_objects adds it to `component`'s some_list_of_objects.
Changing objects in the `component`'s some_list_of_objects changes that object in `shallow_copied_component`'s some_list_of_objects.
Adding elements to `deep_copied_component`'s some_list_of_objects doesn't add it to `component`'s some_list_of_objects.
Changing objects in the `component`'s some_list_of_objects doesn't change that object in `deep_copied_component`'s some_list_of_objects.
id(deep_copied_component.some_circular_ref.parent): 4429472784
id(deep_copied_component.some_circular_ref.parent.some_circular_ref.parent): 4429472784
^^ This shows that deepcopied objects contain same reference, they are not cloned repeatedly.
```

- Design Pattern Structural คืออะไร ?
- Design Pattern Structural เป็นหนึ่งในหมวดหมู่ของ Design Patterns ที่มุ่งเน้นไปที่วิธีการจัดการและประกอบความสัมพันธ์ระหว่าง Object และ Class โดยทำให้โปรแกรมมีความยืดหยุ่นและสามารถรองรับการเปลี่ยนแปลงได้ง่ายขึ้น ซึ่งประกอบด้วย 7 รูปแบบหลัก ได้แก่ Adapter, Bridge, Composite, Decorator, Facade, Flyweight, และ Proxy แต่ละแบบมีคุณสมบัติดังนี้

- Adapter - ปรับให้ interface ของ Class ที่ไม่เข้ากันสามารถทำงานร่วมกันได้ โดยไม่ต้องเปลี่ยนแปลง code ที่มีอยู่ของทั้งสองฝ่าย (Class ผู้สร้างและ instance ที่ใช้) เหมือนกับการใช้ adapter ในชีวิตจริงเพื่อให้ปลั๊กไฟจากประเทศหนึ่งเข้ากับปลั๊กของประเทศอื่นได้
- Bridge - แยก abstraction (interface) จาก implementation ของมันเอง เพื่อให้ทั้งสอง (ที่เคยอยู่ใน class เดียวกัน) สามารถเปลี่ยนแปลงได้อย่างอิสระต่อกันได้ (แทนที่จะต้องสร้าง class กับทุกๆประเภทออกมาแทน)
- Composite - การประกอบ Object ในรูปแบบ tree เพื่อทำให้สามารถสร้าง Object ทั้งแบบตัวเอง และ แบบภายในตัวของมันเอง (แบบกลุ่ม) ออกมาได้
- Decorator - เพิ่ม method ใหม่ให้กับ Object ตัวนั้นๆ โดยไม่เปลี่ยนแปลง Class และ bahavior ของ Object อื่นๆที่เรียกใช้ class นั้นอยู่ (เป็นการเพิ่ม function ให้กับ object ขณะเรียกใช้งาน)
- Facade - คือการสร้าง interface ที่คุยกับ complex system ของ class, library หรือ framework (subsystem ทั้งหลาย) เพื่อเป็นการรวมการพูดคุยมาไว้ภายใน interface ตัวเดียวออกมาแทน
- Flyweight - Pattern ที่ใช้สำหรับลดการใช้ memory ด้วยการ share data ระหว่าง object ที่ใช้งานเหมือนๆกันออกมา มักใช้กับเหตุการณ์ที่ต้องมีการสร้าง object จำนวนมากขึ้นมา (จุดประสงค์เพื่อเป็นการลดการ instance object จำนวนมากให้เกิดขึ้นใน memory ขึ้นมา)
- Proxy - Pattern ที่จะทำการสร้าง object เป็นตัวแทนของการพูดคุยกับ object อื่นแทนการ access ตรงๆ เพื่อให้สามารถควบคุมการจัดการกับ object ที่เป็นเป้าหมายการเรียกใช้ออกมาได้ (เช่น ควบคุมการ access, ควบคุมการสร้าง, การทำ cache หรือ lazy initialization เป็นต้น)

- รูปแบบ Adapter
- Adapter pattern (บางที่ก็จะใช้คำว่า Wrapper pattern) คือ design pattern ที่อนุญาตให้ object ที่ไม่สามารถใช้งานร่วมกันได้ สามารถใช้งานร่วมกันได้ ซึ่งเบื้องหลังของการใช้ Adapter pattern คือการสร้างตัวที่เป็นเหมือนตัวแปลงระหว่าง 2 ตัวที่ไม่เข้ากัน convert เข้ามาหากัน เพื่อให้สามารถใช้งานร่วมกันได้ตามที่ client ต้องการ

- องค์ประกอบของ Adapter จะมีดังนี้

- Target interface ที่ client ต้องการจะใช้งาน
- Adaptee class ที่มี interface ของตัวที่เป็นอยู่ปัจจุบัน (เป็นตัวที่ต้องการจะแปลงไป) แต่ไม่สามารถใช้งานได้ใน client code version ปัจจุบันแล้ว
- Adapter class ที่จะทำการ implement ตาม Target interface ที่จะทำการห่อ Adaptee เพื่อทำการแปลง Adaptee ให้ใช้งานกับ Target ได้
- ตัวอย่าง code
```python
class Target:
    """
    The Target defines the domain-specific interface used by the client code.
    """

    def request(self) -> str:
        return "Target: The default target's behavior."


class Adaptee:
    """
    The Adaptee contains some useful behavior, but its interface is incompatible
    with the existing client code. The Adaptee needs some adaptation before the
    client code can use it.
    """

    def specific_request(self) -> str:
        return ".eetpadA eht fo roivaheb laicepS"


class Adapter(Target, Adaptee):
    """
    The Adapter makes the Adaptee's interface compatible with the Target's
    interface via multiple inheritance.
    """

    def request(self) -> str:
        return f"Adapter: (TRANSLATED) {self.specific_request()[::-1]}"


def client_code(target: "Target") -> None:
    """
    The client code supports all classes that follow the Target interface.
    """

    print(target.request(), end="")


if __name__ == "__main__":
    print("Client: I can work just fine with the Target objects:")
    target = Target()
    client_code(target)
    print("\n")

    adaptee = Adaptee()
    print("Client: The Adaptee class has a weird interface. "
          "See, I don't understand it:")
    print(f"Adaptee: {adaptee.specific_request()}", end="\n\n")

    print("Client: But I can work with it via the Adapter:")
    adapter = Adapter()
    client_code(adapter)
```
- Output
```python
Client: I can work just fine with the Target objects:
Target: The default target's behavior.

Client: The Adaptee class has a weird interface. See, I don't understand it:
Adaptee: .eetpadA eht fo roivaheb laicepS

Client: But I can work with it via the Adapter:
Adapter: (TRANSLATED) Special behavior of the Adaptee.
```
- Bridge design pattern คือ pattern ที่ทำการแยกส่วน abstraction ออกมาจากส่วนของ implementation อีกทีเมื่อพบว่า ของลักษณะ 2 อย่างสามารถแยกส่วนให้ independent (ไม่ขึ้นต่อกัน) ได้ โดยปกติ pattern นี้จะเกี่ยวกับการแยกส่วนของพวก class ใหญ่ๆ หรือ set ของ class ที่ใกล้ๆกัน (แต่ใช้แยกกันได้) ทำการแยกส่วนกันออกมา เพื่อให้สามารถ implement ทั้ง 2 ส่วนแยกออกจากกันได้

- องค์ประกอบของ Bridge จะประกอบด้วย

- Abstraction layer นี้จะเป็นส่วนที่เป็น core (ส่วนใหญ่จะเป็น interface หรือ abstract class) ของ component ที่ต้องการประกาศให้เป็น high level control logic เพื่อใช้สำหรับการแยกส่วน implementation ออกจากกัน
- Refined Abstraction เป็นส่วนขยายจาก Abstraction อีกทีโดยเพิ่ม behavior ลงไปใน Abstraction (โดยไม่ต้องแก้ไข interface เพิ่มเติมใน Implementor)
- Implementor เป็นส่วนของ interface ที่ทำการกำหนดว่า จะต้อง implement operation ออกมายังไง (โดยอ้างอิงถึง abstraction ที่เป็นตัวหลัก)
- Concrete Implementor เป็น class ที่จะ implement ต่อจาก implementor interface อีกที โดยจะเป็นการใส่ method ของการทำงานเข้าไป

- ตัวอย่าง code
```python 
from __future__ import annotations
from abc import ABC, abstractmethod


class Abstraction:
    """
    The Abstraction defines the interface for the "control" part of the two
    class hierarchies. It maintains a reference to an object of the
    Implementation hierarchy and delegates all of the real work to this object.
    """

    def __init__(self, implementation: Implementation) -> None:
        self.implementation = implementation

    def operation(self) -> str:
        return (f"Abstraction: Base operation with:\n"
                f"{self.implementation.operation_implementation()}")


class ExtendedAbstraction(Abstraction):
    """
    You can extend the Abstraction without changing the Implementation classes.
    """

    def operation(self) -> str:
        return (f"ExtendedAbstraction: Extended operation with:\n"
                f"{self.implementation.operation_implementation()}")


class Implementation(ABC):
    """
    The Implementation defines the interface for all implementation classes. It
    doesn't have to match the Abstraction's interface. In fact, the two
    interfaces can be entirely different. Typically the Implementation interface
    provides only primitive operations, while the Abstraction defines higher-
    level operations based on those primitives.
    """

    @abstractmethod
    def operation_implementation(self) -> str:
        pass


"""
Each Concrete Implementation corresponds to a specific platform and implements
the Implementation interface using that platform's API.
"""


class ConcreteImplementationA(Implementation):
    def operation_implementation(self) -> str:
        return "ConcreteImplementationA: Here's the result on the platform A."


class ConcreteImplementationB(Implementation):
    def operation_implementation(self) -> str:
        return "ConcreteImplementationB: Here's the result on the platform B."


def client_code(abstraction: Abstraction) -> None:
    """
    Except for the initialization phase, where an Abstraction object gets linked
    with a specific Implementation object, the client code should only depend on
    the Abstraction class. This way the client code can support any abstraction-
    implementation combination.
    """

    # ...

    print(abstraction.operation(), end="")

    # ...


if __name__ == "__main__":
    """
    The client code should be able to work with any pre-configured abstraction-
    implementation combination.
    """

    implementation = ConcreteImplementationA()
    abstraction = Abstraction(implementation)
    client_code(abstraction)

    print("\n")

    implementation = ConcreteImplementationB()
    abstraction = ExtendedAbstraction(implementation)
    client_code(abstraction)
```

- Output
```python 
Abstraction: Base operation with:
ConcreteImplementationA: Here's the result on the platform A.

ExtendedAbstraction: Extended operation with:
ConcreteImplementationB: Here's the result on the platform B.
```

- 3. รูปแบบ Composite
- Compisite pattern คือ pattern ที่ทำการรวม object ไว้เป็นโครงสร้างแบบ tree structure เพื่อนำเสนอ object ในรูปแบบ heirarchies ออกมา โดย Pattern นี้จะอนุญาตให้ client สามารถเรียก object ทีละตัวแยกออกจากกัน และสามารถเรียกใข้ object นั้นแบบรวมหลายตัวพร้อมกัน ด้วย class ตัวเดียวกันออกมาได้นั่นเอง

- องค์ประกอบของ Composite

- Components intetface ที่กำหนด opration ทั่วไปสำหรับ composite (object ที่ใช้รวม object ตัวอื่นๆ) และ leaf node (object ที่ใช้แยก) ใน tree structure ซึ่งโดยปกติ ก็จะประกอบไปด้วย เพิ่ม, ลบ และดึง child component ออกมา
Leaf นำเสนอ leaf object ที่อยู่ใน composite โดย leaf object นั้นจะไม่มี children อยู่ แต่จะมีการกำหนด behavior ของ object เอาไว้ในนี้แทน (ซึ่งจะเป็น behavior เดียวกับที่ composite ทำงาน)
Composite class ที่ทำการเก็บ child components เอาไว้ ซึ่งใน composite จะประกอบด้วย leaf และ composite อยู่ด้วยกัน โดย Composite จะ implement ตาม interface และกำหนด operation ให้กับ children เพื่อให้ children แต่ละตัวต่างไปทำ behavior ของตัวเองต่อได้

- ตัวอย่าง code
```python
from __future__ import annotations
from abc import ABC, abstractmethod
from typing import List


class Component(ABC):
    """
    The base Component class declares common operations for both simple and
    complex objects of a composition.
    """

    @property
    def parent(self) -> Component:
        return self._parent

    @parent.setter
    def parent(self, parent: Component):
        """
        Optionally, the base Component can declare an interface for setting and
        accessing a parent of the component in a tree structure. It can also
        provide some default implementation for these methods.
        """

        self._parent = parent

    """
    In some cases, it would be beneficial to define the child-management
    operations right in the base Component class. This way, you won't need to
    expose any concrete component classes to the client code, even during the
    object tree assembly. The downside is that these methods will be empty for
    the leaf-level components.
    """

    def add(self, component: Component) -> None:
        pass

    def remove(self, component: Component) -> None:
        pass

    def is_composite(self) -> bool:
        """
        You can provide a method that lets the client code figure out whether a
        component can bear children.
        """

        return False

    @abstractmethod
    def operation(self) -> str:
        """
        The base Component may implement some default behavior or leave it to
        concrete classes (by declaring the method containing the behavior as
        "abstract").
        """

        pass


class Leaf(Component):
    """
    The Leaf class represents the end objects of a composition. A leaf can't
    have any children.

    Usually, it's the Leaf objects that do the actual work, whereas Composite
    objects only delegate to their sub-components.
    """

    def operation(self) -> str:
        return "Leaf"


class Composite(Component):
    """
    The Composite class represents the complex components that may have
    children. Usually, the Composite objects delegate the actual work to their
    children and then "sum-up" the result.
    """

    def __init__(self) -> None:
        self._children: List[Component] = []

    """
    A composite object can add or remove other components (both simple or
    complex) to or from its child list.
    """

    def add(self, component: Component) -> None:
        self._children.append(component)
        component.parent = self

    def remove(self, component: Component) -> None:
        self._children.remove(component)
        component.parent = None

    def is_composite(self) -> bool:
        return True

    def operation(self) -> str:
        """
        The Composite executes its primary logic in a particular way. It
        traverses recursively through all its children, collecting and summing
        their results. Since the composite's children pass these calls to their
        children and so forth, the whole object tree is traversed as a result.
        """

        results = []
        for child in self._children:
            results.append(child.operation())
        return f"Branch({'+'.join(results)})"


def client_code(component: Component) -> None:
    """
    The client code works with all of the components via the base interface.
    """

    print(f"RESULT: {component.operation()}", end="")


def client_code2(component1: Component, component2: Component) -> None:
    """
    Thanks to the fact that the child-management operations are declared in the
    base Component class, the client code can work with any component, simple or
    complex, without depending on their concrete classes.
    """

    if component1.is_composite():
        component1.add(component2)

    print(f"RESULT: {component1.operation()}", end="")


if __name__ == "__main__":
    # This way the client code can support the simple leaf components...
    simple = Leaf()
    print("Client: I've got a simple component:")
    client_code(simple)
    print("\n")

    # ...as well as the complex composites.
    tree = Composite()

    branch1 = Composite()
    branch1.add(Leaf())
    branch1.add(Leaf())

    branch2 = Composite()
    branch2.add(Leaf())

    tree.add(branch1)
    tree.add(branch2)

    print("Client: Now I've got a composite tree:")
    client_code(tree)
    print("\n")

    print("Client: I don't need to check the components classes even when managing the tree:")
    client_code2(tree, simple)
```

- Output
```python
Client: I've got a simple component:
RESULT: Leaf

Client: Now I've got a composite tree:
RESULT: Branch(Branch(Leaf+Leaf)+Branch(Leaf))

Client: I don't need to check the components classes even when managing the tree:
RESULT: Branch(Branch(Leaf+Leaf)+Branch(Leaf)+Leaf)
```

- รูปแบบ Decorator
- รูปแบบการออกแบบ Decorator เป็นรูปแบบเชิงโครงสร้าง (structural pattern) ที่เปิดให้เราสามารถเพิ่มพฤติกรรม (behavior) เข้าไปยังวัตถุ (object) เดี่ยวๆ ได้ โดยไม่กระทบต่อพฤติกรรมของ object อื่นๆ ใน class เดียวกัน รูปแบบนี้เป็นประโยชน์อย่างมากในการยึดหลักการ Open/Closed ซึ่งเป็นหนึ่งในหลักการ SOLID ที่ระบุว่าคลาสหนึ่งๆ ควรเปิดสำหรับการเพิ่มเติมส่วนขยาย แต่ปิดสำหรับการแก้ไขดัดแปลงโดยตรง

- องค์ประกอบของ Decorator

- Component กำหนด interface สำหรับ Object ที่เราจะสามารถเพิ่มความสามารถเข้าไปได้ภายหลัง (ตอนที่โปรแกรมรันอยู่)
- Concrete Component นำ interface ของ Component มา implement ตัวนี้เปรียบเสมือน Base Object ที่เราจะเพิ่มความสามารถให้ในภายหลังได้
- Decorator ส่วนนี้จะ reference ไปยัง Object ที่เป็น Component และมี interface ที่สอดคล้องกับ interface ของ Component ด้วย ตัว Decorator จะเป็นเหมือน Base ในการสร้างตัวตกแต่งที่เฉพาะเจาะจงต่อไป
- Concrete Decorators เป็นการใช้งาน Decorator จริงๆ ตรงนี้เราจะเขียน code ใส่ behavior ต่างๆ ที่อยากเพิ่มให้กับ Object xของเราเข้าไป ซึ่งอาจมี Concrete Decorator ได้หลายตัวเพื่อตกแต่งในรูปแบบที่แตกต่างกันออกไป

- ตัวอย่าง code
```python
class Component():
    """
    The base Component interface defines operations that can be altered by
    decorators.
    """

    def operation(self) -> str:
        pass


class ConcreteComponent(Component):
    """
    Concrete Components provide default implementations of the operations. There
    might be several variations of these classes.
    """

    def operation(self) -> str:
        return "ConcreteComponent"


class Decorator(Component):
    """
    The base Decorator class follows the same interface as the other components.
    The primary purpose of this class is to define the wrapping interface for
    all concrete decorators. The default implementation of the wrapping code
    might include a field for storing a wrapped component and the means to
    initialize it.
    """

    _component: Component = None

    def __init__(self, component: Component) -> None:
        self._component = component

    @property
    def component(self) -> Component:
        """
        The Decorator delegates all work to the wrapped component.
        """

        return self._component

    def operation(self) -> str:
        return self._component.operation()


class ConcreteDecoratorA(Decorator):
    """
    Concrete Decorators call the wrapped object and alter its result in some
    way.
    """

    def operation(self) -> str:
        """
        Decorators may call parent implementation of the operation, instead of
        calling the wrapped object directly. This approach simplifies extension
        of decorator classes.
        """
        return f"ConcreteDecoratorA({self.component.operation()})"


class ConcreteDecoratorB(Decorator):
    """
    Decorators can execute their behavior either before or after the call to a
    wrapped object.
    """

    def operation(self) -> str:
        return f"ConcreteDecoratorB({self.component.operation()})"


def client_code(component: Component) -> None:
    """
    The client code works with all objects using the Component interface. This
    way it can stay independent of the concrete classes of components it works
    with.
    """

    # ...

    print(f"RESULT: {component.operation()}", end="")

    # ...


if __name__ == "__main__":
    # This way the client code can support both simple components...
    simple = ConcreteComponent()
    print("Client: I've got a simple component:")
    client_code(simple)
    print("\n")

    # ...as well as decorated ones.
    #
    # Note how decorators can wrap not only simple components but the other
    # decorators as well.
    decorator1 = ConcreteDecoratorA(simple)
    decorator2 = ConcreteDecoratorB(decorator1)
    print("Client: Now I've got a decorated component:")
    client_code(decorator2)
```

- Output
```python
Client: I've got a simple component:
RESULT: ConcreteComponent

Client: Now I've got a decorated component:
RESULT: ConcreteDecoratorB(ConcreteDecoratorA(ConcreteComponent))
```
- 5.รูปแบบ Facade
- รูปแบบการออกแบบ Facade เป็นรูปแบบที่สร้าง interface แบบง่าย เพื่อให้สามารถใช้งานระบบย่อย (subsystems) อันซับซ้อนที่อาจประกอบด้วย class, library หรือ framework ต่างๆออกมาได้ รูปแบบนี้จะใช้ facade object เพื่อทำหน้าที่เป็นจุดเข้าถึงเพียงจุดเดียว 
  ซึ่งจะคอยอำพรางความซับซ้อนของระบบย่อยเอาไว้ไม่ให้ฝั่งผู้ใช้งาน (client) เห็น ทำให้ผู้ใช้งานสามารถโต้ตอบกับระบบได้ผ่าน interface ที่ตรงไปตรงมา โดยไม่ต้องกังวลกับความซับซ้อนภายในได้

- องค์ประกอบของ Facade ประกอบด้วย

- Facade class หลักที่ทำหน้าที่เป็น interface แบบง่ายสำหรับการเข้าถึงระบบย่อย Facade จะรับผิดชอบจัดการกับระบบย่อยทั้งหมดและเปิดเผย API ที่ใช้งานง่ายแก่ผู้ใช้งาน
- Subsystem ระบบย่อยหรือ Class ต่างๆ ที่มีความซับซ้อน Facade จะทำหน้าที่ซ่อนความซับซ้อนเหล่านี้จากผู้ใช้งานเอาไว้
- Client ผู้ใช้งานหรือ Class อื่นๆ ที่ต้องการใช้ระบบย่อย Client จะโต้ตอบกับระบบผ่าน Facade โดยไม่ต้องรู้รายละเอียดของระบบย่อย

- ตัวอย่าง code
```python
from __future__ import annotations


class Facade:
    """
    The Facade class provides a simple interface to the complex logic of one or
    several subsystems. The Facade delegates the client requests to the
    appropriate objects within the subsystem. The Facade is also responsible for
    managing their lifecycle. All of this shields the client from the undesired
    complexity of the subsystem.
    """

    def __init__(self, subsystem1: Subsystem1, subsystem2: Subsystem2) -> None:
        """
        Depending on your application's needs, you can provide the Facade with
        existing subsystem objects or force the Facade to create them on its
        own.
        """

        self._subsystem1 = subsystem1 or Subsystem1()
        self._subsystem2 = subsystem2 or Subsystem2()

    def operation(self) -> str:
        """
        The Facade's methods are convenient shortcuts to the sophisticated
        functionality of the subsystems. However, clients get only to a fraction
        of a subsystem's capabilities.
        """

        results = []
        results.append("Facade initializes subsystems:")
        results.append(self._subsystem1.operation1())
        results.append(self._subsystem2.operation1())
        results.append("Facade orders subsystems to perform the action:")
        results.append(self._subsystem1.operation_n())
        results.append(self._subsystem2.operation_z())
        return "\n".join(results)


class Subsystem1:
    """
    The Subsystem can accept requests either from the facade or client directly.
    In any case, to the Subsystem, the Facade is yet another client, and it's
    not a part of the Subsystem.
    """

    def operation1(self) -> str:
        return "Subsystem1: Ready!"

    # ...

    def operation_n(self) -> str:
        return "Subsystem1: Go!"


class Subsystem2:
    """
    Some facades can work with multiple subsystems at the same time.
    """

    def operation1(self) -> str:
        return "Subsystem2: Get ready!"

    # ...

    def operation_z(self) -> str:
        return "Subsystem2: Fire!"


def client_code(facade: Facade) -> None:
    """
    The client code works with complex subsystems through a simple interface
    provided by the Facade. When a facade manages the lifecycle of the
    subsystem, the client might not even know about the existence of the
    subsystem. This approach lets you keep the complexity under control.
    """

    print(facade.operation(), end="")


if __name__ == "__main__":
    # The client code may have some of the subsystem's objects already created.
    # In this case, it might be worthwhile to initialize the Facade with these
    # objects instead of letting the Facade create new instances.
    subsystem1 = Subsystem1()
    subsystem2 = Subsystem2()
    facade = Facade(subsystem1, subsystem2)
    client_code(facade)
```

- Output
```python
Facade initializes subsystems:
Subsystem1: Ready!
Subsystem2: Get ready!
Facade orders subsystems to perform the action:
Subsystem1: Go!
Subsystem2: Fire!
```
- 6.รูปแบบ Flyweight
- รูปแบบการออกแบบ Flyweight เป็นรูปแบบที่ใช้เพื่อลดการใช้หน่วยความจำหรือลดต้นทุนการคำนวณโดยการแบ่งปันข้อมูลให้มากที่สุดเท่าที่จะทำได้กับ Object ที่เกี่ยวข้อง รูปแบบนี้มีประโยชน์อย่างมากเมื่อมี Object จำนวนมากที่ต้องใช้ state ร่วมกัน โดยหลักการแล้วรูปแบบ Flyweight มีเป้าหมายเพื่อนำ instance ของวัตถุกลับมาใช้ใหม่เพื่อลดความต้องการทรัพยากรหน่วยความจำด้วยการ share ร่วมกัน โดยแยกแยะระหว่างสถานะภายในของวัตถุ (intrinsic state) ซึ่งจะเหมือนกันในทุก instance ออกจากสถานะภายนอก (extrinsic state) ซึ่งจะแตกต่างกันได้ระหว่าง object

- อธิบายเพิ่มเติม

- Intrinsic state คือ ข้อมูลหรือคุณสมบัติที่เป็นคุณสมบัติหลักของ Object (unique) ไม่เปลี่ยนแปลงตามบริบทการใช้งาน ตัวอย่างเช่น รหัสอักขระของตัวอักษร (a, ก), ขนาดของรูปภาพ, เพศของบุคคล
- Extrinsic State คือ ข้อมูลหรือคุณสมบัติที่เปลี่ยนแปลงตามบริบทการใช้งาน ตัวอย่างเช่น ตำแหน่งของตัวอักษรในข้อความ, สีพื้นหลังของรูปภาพ, อารมณ์ของบุคคล
- องค์ประกอบของ Flyweight ประกอบด้วย

- Flyweight interface กลางที่ Flyweight ตัวต่างๆ จะนำไปใช้งานเพื่อรองรับการรับและจัดการกับ extrinsic state (สถานะภายนอก)
Concrete Flyweight คือการเขียน code เพื่อใช้งานตาม interface ของ Flyweight ตรงนี้จะมีการเก็บ intrinsic state (สถานะภายใน) ไว้ โดย intrinsic state จะเป็นข้อมูลที่ไม่ขึ้นอยู่กับบริบทของการใช้งาน และสามารถแชร์กันได้ (ตัวอย่างเช่น รหัสอักขระของตัวอักษรแต่ละตัว)
- Flyweight Factory ส่วนนี้ทำหน้าที่จัดการ object ประเภท Flyweight และมั่นใจว่าจะเกิดการแชร์ใช้ object หรือ instance ร่วมกันอย่างเหมาะสม เมื่อ Client request การใช้งาน Flyweight Factory นี้จะดูว่ามีอยู่แล้วหรือไม่ ถ้ายังไม่มีก็จะสร้างใหม่ออกไปและจัดเก็บไว้ใน Factory อย่างถูกต้องได้
- Client Code ส่วนที่เรียกใช้ Flyweight Factory เพื่อเข้าถึง Object ประเภท Flyweight โดยมีหน้าที่รับผิดชอบเรื่องการจัดการ extrinsic state (สถานะภายนอก) ที่เกี่ยวข้องกับ Flyweight แต่ละตัว (ซึ่งมีโอกาสแตกต่างกันได้ และแชร์กันไม่ได้)

- ตัวอย่าง code
```python
import json
from typing import Dict


class Flyweight():
    """
    The Flyweight stores a common portion of the state (also called intrinsic
    state) that belongs to multiple real business entities. The Flyweight
    accepts the rest of the state (extrinsic state, unique for each entity) via
    its method parameters.
    """

    def __init__(self, shared_state: str) -> None:
        self._shared_state = shared_state

    def operation(self, unique_state: str) -> None:
        s = json.dumps(self._shared_state)
        u = json.dumps(unique_state)
        print(f"Flyweight: Displaying shared ({s}) and unique ({u}) state.", end="")


class FlyweightFactory():
    """
    The Flyweight Factory creates and manages the Flyweight objects. It ensures
    that flyweights are shared correctly. When the client requests a flyweight,
    the factory either returns an existing instance or creates a new one, if it
    doesn't exist yet.
    """

    _flyweights: Dict[str, Flyweight] = {}

    def __init__(self, initial_flyweights: Dict) -> None:
        for state in initial_flyweights:
            self._flyweights[self.get_key(state)] = Flyweight(state)

    def get_key(self, state: Dict) -> str:
        """
        Returns a Flyweight's string hash for a given state.
        """

        return "_".join(sorted(state))

    def get_flyweight(self, shared_state: Dict) -> Flyweight:
        """
        Returns an existing Flyweight with a given state or creates a new one.
        """

        key = self.get_key(shared_state)

        if not self._flyweights.get(key):
            print("FlyweightFactory: Can't find a flyweight, creating new one.")
            self._flyweights[key] = Flyweight(shared_state)
        else:
            print("FlyweightFactory: Reusing existing flyweight.")

        return self._flyweights[key]

    def list_flyweights(self) -> None:
        count = len(self._flyweights)
        print(f"FlyweightFactory: I have {count} flyweights:")
        print("\n".join(map(str, self._flyweights.keys())), end="")


def add_car_to_police_database(
    factory: FlyweightFactory, plates: str, owner: str,
    brand: str, model: str, color: str
) -> None:
    print("\n\nClient: Adding a car to database.")
    flyweight = factory.get_flyweight([brand, model, color])
    # The client code either stores or calculates extrinsic state and passes it
    # to the flyweight's methods.
    flyweight.operation([plates, owner])


if __name__ == "__main__":
    """
    The client code usually creates a bunch of pre-populated flyweights in the
    initialization stage of the application.
    """

    factory = FlyweightFactory([
        ["Chevrolet", "Camaro2018", "pink"],
        ["Mercedes Benz", "C300", "black"],
        ["Mercedes Benz", "C500", "red"],
        ["BMW", "M5", "red"],
        ["BMW", "X6", "white"],
    ])

    factory.list_flyweights()

    add_car_to_police_database(
        factory, "CL234IR", "James Doe", "BMW", "M5", "red")

    add_car_to_police_database(
        factory, "CL234IR", "James Doe", "BMW", "X1", "red")

    print("\n")

    factory.list_flyweights()
```

- Output
```
FlyweightFactory: I have 5 flyweights:
Camaro2018_Chevrolet_pink
C300_Mercedes Benz_black
C500_Mercedes Benz_red
BMW_M5_red
BMW_X6_white

Client: Adding a car to database.
FlyweightFactory: Reusing existing flyweight.
Flyweight: Displaying shared (["BMW", "M5", "red"]) and unique (["CL234IR", "James Doe"]) state.

Client: Adding a car to database.
FlyweightFactory: Can't find a flyweight, creating new one.
Flyweight: Displaying shared (["BMW", "X1", "red"]) and unique (["CL234IR", "James Doe"]) state.

FlyweightFactory: I have 6 flyweights:
Camaro2018_Chevrolet_pink
C300_Mercedes Benz_black
C500_Mercedes Benz_red
BMW_M5_red
BMW_X6_white
BMW_X1_red
```

- 7. รูปแบบ Proxy
- รูปแบบการออกแบบเชิงโครงสร้าง Proxy จะสร้าง Object ตัวแทนขึ้นมาทำหน้าที่ควบคุมการเข้าถึง Object จริง โดย Proxy สามารถดักจับการเข้าถึง Object จริงไว้ทั้งหมดแทน เพื่อเป็นตัวดำเนินการเพิ่มเติมอื่นๆแทน ไม่ว่าจะเป็นก่อนหรือหลังจากที่ส่งต่อการทำงานไปยัง Object จริง ตัวอย่างการใช้งาน ได้แก่ การควบคุมการเข้าถึง การเก็บข้อมูลไว้ใช้ซ้ำ (caching) การเริ่มใช้งาน Object จริงเมื่อจำเป็นเท่านั้น (lazy initialization) การบันทึกข้อมูล (logging) และการตรวจสอบ (monitoring) เป็นต้น

- องค์ประกอบของ Proxy ประกอบด้วย

- Subject interface ที่กำหนดชุดคำสั่งการทำงานพื้นฐานที่ทั้ง RealSubject และ Proxy ต้องมีใช้งานร่วมกัน เพื่อให้ฝั่ง Client (ผู้ใช้งาน) สามารถใช้ทั้ง Object จริงและ Object Proxy ออกมาได้
- RealSubject นี่คือ Object จริง ที่มีชุดคำสั่งหลักของระบบที่เราต้องการให้มีการควบคุมการเข้าถึง
- Proxy จะมีการเก็บ reference ไปยัง RealSubject ส่วน Proxy นี้มีหน้าที่ควบคุมการเข้าถึงตัว RealSubject ได้หลายรูปแบบ ไม่ว่าจะเป็นส่งต่อคำสั่งให้ RealSubject ทำงาน ไปจนถึงหน่วงเวลาการสร้าง RealSubject (ในกรณี lazy initialization) หรือห้ามเข้าถึงเลยก็ทำได้ นอกจากนี้ Proxy สามารถทำงานอื่นๆ เพิ่มเติมได้ทั้งก่อน และหลัง การติดต่อ RealSubject ด้วยเช่นกัน

- ตัวอย่าง code
```python
from abc import ABC, abstractmethod


class Subject(ABC):
    """
    The Subject interface declares common operations for both RealSubject and
    the Proxy. As long as the client works with RealSubject using this
    interface, you'll be able to pass it a proxy instead of a real subject.
    """

    @abstractmethod
    def request(self) -> None:
        pass


class RealSubject(Subject):
    """
    The RealSubject contains some core business logic. Usually, RealSubjects are
    capable of doing some useful work which may also be very slow or sensitive -
    e.g. correcting input data. A Proxy can solve these issues without any
    changes to the RealSubject's code.
    """

    def request(self) -> None:
        print("RealSubject: Handling request.")


class Proxy(Subject):
    """
    The Proxy has an interface identical to the RealSubject.
    """

    def __init__(self, real_subject: RealSubject) -> None:
        self._real_subject = real_subject

    def request(self) -> None:
        """
        The most common applications of the Proxy pattern are lazy loading,
        caching, controlling the access, logging, etc. A Proxy can perform one
        of these things and then, depending on the result, pass the execution to
        the same method in a linked RealSubject object.
        """

        if self.check_access():
            self._real_subject.request()
            self.log_access()

    def check_access(self) -> bool:
        print("Proxy: Checking access prior to firing a real request.")
        return True

    def log_access(self) -> None:
        print("Proxy: Logging the time of request.", end="")


def client_code(subject: Subject) -> None:
    """
    The client code is supposed to work with all objects (both subjects and
    proxies) via the Subject interface in order to support both real subjects
    and proxies. In real life, however, clients mostly work with their real
    subjects directly. In this case, to implement the pattern more easily, you
    can extend your proxy from the real subject's class.
    """

    # ...

    subject.request()

    # ...


if __name__ == "__main__":
    print("Client: Executing the client code with a real subject:")
    real_subject = RealSubject()
    client_code(real_subject)

    print("")

    print("Client: Executing the same client code with a proxy:")
    proxy = Proxy(real_subject)
    client_code(proxy)

```

- Output
```
Client: Executing the client code with a real subject:
RealSubject: Handling request.

Client: Executing the same client code with a proxy:
Proxy: Checking access prior to firing a real request.
RealSubject: Handling request.
Proxy: Logging the time of request
```


- Design Pattern Behavioral คืออะไร ?
- Design Patterns Behavioral คือรูปแบบการออกแบบพฤติกรรม เป็นรูปแบบการออกแบบที่มุ่งเน้นไปที่ การสื่อสารและความสัมพันธ์ระหว่างวัตถุ (object) ต่างๆ ในระบบ Software รูปแบบเหล่านี้ช่วยให้นักพัฒนา Software สามารถออกแบบระบบที่ยืดหยุ่น เข้าใจง่าย และปรับเปลี่ยนได้ง่าย โดยไม่ต้องเขียน code ใหม่ทั้งหมดได้ ซึ่งใน Behavioral นี้มีทั้งหมด 10 รูปแบบได้แก่

- Chain of Responsibility รูปแบบการออกแบบเชิงพฤติกรรมที่ทำให้เราสามารถส่งต่อ request ต่างๆ ผ่านกลุ่มของตัวจัดการ (handler) โดยเมื่อได้รับ request มาแล้ว ตัวจัดการแต่ละตัวจะตัดสินใจว่าจะดำเนินการตามคำขอนั้นเลย หรือจะส่งต่อไปยังตัวจัดการถัดไปในกลุ่มได้
- Command รูปแบบการออกแบบเชิงพฤติกรรมที่เปลี่ยน request ให้เป็น object แบบ stand-alone ซึ่งภายใน object นั้นจะมีข้อมูลทั้งหมดเกี่ยวกับ request เอาไว้ การเปลี่ยนแปลงนี้ทำให้เราสามารถส่ง request ในรูปแบบของ argument ของ method ได้ รวมถึงสามารถหน่วงเวลาหรือจัดการลำดับการทำงานของ request หรือแม้แต่ยกเลิกคำสั่ง (undo) นั้นได้ด้วย
- Iterator รูปแบบการออกแบบเชิงพฤติกรรมที่ช่วยให้เราสามารถสำรวจข้อมูลใน collection (ชุดข้อมูล) ได้ โดยไม่ต้องรู้โครงสร้างภายในของ collection นั้นว่าเป็นโครงสร้างแบบไหน (เช่น list, stack เป็นต้น)
- Mediator รูปแบบการออกแบบเชิงพฤติกรรมที่ช่วยให้เราลดความยุ่งยากในการพึ่งพากันระหว่าง object ต่างๆ โดยรูปแบบนี้จะจำกัดการสื่อสารโดยตรงระหว่าง Object ด้วยกันเอง และบังคับให้พวกมันทำงานร่วมกันผ่าน Object ตัวกลางที่เรียกว่า “mediator” เท่านั้น
- Memento รูปแบบการออกแบบเชิงพฤติกรรมที่ช่วยให้เราสามารถบันทึกและเรียกคืนสถานะก่อนหน้าของ Object ได้ โดยที่ไม่ต้องเปิดเผยรายละเอียดภายในของการทำงานได้
- Observer รูปแบบการออกแบบเชิงพฤติกรรมที่ให้เราสามารถสร้างกลไกการติดตาม (subscription) เพื่อแจ้งให้ Object หลายๆ ตัวทราบเกี่ยวกับ event ต่างๆที่เกิดขึ้นกับ Object ที่กำลังเฝ้าสังเกตอยู่ได้ (เป็นตัวที่คอยบอกตัวอื่นๆว่าตัวที่เฝ้าสังเกตอยู่มีบางอย่างเกิดขึ้น เพื่อให้จัดการ action ต่อได้)
- State รูปแบบการออกแบบเชิงพฤติกรรมที่ทำให้ Object สามารถเปลี่ยนแปลงการทำงานของตัวเองได้ เมื่อสถานะ (state) ภายในของมันเปลี่ยนไป ซึ่งภายนอกจะดูเหมือนกับว่า Object นั้นได้เปลี่ยนประเภท (class) ของตัวเองออกไปแทน (จัดการ state แบบ class)
- Strategy รูปแบบการออกแบบเชิงพฤติกรรมที่ให้เรากำหนดกลุ่ม algorithm ต่างๆ โดยแยกแต่ละ algorithm ออกเป็น class ของตัวเอง เพื่อให้ Object ที่ใช้ algorithm เหล่านี้สามารถสับเปลี่ยนกันได้
- Template Method รูปแบบการออกแบบเชิงพฤติกรรมที่กำหนดโครงร่างหลักของ algorithm ไว้ใน super class แต่เปิดให้ sub class ต่างๆ สามารถปรับแต่งขั้นตอนเฉพาะภายใน algorithm ของ sub class นั้นๆเองได้ โดยไม่ต้องเปลี่ยนแปลงโครงสร้างโดยรวมของ super class
- Visitor รูปแบบการออกแบบเชิงพฤติกรรมที่ช่วยให้เราแยก algorithm ออกจาก object ที่ algorithm นั้นจะทำงานด้วยอยู่

- รูปแบบ Chain of Responsibility
- Chain of Responsibility pattern เป็น behavioral design pattern ที่อนุญาตให้ object ส่งต่อ request ไปตาม chain ของตัวจัดการ (handler) เมื่อได้รับ request มา handler แต่ละตัวจะมีสิทธิ์ในการตัดสินใจได้ว่ามันจะทำการประมวลผล request นั้นด้วยตัวมันเองเลยหรือจะส่งต่อ request นั้นไปให้กับ handler ตัวต่อไปใน chain ต่อไปเรื่อยๆแทน

- Pattern นี้จะลดการ decouple ระหว่าง ผู้ส่ง request กับตัวที่รับ request ซึ่งเกิดขึ้นด้วยการเปิดโอกาสให้ Object มากกว่าหนึ่งตัวสามารถจัดการกับ request นั้นได้ ส่งเสริมหลักการของ principle of least knowledge ตรงที่ลดการ coupling ระหว่าง Class ต่างๆลงได้

- โครงสร้างหลักของ Chain of Responsibility pattern โดยทั่วไปจะประกอบไปด้วยส่วนประกอบเหล่านี้

- Handler (ผู้จัดการ) ทำหน้าที่นิยามส่วนติดต่อ (Interface) สำหรับจัดการกับ request และในบางกรณีก็จะทำการ implement ความเกี่ยวโยงระหว่าง handler ที่เป็น successor (ตัวที่ต่อกัน) ด้วย โดยที่ handler นี้มีสิทธิ์ที่จะตัดสินใจว่าจะจัดการกับ request ด้วยตัวของมันเอง หรือจะส่งต่อ request ไปให้ handler ตัวถัดไปใน chain ได้
- Concrete Handler (ผู้จัดการแบบเฉพาะเจาะจง) ทำหน้าที่จัดการกับ requests ที่ตัวมันเองมีหน้าที่รับผิดชอบ อีกทั้งยังสามารถเข้าถึง successor ของมันได้อีกด้วย ถ้า Concrete Handler ตัวนั้นสามารถจัดการกับ request ได้มันก็จะทำ อันไหนทำไม่ได้มันก็จะส่งต่อ request นั้นให้ successor ของมันต่อไป
- Client (ผู้ใช้) จะทำการเริ่มต้น request โดยส่งไปที่ Object Concrete Handler ที่เกี่ยวข้องใน chain เข้าไป

```python
from __future__ import annotations
from abc import ABC, abstractmethod
from typing import Any, Optional


class Handler(ABC):
    """
    The Handler interface declares a method for building the chain of handlers.
    It also declares a method for executing a request.
    """

    @abstractmethod
    def set_next(self, handler: Handler) -> Handler:
        pass

    @abstractmethod
    def handle(self, request) -> Optional[str]:
        pass


class AbstractHandler(Handler):
    """
    The default chaining behavior can be implemented inside a base handler
    class.
    """

    _next_handler: Handler = None

    def set_next(self, handler: Handler) -> Handler:
        self._next_handler = handler
        # Returning a handler from here will let us link handlers in a
        # convenient way like this:
        # monkey.set_next(squirrel).set_next(dog)
        return handler

    @abstractmethod
    def handle(self, request: Any) -> str:
        if self._next_handler:
            return self._next_handler.handle(request)

        return None


"""
All Concrete Handlers either handle a request or pass it to the next handler in
the chain.
"""


class MonkeyHandler(AbstractHandler):
    def handle(self, request: Any) -> str:
        if request == "Banana":
            return f"Monkey: I'll eat the {request}"
        else:
            return super().handle(request)


class SquirrelHandler(AbstractHandler):
    def handle(self, request: Any) -> str:
        if request == "Nut":
            return f"Squirrel: I'll eat the {request}"
        else:
            return super().handle(request)


class DogHandler(AbstractHandler):
    def handle(self, request: Any) -> str:
        if request == "MeatBall":
            return f"Dog: I'll eat the {request}"
        else:
            return super().handle(request)


def client_code(handler: Handler) -> None:
    """
    The client code is usually suited to work with a single handler. In most
    cases, it is not even aware that the handler is part of a chain.
    """

    for food in ["Nut", "Banana", "Cup of coffee"]:
        print(f"\nClient: Who wants a {food}?")
        result = handler.handle(food)
        if result:
            print(f"  {result}", end="")
        else:
            print(f"  {food} was left untouched.", end="")


if __name__ == "__main__":
    monkey = MonkeyHandler()
    squirrel = SquirrelHandler()
    dog = DogHandler()

    monkey.set_next(squirrel).set_next(dog)

    # The client should be able to send a request to any handler, not just the
    # first one in the chain.
    print("Chain: Monkey > Squirrel > Dog")
    client_code(monkey)
    print("\n")

    print("Subchain: Squirrel > Dog")
    client_code(squirrel)
```
- Output
```python
Chain: Monkey > Squirrel > Dog

Client: Who wants a Nut?
  Squirrel: I'll eat the Nut
Client: Who wants a Banana?
  Monkey: I'll eat the Banana
Client: Who wants a Cup of coffee?
  Cup of coffee was left untouched.

Subchain: Squirrel > Dog

Client: Who wants a Nut?
  Squirrel: I'll eat the Nut
Client: Who wants a Banana?
  Banana was left untouched.
Client: Who wants a Cup of coffee?
  Cup of coffee was left untouched.
```

- 2.รูปแบบ Command
- Command pattern คือ behavioral design pattern รูปแบบหนึ่งที่เปลี่ยน request ธรรมดา ให้กลายเป็น object แบบ stand-alone ซึ่งภายใน object นั้นจะมีข้อมูลต่างๆ ของ request เก็บเอาไว้ การที่เราแปลงแบบนี้ทำให้เราสามารถใส่ request ต่างๆ เข้าไปใน method, ทำการหน่วงเวลา หรือจัดคิวของ request ได้ รวมถึงยังทำให้เราสามารถมีระบบ undo ที่สามารถย้อนกลับการทำงานได้ด้วย

- การใช้ pattern นี้จะมีประโยชน์อย่างมากในการสร้างระบบ transaction ต่างๆ, การทำ log และ สถานการณ์ที่เราต้องออก request โดยที่เราอาจไม่รู้รายละเอียดของ operation ที่ request นั้นร้องขอ หรือไม่รู้ว่าใครจะเป็น receiver ของ request ตัวนั้น pattern นี้ก็จะสามารถดำเนินการสร้างในรูปแบบ object ออกเป็น request ออกมาก่อนได้

- โดยทั่วไป Command pattern จะมี component หลักๆ ดังนี้

- Command Interface interface ที่มีการประกาศ method ไว้สำหรับ execute command
- Concrete Command เป็นส่วนที่ implement Command interface และมีการนิยามความสัมพันธ์ระหว่าง object Receiver กับ action ต่างๆ
- Client เป็นส่วนที่สร้าง object Concrete Command และทำการกำหนดว่า ใครจะเป็น receiver
- Invoker เป็นส่วนที่บอกให้ command ทำการ execute request
- Receiver เป็นส่วนที่รู้ว่าต้องทำ operation อะไรบ้าง ที่สัมพันธ์กับการทำงานของ request นั้น โดยเราสามารถใช้ class ไหนก็ได้มาเป็น Receiver

- ตัวอย่าง code
```python
from __future__ import annotations
from abc import ABC, abstractmethod


class Command(ABC):
    """
    The Command interface declares a method for executing a command.
    """

    @abstractmethod
    def execute(self) -> None:
        pass


class SimpleCommand(Command):
    """
    Some commands can implement simple operations on their own.
    """

    def __init__(self, payload: str) -> None:
        self._payload = payload

    def execute(self) -> None:
        print(f"SimpleCommand: See, I can do simple things like printing"
              f"({self._payload})")


class ComplexCommand(Command):
    """
    However, some commands can delegate more complex operations to other
    objects, called "receivers."
    """

    def __init__(self, receiver: Receiver, a: str, b: str) -> None:
        """
        Complex commands can accept one or several receiver objects along with
        any context data via the constructor.
        """

        self._receiver = receiver
        self._a = a
        self._b = b

    def execute(self) -> None:
        """
        Commands can delegate to any methods of a receiver.
        """

        print("ComplexCommand: Complex stuff should be done by a receiver object", end="")
        self._receiver.do_something(self._a)
        self._receiver.do_something_else(self._b)


class Receiver:
    """
    The Receiver classes contain some important business logic. They know how to
    perform all kinds of operations, associated with carrying out a request. In
    fact, any class may serve as a Receiver.
    """

    def do_something(self, a: str) -> None:
        print(f"\nReceiver: Working on ({a}.)", end="")

    def do_something_else(self, b: str) -> None:
        print(f"\nReceiver: Also working on ({b}.)", end="")


class Invoker:
    """
    The Invoker is associated with one or several commands. It sends a request
    to the command.
    """

    _on_start = None
    _on_finish = None

    """
    Initialize commands.
    """

    def set_on_start(self, command: Command):
        self._on_start = command

    def set_on_finish(self, command: Command):
        self._on_finish = command

    def do_something_important(self) -> None:
        """
        The Invoker does not depend on concrete command or receiver classes. The
        Invoker passes a request to a receiver indirectly, by executing a
        command.
        """

        print("Invoker: Does anybody want something done before I begin?")
        if isinstance(self._on_start, Command):
            self._on_start.execute()

        print("Invoker: ...doing something really important...")

        print("Invoker: Does anybody want something done after I finish?")
        if isinstance(self._on_finish, Command):
            self._on_finish.execute()


if __name__ == "__main__":
    """
    The client code can parameterize an invoker with any commands.
    """

    invoker = Invoker()
    invoker.set_on_start(SimpleCommand("Say Hi!"))
    receiver = Receiver()
    invoker.set_on_finish(ComplexCommand(
        receiver, "Send email", "Save report"))

    invoker.do_something_important()
```
- Output
```python
Invoker: Does anybody want something done before I begin?
SimpleCommand: See, I can do simple things like printing (Say Hi!)
Invoker: ...doing something really important...
Invoker: Does anybody want something done after I finish?
ComplexCommand: Complex stuff should be done by a receiver object
Receiver: Working on (Send email.)
Receiver: Also working on (Save report.)
```

- 3.รูปแบบ Iterator
- Iterator pattern คือ behavioral design pattern ที่ให้วิธีการเข้าถึง element ต่างๆ ภายใน aggregate object โดยทำทีละตัว (sequentially) และไม่จำเป็นต้องเปิดเผยว่าจริงๆ แล้วข้างในเป็นอย่างไร

- Pattern นี้ทำให้เราสามารถเดินทะลุ (traverse) object นั้นๆ ได้โดยไม่ต้องรู้เลยว่าภายใน object มีการเก็บข้อมูลไว้ในรูปแบบไหน โดยตัว pattern นี้จะทำการแยก algorithm ออกมาจาก operation ที่ทำโดยตัว object ซึ่งทำให้ algorithm เราสามารถทำงานได้โดยไม่ต้องรู้เลยว่า object นั้นจัดเก็บข้อมูลหรือทำงานอย่างไรได้

- ส่วนประกอบหลักๆ ของ Iterator pattern

- Iterator Interface นิยามว่าต้องมีรูปแบบการทำงานอย่างไรบ้าง ซึ่งจะรวมถึง method ไว้สำหรับการเข้าถึง element ณ ตอนนั้น, ย้ายไปที่ element ถัดไป, และเช็คว่ามี element เหลืออยู่ไหม
- Concrete Iterator implement Iterator interface และเป็นส่วนที่คอยเก็บ state ว่าตอนนี้การเดินทางไปถึงไหนแล้ว และมีหน้าที่จัดการตำแหน่งล่าสุดของการทำ iteration
- Aggregate Interface นิยาม interface สำหรับการสร้าง Iterator object
- Concrete Aggregate implement Aggregate interface และเป็นส่วนที่คืนค่า Concrete Iterator ที่สอดคล้องกันออกมา

```python
from __future__ import annotations
from collections.abc import Iterable, Iterator
from typing import Any


"""
To create an iterator in Python, there are two abstract classes from the built-
in `collections` module - Iterable,Iterator. We need to implement the
`__iter__()` method in the iterated object (collection), and the `__next__ ()`
method in theiterator.
"""


class AlphabeticalOrderIterator(Iterator):
    """
    Concrete Iterators implement various traversal algorithms. These classes
    store the current traversal position at all times.
    """

    """
    `_position` attribute stores the current traversal position. An iterator may
    have a lot of other fields for storing iteration state, especially when it
    is supposed to work with a particular kind of collection.
    """
    _position: int = None

    """
    This attribute indicates the traversal direction.
    """
    _reverse: bool = False

    def __init__(self, collection: WordsCollection, reverse: bool = False) -> None:
        self._collection = collection
        self._reverse = reverse
        self._position = -1 if reverse else 0

    def __next__(self) -> Any:
        """
        The __next__() method must return the next item in the sequence. On
        reaching the end, and in subsequent calls, it must raise StopIteration.
        """
        try:
            value = self._collection[self._position]
            self._position += -1 if self._reverse else 1
        except IndexError:
            raise StopIteration()

        return value


class WordsCollection(Iterable):
    """
    Concrete Collections provide one or several methods for retrieving fresh
    iterator instances, compatible with the collection class.
    """

    def __init__(self, collection: list[Any] | None = None) -> None:
        self._collection = collection or []


    def __getitem__(self, index: int) -> Any:
        return self._collection[index]

    def __iter__(self) -> AlphabeticalOrderIterator:
        """
        The __iter__() method returns the iterator object itself, by default we
        return the iterator in ascending order.
        """
        return AlphabeticalOrderIterator(self)

    def get_reverse_iterator(self) -> AlphabeticalOrderIterator:
        return AlphabeticalOrderIterator(self, True)

    def add_item(self, item: Any) -> None:
        self._collection.append(item)


if __name__ == "__main__":
    # The client code may or may not know about the Concrete Iterator or
    # Collection classes, depending on the level of indirection you want to keep
    # in your program.
    collection = WordsCollection()
    collection.add_item("First")
    collection.add_item("Second")
    collection.add_item("Third")

    print("Straight traversal:")
    print("\n".join(collection))
    print("")

    print("Reverse traversal:")
    print("\n".join(collection.get_reverse_iterator()), end="")
```

```python
Straight traversal:
First
Second
Third

Reverse traversal:
Third
Second
First
```


- 4.รูปแบบ Mediator
- Mediator pattern คือ behavioral design pattern ที่จะมาช่วยจัดเตรียม interface แบบรวมศูนย์ สำหรับจัดการชุดของ interfaces อื่นๆ ใน subsystem โดย pattern นี้จะนิยาม object ตัวหนึ่งขึ้นมา เพื่อห่อหุ้ม (encapsulate) ว่าจริงๆ แล้ว object กลุ่มนั้นมีการพูดคุยกันอย่างไรได้บ้าง

- ด้วยวิธีนี้เราจะทำให้เกิดการทำ loose coupling โดยที่ object เหล่านั้นไม่จำเป็นต้องอ้างอิงหากันตรงๆ ซึ่งตัว mediator จะทำหน้าที่เป็นตัวกลางในการควบคุมกลุ่ม object เหล่านั้น ในแง่ว่าจะ interact กันอย่างไรหรือตอนไหนออกมาได้

- ส่วนประกอบหลักของ Mediator pattern มีดังนี้:

- Mediator Interface นิยาม interface ที่ใช้ในการสื่อสารกับ object Colleague ต่างๆ
- Concrete Mediator มีการ implement Mediator interface และทำหน้าที่ประสานงานการสื่อสารระหว่าง object Colleague ด้วยกัน โดยตัวนี้จะรู้จักและเก็บ reference ของ colleagues ต่างๆ เอาไว้
- Colleague (หรือ Participant) นิยาม interface ของการสื่อสารที่ต้องผ่านการจัดการโดย Mediator โดย Colleague แต่ละตัวจะรู้ว่า Mediator ของตัวเองคือใคร
- Concrete Colleague ตัวที่ทำให้ Colleague สามารถสื่อสารหากันได้ (แทนที่จะต้องไปคุยกันเอง)

```python
from __future__ import annotations
from abc import ABC


class Mediator(ABC):
    """
    The Mediator interface declares a method used by components to notify the
    mediator about various events. The Mediator may react to these events and
    pass the execution to other components.
    """

    def notify(self, sender: object, event: str) -> None:
        pass


class ConcreteMediator(Mediator):
    def __init__(self, component1: Component1, component2: Component2) -> None:
        self._component1 = component1
        self._component1.mediator = self
        self._component2 = component2
        self._component2.mediator = self

    def notify(self, sender: object, event: str) -> None:
        if event == "A":
            print("Mediator reacts on A and triggers following operations:")
            self._component2.do_c()
        elif event == "D":
            print("Mediator reacts on D and triggers following operations:")
            self._component1.do_b()
            self._component2.do_c()


class BaseComponent:
    """
    The Base Component provides the basic functionality of storing a mediator's
    instance inside component objects.
    """

    def __init__(self, mediator: Mediator = None) -> None:
        self._mediator = mediator

    @property
    def mediator(self) -> Mediator:
        return self._mediator

    @mediator.setter
    def mediator(self, mediator: Mediator) -> None:
        self._mediator = mediator


"""
Concrete Components implement various functionality. They don't depend on other
components. They also don't depend on any concrete mediator classes.
"""


class Component1(BaseComponent):
    def do_a(self) -> None:
        print("Component 1 does A.")
        self.mediator.notify(self, "A")

    def do_b(self) -> None:
        print("Component 1 does B.")
        self.mediator.notify(self, "B")


class Component2(BaseComponent):
    def do_c(self) -> None:
        print("Component 2 does C.")
        self.mediator.notify(self, "C")

    def do_d(self) -> None:
        print("Component 2 does D.")
        self.mediator.notify(self, "D")


if __name__ == "__main__":
    # The client code.
    c1 = Component1()
    c2 = Component2()
    mediator = ConcreteMediator(c1, c2)

    print("Client triggers operation A.")
    c1.do_a()

    print("\n", end="")

    print("Client triggers operation D.")
    c2.do_d()

```

```python
Client triggers operation A.
Component 1 does A.
Mediator reacts on A and triggers following operations:
Component 2 does C.


Client triggers operation D.
Component 2 does D.
Mediator reacts on D and triggers following operations:
Component 1 does B.
Component 2 does C.
```

- 5.รูปแบบ Memento
- Memento pattern เป็น behavioral design pattern ที่ทำให้เราสามารถเปลี่ยน object ให้กลับไปเป็น state ก่อนหน้าได้ (เหมือน undo หรือ rollback) จุดประสงค์หลักของการใช้ pattern นี้คือการเก็บ (capture) และดึง internal state ของ object ออกมา เพื่อที่เราจะได้เอากลับมาใช้เปลี่ยน object นั้นกลับไปเป็น state นั้นใหม่อีกรอบได้ ในขณะที่เรายังสามารถคงคุณสมบัติ encapsulation ของ OOP เอาไว้ได้เช่นเดิม โดย pattern นี้มีประโยชน์อย่างมากในการทำพวก undo mechanism ใน application ต่างๆได้

- ส่วนประกอบหลักของ Memento pattern มีดังนี้

- Originator object ที่ต้องการจะ save และเรียกคืน (restore) state ตัว Originator จะสร้าง memento ซึ่งจะมี snapshot ของ internal state ณ ตอนนั้นๆ อยู่ข้างใน และใช้เจ้า memento นี้ในการเปลี่ยน state ของตัวเองกลับไปเหมือนเดิม
- Memento object ที่คอยเก็บ state ของ originator เอาไว้ โดยปกติแล้วการที่ structure ข้างในเป็นอย่างไรนั้นจะถูกซ่อนเอาไว้ และจะมีแค่ originator เท่านั้นที่รู้
- Caretaker object ที่คอยเก็บ memento ไว้หลายๆ อัน โดยจะ คอยบันทึก state ของ originator ผ่าน memento แต่มันจะไม่ทำงาน หรือเข้าถึงข้อมูลภายใน memento (มองง่ายๆเหมือน History นั่นแหละ)

```python
from __future__ import annotations
from abc import ABC, abstractmethod
from datetime import datetime
from random import sample
from string import ascii_letters


class Originator:
    """
    The Originator holds some important state that may change over time. It also
    defines a method for saving the state inside a memento and another method
    for restoring the state from it.
    """

    _state = None
    """
    For the sake of simplicity, the originator's state is stored inside a single
    variable.
    """

    def __init__(self, state: str) -> None:
        self._state = state
        print(f"Originator: My initial state is: {self._state}")

    def do_something(self) -> None:
        """
        The Originator's business logic may affect its internal state.
        Therefore, the client should backup the state before launching methods
        of the business logic via the save() method.
        """

        print("Originator: I'm doing something important.")
        self._state = self._generate_random_string(30)
        print(f"Originator: and my state has changed to: {self._state}")

    @staticmethod
    def _generate_random_string(length: int = 10) -> str:
        return "".join(sample(ascii_letters, length))

    def save(self) -> Memento:
        """
        Saves the current state inside a memento.
        """

        return ConcreteMemento(self._state)

    def restore(self, memento: Memento) -> None:
        """
        Restores the Originator's state from a memento object.
        """

        self._state = memento.get_state()
        print(f"Originator: My state has changed to: {self._state}")


class Memento(ABC):
    """
    The Memento interface provides a way to retrieve the memento's metadata,
    such as creation date or name. However, it doesn't expose the Originator's
    state.
    """

    @abstractmethod
    def get_name(self) -> str:
        pass

    @abstractmethod
    def get_date(self) -> str:
        pass


class ConcreteMemento(Memento):
    def __init__(self, state: str) -> None:
        self._state = state
        self._date = str(datetime.now())[:19]

    def get_state(self) -> str:
        """
        The Originator uses this method when restoring its state.
        """
        return self._state

    def get_name(self) -> str:
        """
        The rest of the methods are used by the Caretaker to display metadata.
        """

        return f"{self._date} / ({self._state[0:9]}...)"

    def get_date(self) -> str:
        return self._date


class Caretaker:
    """
    The Caretaker doesn't depend on the Concrete Memento class. Therefore, it
    doesn't have access to the originator's state, stored inside the memento. It
    works with all mementos via the base Memento interface.
    """

    def __init__(self, originator: Originator) -> None:
        self._mementos = []
        self._originator = originator

    def backup(self) -> None:
        print("\nCaretaker: Saving Originator's state...")
        self._mementos.append(self._originator.save())

    def undo(self) -> None:
        if not len(self._mementos):
            return

        memento = self._mementos.pop()
        print(f"Caretaker: Restoring state to: {memento.get_name()}")
        try:
            self._originator.restore(memento)
        except Exception:
            self.undo()

    def show_history(self) -> None:
        print("Caretaker: Here's the list of mementos:")
        for memento in self._mementos:
            print(memento.get_name())


if __name__ == "__main__":
    originator = Originator("Super-duper-super-puper-super.")
    caretaker = Caretaker(originator)

    caretaker.backup()
    originator.do_something()

    caretaker.backup()
    originator.do_something()

    caretaker.backup()
    originator.do_something()

    print()
    caretaker.show_history()

    print("\nClient: Now, let's rollback!\n")
    caretaker.undo()

    print("\nClient: Once more!\n")
    caretaker.undo()
```

```python
Originator: My initial state is: Super-duper-super-puper-super.

Caretaker: Saving Originator's state...
Originator: I'm doing something important.
Originator: and my state has changed to: wQAehHYOqVSlpEXjyIcgobrxsZUnat

Caretaker: Saving Originator's state...
Originator: I'm doing something important.
Originator: and my state has changed to: lHxNORKcsgMWYnJqoXjVCbQLEIeiSp

Caretaker: Saving Originator's state...
Originator: I'm doing something important.
Originator: and my state has changed to: cvIYsRilNOtwynaKdEZpDCQkFAXVMf

Caretaker: Here's the list of mementos:
2019-01-26 21:11:24 / (Super-dup...)
2019-01-26 21:11:24 / (wQAehHYOq...)
2019-01-26 21:11:24 / (lHxNORKcs...)

Client: Now, let's rollback!

Caretaker: Restoring state to: 2019-01-26 21:11:24 / (lHxNORKcs...)
Originator: My state has changed to: lHxNORKcsgMWYnJqoXjVCbQLEIeiSp

Client: Once more!

Caretaker: Restoring state to: 2019-01-26 21:11:24 / (wQAehHYOq...)
Originator: My state has changed to: wQAehHYOqVSlpEXjyIcgobrxsZUnat
```

- 6. รูปแบบ Observer
- Observer pattern เป็น behavioral design pattern โดยจะมี object หนึ่งตัวเป็น subject คอยเก็บ list ของตัว observer ไว้ เวลาที่มีการเปลี่ยนแปลง state ใดๆ subject จะทำการแจ้ง (notify) ไปยัง observers ทั้งหมดแบบอัตโนมัติ (โดยปกติแล้ววิธีการแจ้งจะเป็นการเรียก method ของ observers นั้นๆ ซึ่งนี่ถือเป็นรูปแบบพื้นฐานของ publish-subscribe เลยก็ว่าได้) เพื่อให้สามารถรับรู้ (observe) และตอบสนองกับเหตุการณ์ (event) ใน object อื่นๆ โดยที่ทั้งหมดนี้เราไม่จำเป็นต้องมา coupling ระหว่าง object เหล่านั้นเลยได้ (ต่างคนต่างจัดการแค่คุยผ่านสัญญาณออกมาพอ)

- ส่วนประกอบหลักของ Observer pattern มีดังนี้

- Subject เป็นตัวเก็บ list ของ observers ไว้ และจะมี method ไว้เพิ่ม ลบ และแจ้ง observers
- Observer จะเป็น interface หรือ abstract class ที่นิยาม method (ชื่อ update) เอาไว้ โดย update method นี้จะถูก subject เรียกเพื่อแจ้ง observers เวลามี state เปลี่ยน
- Concrete Subject จะ implement subject interface และเก็บ state ของตัวเอง ซึ่งในตอนที่มีการเปลี่ยนแปลง state นั้นเองที่จะมีการแจ้งไปยัง observers ทั้งหมด
- Concrete Observer จะ implement observer interface และเก็บ reference ของ subject เอาไว้ เพื่อที่ว่าตัวมันเองจะ update ตัวเองได้แบบอัตโนมัติ ตอนได้รับแจ้งว่า state มีการเปลี่ยนแปลง

```python
from __future__ import annotations
from abc import ABC, abstractmethod
from random import randrange
from typing import List


class Subject(ABC):
    """
    The Subject interface declares a set of methods for managing subscribers.
    """

    @abstractmethod
    def attach(self, observer: Observer) -> None:
        """
        Attach an observer to the subject.
        """
        pass

    @abstractmethod
    def detach(self, observer: Observer) -> None:
        """
        Detach an observer from the subject.
        """
        pass

    @abstractmethod
    def notify(self) -> None:
        """
        Notify all observers about an event.
        """
        pass


class ConcreteSubject(Subject):
    """
    The Subject owns some important state and notifies observers when the state
    changes.
    """

    _state: int = None
    """
    For the sake of simplicity, the Subject's state, essential to all
    subscribers, is stored in this variable.
    """

    _observers: List[Observer] = []
    """
    List of subscribers. In real life, the list of subscribers can be stored
    more comprehensively (categorized by event type, etc.).
    """

    def attach(self, observer: Observer) -> None:
        print("Subject: Attached an observer.")
        self._observers.append(observer)

    def detach(self, observer: Observer) -> None:
        self._observers.remove(observer)

    """
    The subscription management methods.
    """

    def notify(self) -> None:
        """
        Trigger an update in each subscriber.
        """

        print("Subject: Notifying observers...")
        for observer in self._observers:
            observer.update(self)

    def some_business_logic(self) -> None:
        """
        Usually, the subscription logic is only a fraction of what a Subject can
        really do. Subjects commonly hold some important business logic, that
        triggers a notification method whenever something important is about to
        happen (or after it).
        """

        print("\nSubject: I'm doing something important.")
        self._state = randrange(0, 10)

        print(f"Subject: My state has just changed to: {self._state}")
        self.notify()


class Observer(ABC):
    """
    The Observer interface declares the update method, used by subjects.
    """

    @abstractmethod
    def update(self, subject: Subject) -> None:
        """
        Receive update from subject.
        """
        pass


"""
Concrete Observers react to the updates issued by the Subject they had been
attached to.
"""


class ConcreteObserverA(Observer):
    def update(self, subject: Subject) -> None:
        if subject._state < 3:
            print("ConcreteObserverA: Reacted to the event")


class ConcreteObserverB(Observer):
    def update(self, subject: Subject) -> None:
        if subject._state == 0 or subject._state >= 2:
            print("ConcreteObserverB: Reacted to the event")


if __name__ == "__main__":
    # The client code.

    subject = ConcreteSubject()

    observer_a = ConcreteObserverA()
    subject.attach(observer_a)

    observer_b = ConcreteObserverB()
    subject.attach(observer_b)

    subject.some_business_logic()
    subject.some_business_logic()

    subject.detach(observer_a)

    subject.some_business_logic()
```

```python
Subject: Attached an observer.
Subject: Attached an observer.

Subject: I'm doing something important.
Subject: My state has just changed to: 0
Subject: Notifying observers...
ConcreteObserverA: Reacted to the event
ConcreteObserverB: Reacted to the event

Subject: I'm doing something important.
Subject: My state has just changed to: 5
Subject: Notifying observers...
ConcreteObserverB: Reacted to the event

Subject: I'm doing something important.
Subject: My state has just changed to: 0
Subject: Notifying observers...
ConcreteObserverB: Reacted to the event
```

- 7. รูปแบบ State
- State pattern เป็น behavioral design pattern ที่จะทำให้ object หนึ่งมีความสามารถในการเปลี่ยนแปลงพฤติกรรม เมื่อ internal state ของมันเปลี่ยน การเปลี่ยนแปลงนี้ ถ้าดูจากภายนอกแล้วจะเหมือนกับว่า object ตัวนั้นเปลี่ยน class ของมันไปเลยก็ว่าได้

- จุดเด่นของ pattern นี้คือจะห่อหุ้ม (encapsulate) พฤติกรรมต่างๆ ของ function ชุดหนึ่งๆเอาไว้ให้ขึ้นกับชนิดของ state object ซึ่งก็คือตัวแทนของ state ณ ตอนนั้นๆ และสิ่งนี้เองที่ทำให้พฤติกรรมของ object สามารถเปลี่ยนแปลงได้แบบ dynamic ตาม state ออกมาได้

- ส่วนประกอบหลักของ State pattern มีดังนี้

- Context เป็นตัวเก็บ instance ของ ConcreteState subclass ซึ่งจะนิยามว่าตอนนี้ state เป็นอะไร
- State Interface เป็นตัวนิยาม interface ที่ไว้ห่อหุ้มพฤติกรรมต่างๆ ที่สัมพันธ์กับ state นั้นๆ ของ Context
- Concrete States implement State interface และจะมีการใส่ logic เข้าไป เพื่อให้ได้ action เฉพาะเจาะจงออกมา ซึ่งจะเห็นได้ว่าพฤติกรรมของ Context object นั้นจะเปลี่ยนไปตาม state object ที่เปลี่ยนแปลง

```python
from __future__ import annotations
from abc import ABC, abstractmethod


class Context:
    """
    The Context defines the interface of interest to clients. It also maintains
    a reference to an instance of a State subclass, which represents the current
    state of the Context.
    """

    _state = None
    """
    A reference to the current state of the Context.
    """

    def __init__(self, state: State) -> None:
        self.transition_to(state)

    def transition_to(self, state: State):
        """
        The Context allows changing the State object at runtime.
        """

        print(f"Context: Transition to {type(state).__name__}")
        self._state = state
        self._state.context = self

    """
    The Context delegates part of its behavior to the current State object.
    """

    def request1(self):
        self._state.handle1()

    def request2(self):
        self._state.handle2()


class State(ABC):
    """
    The base State class declares methods that all Concrete State should
    implement and also provides a backreference to the Context object,
    associated with the State. This backreference can be used by States to
    transition the Context to another State.
    """

    @property
    def context(self) -> Context:
        return self._context

    @context.setter
    def context(self, context: Context) -> None:
        self._context = context

    @abstractmethod
    def handle1(self) -> None:
        pass

    @abstractmethod
    def handle2(self) -> None:
        pass


"""
Concrete States implement various behaviors, associated with a state of the
Context.
"""


class ConcreteStateA(State):
    def handle1(self) -> None:
        print("ConcreteStateA handles request1.")
        print("ConcreteStateA wants to change the state of the context.")
        self.context.transition_to(ConcreteStateB())

    def handle2(self) -> None:
        print("ConcreteStateA handles request2.")


class ConcreteStateB(State):
    def handle1(self) -> None:
        print("ConcreteStateB handles request1.")

    def handle2(self) -> None:
        print("ConcreteStateB handles request2.")
        print("ConcreteStateB wants to change the state of the context.")
        self.context.transition_to(ConcreteStateA())


if __name__ == "__main__":
    # The client code.

    context = Context(ConcreteStateA())
    context.request1()
    context.request2()
```

```python
Context: Transition to ConcreteStateA
ConcreteStateA handles request1.
ConcreteStateA wants to change the state of the context.
Context: Transition to ConcreteStateB
ConcreteStateB handles request2.
ConcreteStateB wants to change the state of the context.
Context: Transition to ConcreteStateA
```

- 8. รูปแบบ Strategy
- Strategy pattern เป็น behavioral design pattern ที่ทำให้เราสามารถเลือกพฤติกรรมของ algorithm ตอน runtime ได้ โดยที่แทนที่เราจะ implement algorithm โดยตรง code strategry สามารถทำให้ code ได้รับ instruction ตอน runtime ว่าจะต้องใช้ algorithm ไหนในกลุ่มของ algorithms ทั้งหมดที่เรามีได้ (อารมณ์เตรียมวิธีการแต่ละแบบเอาไว้ แต่เรียกใช้จริงเป็นแบบไหนก็ขึ้นอยู่กับ case ตอนนั้น)

- Pattern นี้จะนิยามกลุ่ม (family) ของ algorithms แล้วทำการห่อหุ้ม (encapsulates) แต่ละแบบแยกจากกัน และทำให้สามารถสลับเปลี่ยนกันได้ภายในกลุ่มเดียวกัน ซึ่งจุดเด่นของ Strategy ก็คือจะทำให้ algorithm ของเรานั้นเป็นอิสระจาก clients ที่ใช้มันอยู่ได้

- ส่วนประกอบหลักของ Strategy pattern มีดังนี้

- Context เป็นตัวที่จะเก็บ reference ที่ชี้ไปยัง concrete strategies ตัวหนึ่งๆ และ Context ตัวนี้จะติดต่อกับ strategy ที่มันชี้ไปถึงอยู่ ผ่าน strategy interface เท่านั้น
- Strategy Interface เป็นตัวประกาศว่า algorithms อื่นๆ จะต้องมี interface แบบนี้ ซึ่ง Context จะใช้อันนี้ในการเรียก algorithm ที่นิยามไว้ใน Concrete Strategy
- Concrete Strategies implement strategy interface และทำหน้าที่ implement ตัว algorithm จริงๆ เวลาที่ Context ต้องการใช้ algorithm ไหน จะต้องมาเรียกพวก concrete strategy ให้จัดเตรียมการทำงานของ logic ข้างในให้เรียบร้อย

```python
from __future__ import annotations
from abc import ABC, abstractmethod
from typing import List


class Context():
    """
    The Context defines the interface of interest to clients.
    """

    def __init__(self, strategy: Strategy) -> None:
        """
        Usually, the Context accepts a strategy through the constructor, but
        also provides a setter to change it at runtime.
        """

        self._strategy = strategy

    @property
    def strategy(self) -> Strategy:
        """
        The Context maintains a reference to one of the Strategy objects. The
        Context does not know the concrete class of a strategy. It should work
        with all strategies via the Strategy interface.
        """

        return self._strategy

    @strategy.setter
    def strategy(self, strategy: Strategy) -> None:
        """
        Usually, the Context allows replacing a Strategy object at runtime.
        """

        self._strategy = strategy

    def do_some_business_logic(self) -> None:
        """
        The Context delegates some work to the Strategy object instead of
        implementing multiple versions of the algorithm on its own.
        """

        # ...

        print("Context: Sorting data using the strategy (not sure how it'll do it)")
        result = self._strategy.do_algorithm(["a", "b", "c", "d", "e"])
        print(",".join(result))

        # ...


class Strategy(ABC):
    """
    The Strategy interface declares operations common to all supported versions
    of some algorithm.

    The Context uses this interface to call the algorithm defined by Concrete
    Strategies.
    """

    @abstractmethod
    def do_algorithm(self, data: List):
        pass


"""
Concrete Strategies implement the algorithm while following the base Strategy
interface. The interface makes them interchangeable in the Context.
"""


class ConcreteStrategyA(Strategy):
    def do_algorithm(self, data: List) -> List:
        return sorted(data)


class ConcreteStrategyB(Strategy):
    def do_algorithm(self, data: List) -> List:
        return reversed(sorted(data))


if __name__ == "__main__":
    # The client code picks a concrete strategy and passes it to the context.
    # The client should be aware of the differences between strategies in order
    # to make the right choice.

    context = Context(ConcreteStrategyA())
    print("Client: Strategy is set to normal sorting.")
    context.do_some_business_logic()
    print()

    print("Client: Strategy is set to reverse sorting.")
    context.strategy = ConcreteStrategyB()
    context.do_some_business_logic()
```

```python
Client: Strategy is set to normal sorting.
Context: Sorting data using the strategy (not sure how it'll do it)
a,b,c,d,e

Client: Strategy is set to reverse sorting.
Context: Sorting data using the strategy (not sure how it'll do it)
e,d,c,b,a
```

- 9.รูปแบบ Template Method
- Template Method pattern นั้นเป็น behavioral design pattern ที่เป็นตัวกำหนดโครงสร้าง (skeleton) ของ algorithm โดยโครงสร้างนี้จะอยู่ใน superclass แต่จะทำให้ subclasses สามารถแก้ไข (override) บางขั้นตอนที่เฉพาะเจาะจงใน algorithm นั้นได้ โดยที่จะไม่ไปเปลี่ยนแปลงโครงสร้างทั้งหมดออกมาได้

- การใช้งานนี้ดีตรงที่เราจะสามารถนำ algorithm ตัวเดิมที่ไม่ได้ขึ้นตรงกับ Class โดยตรงกลับมาใช้ใหม่ได้ และมั่นใจว่าโครงสร้างทั้งหมดจะยังคงเหมือนเดิมได้ ในขณะที่เราสามารถปล่อยให้ subclasses นั้นๆ เข้ามาสร้างพฤติกรรมที่ตรงกับแต่ละขั้นตอนเพิ่มเติมได้

- ส่วนประกอบหลักของ Template Method pattern มีดังนี้

- Abstract Class (Template) จะนิยาม abstract methods ไว้สำหรับขั้นตอนต่างๆ ที่จะต้องมีใน algorithm นอกจากนี้ยังต้องมีการ implement template method ไว้ด้วยเพื่อกำหนดโครงสร้าง (skeleton) ของ algorithm ซึ่งจะมีการเรียก abstract methods ต่างๆ ที่ subclass จะต้องไป implement
- Concrete Classes ทำการ implement abstract methods ต่างๆ ที่อยู่ใน superclass เพื่อเพิ่มการทำงานจริงที่อยู่ในแต่ละขั้นตอนของ algorithm เข้าไปได้ โดยที่โครงสร้างทั้งหมดและลำดับขั้นตอนจะถูกควบคุมอยู่ที่ superclass แทน

```python
from abc import ABC, abstractmethod


class AbstractClass(ABC):
    """
    The Abstract Class defines a template method that contains a skeleton of
    some algorithm, composed of calls to (usually) abstract primitive
    operations.

    Concrete subclasses should implement these operations, but leave the
    template method itself intact.
    """

    def template_method(self) -> None:
        """
        The template method defines the skeleton of an algorithm.
        """

        self.base_operation1()
        self.required_operations1()
        self.base_operation2()
        self.hook1()
        self.required_operations2()
        self.base_operation3()
        self.hook2()

    # These operations already have implementations.

    def base_operation1(self) -> None:
        print("AbstractClass says: I am doing the bulk of the work")

    def base_operation2(self) -> None:
        print("AbstractClass says: But I let subclasses override some operations")

    def base_operation3(self) -> None:
        print("AbstractClass says: But I am doing the bulk of the work anyway")

    # These operations have to be implemented in subclasses.

    @abstractmethod
    def required_operations1(self) -> None:
        pass

    @abstractmethod
    def required_operations2(self) -> None:
        pass

    # These are "hooks." Subclasses may override them, but it's not mandatory
    # since the hooks already have default (but empty) implementation. Hooks
    # provide additional extension points in some crucial places of the
    # algorithm.

    def hook1(self) -> None:
        pass

    def hook2(self) -> None:
        pass


class ConcreteClass1(AbstractClass):
    """
    Concrete classes have to implement all abstract operations of the base
    class. They can also override some operations with a default implementation.
    """

    def required_operations1(self) -> None:
        print("ConcreteClass1 says: Implemented Operation1")

    def required_operations2(self) -> None:
        print("ConcreteClass1 says: Implemented Operation2")


class ConcreteClass2(AbstractClass):
    """
    Usually, concrete classes override only a fraction of base class'
    operations.
    """

    def required_operations1(self) -> None:
        print("ConcreteClass2 says: Implemented Operation1")

    def required_operations2(self) -> None:
        print("ConcreteClass2 says: Implemented Operation2")

    def hook1(self) -> None:
        print("ConcreteClass2 says: Overridden Hook1")


def client_code(abstract_class: AbstractClass) -> None:
    """
    The client code calls the template method to execute the algorithm. Client
    code does not have to know the concrete class of an object it works with, as
    long as it works with objects through the interface of their base class.
    """

    # ...
    abstract_class.template_method()
    # ...


if __name__ == "__main__":
    print("Same client code can work with different subclasses:")
    client_code(ConcreteClass1())
    print("")

    print("Same client code can work with different subclasses:")
    client_code(ConcreteClass2())
```

```python
Same client code can work with different subclasses:
AbstractClass says: I am doing the bulk of the work
ConcreteClass1 says: Implemented Operation1
AbstractClass says: But I let subclasses override some operations
ConcreteClass1 says: Implemented Operation2
AbstractClass says: But I am doing the bulk of the work anyway

Same client code can work with different subclasses:
AbstractClass says: I am doing the bulk of the work
ConcreteClass2 says: Implemented Operation1
AbstractClass says: But I let subclasses override some operations
ConcreteClass2 says: Overridden Hook1
ConcreteClass2 says: Implemented Operation2
AbstractClass says: But I am doing the bulk of the work anyway
```
