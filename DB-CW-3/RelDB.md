# Логічна схема БД реляційної моделі даних

## Дисципліна: «Організація баз даних та знань»
### Контрольне завдання №3 (Завдання 1 та 2)

**Предметна область:** База даних меблевого магазину  

Логічна схема реляційної моделі даних розроблена на основі UML-діаграми концептуальних класів попереднього етапу проєктування. У схемі визначено сутності (таблиці), атрибути з типами даних, первинні ключі (`PK`), зовнішні ключі (`FK`) та зв'язки між таблицями відповідно до вимог реляційної цілісності.

```mermaid
erDiagram
    Client {
        client_id integer PK
        full_name string
        phone string
        address string
    }

    Employee {
        employee_id integer PK
        full_name string
        position string
        qualification string
        phone string
    }

    Supplier {
        supplier_id integer PK
        name string
        contact_person string
        phone string
        address string
        supply_terms string
    }

    Manufacturer {
        manufacturer_id integer PK
        name string
        country string
        contacts string
    }

    Furniture {
        furniture_id integer PK
        name string
        category string
        material string
        color string
        dimensions string
        price integer
        availability_status string
        production_time integer
        manufacturer_id integer FK
        supplier_id integer FK
    }

    Orders {
        order_id integer PK
        order_date date
        execution_status string
        delivery_address string
        total_amount integer
        client_id integer FK
        employee_id integer FK
    }

    OrderItem {
        order_item_id integer PK
        order_id integer FK
        furniture_id integer FK
        quantity integer
        item_price integer
    }

    Contract {
        contract_id integer PK
        contract_date date
        terms string
        order_id integer FK
    }

    Receipt {
        receipt_id integer PK
        payment_date date
        amount integer
        order_id integer FK
    }

    Client ||--o{ Orders : ""
    Employee ||--o{ Orders : ""
    Manufacturer ||--o{ Furniture : ""
    Supplier ||--o{ Furniture : ""
    Orders ||--o{ OrderItem : ""
    Furniture ||--o{ OrderItem : ""
    Orders ||--o{ Contract : ""
    Orders ||--o{ Receipt : ""
```

---

### Опис таблиць та зв'язків:
1. **`Client` (Клієнти):** зберігає інформацію про покупців. Зв'язок один-до-багатьох із `Orders` (`client_id`).
2. **`Employee` (Співробітники):** зберігає дані про персонал магазину (менеджерів, адміністраторів). Зв'язок один-до-багатьох із `Orders` (`employee_id`).
3. **`Manufacturer` (Виробники):** фабрики меблів. Зв'язок один-до-багатьох із `Furniture` (`manufacturer_id`).
4. **`Supplier` (Постачальники):** постачальники матеріалів та фурнітури. Зв'язок один-до-багатьох із `Furniture` (`supplier_id`).
5. **`Furniture` (Меблі / Товари):** каталог виробів із характеристиками, вартістю, статусом наявності та термінами виготовлення.
6. **`Orders` (Замовлення):** замовлення клієнтів із прив'язкою до клієнта та відповідального співробітника.
7. **`OrderItem` (Позиції замовлення):** таблиця зв'язку багато-до-багатьох між замовленнями та меблями, що фіксує кількість та ціну одиниці на момент покупки.
8. **`Contract` (Договори):** юридичні договори купівлі-продажу для замовлень.
9. **`Receipt` (Квитанції):** розрахункові квитанції про оплату замовлень.
