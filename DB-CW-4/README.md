# Контрольне завдання №4: Проектування логічної схеми БД ієрархічної моделі даних

## Дисципліна: «Організація баз даних та знань»

### Інформація про роботу
- **Тема:** Побудова логічної схеми БД ієрархічної моделі даних на основі UML-діаграми концептуальних класів через зв'язки між вузлами-класами та вузлами-атрибутами.
- **Предметна область:** База даних меблевого магазину.
- **Студент:** Велієва Л.А., група АІ-253.
- **Термін виконання:** до 8 листопада 2026 року включно.

---

## Зміст каталогу `DB-CW-4`

1. 📄 [`Tree-Model.md`](./Tree-Model.md) — **Завдання 1 та 2:** Логічна схема БД ієрархічної моделі даних, описана мовою розмітки `Mermaid` (`graph TD`), специфікація вузлів-класів і вузлів-атрибутів та обґрунтування правил ієрархічної організації.
2. 📄 [`README.md`](./README.md) — загальний звіт про виконання завдань, опис етапів переходу від концептуальної моделі до ієрархічної та реквізити запиту Pull Request.

---

## Завдання 1 та 2. Проєктування та Mermaid-опис ієрархічної моделі

### 1. Перехід від концептуальної моделі (UML) до ієрархічної моделі даних

На попередньому етапі (`DB-CW-2`) було побудовано UML-діаграму концептуальних класів. При переході до ієрархічної моделі даних враховано ключові принципи організації ієрархічних БД:
- **Деревовидна топологія:** дані організуються у формі орієнтованого кореневого дерева;
- **Корінь дерева (`root`):** кореневим об'єктом обрано `CLIENT[Client]` (Клієнт), навколо якого будується ланцюг взаємодій у меблевому магазині;
- **Відношення «батько-нащадок» (Parent–Child):**
  - Будь-який `child`-вузол має строго **одного** `parent`-вузла;
  - Кожен `parent`-вузол може мати **довільну кількість** `child`-вузлів (1:N);
- **Розподіл вузлів:**
  - **Вузли-класи (прямокутники `[...]`):** `Client`, `Order`, `Contract`, `Receipt`, `Manager`, `Furniture`, `Manufacturer`, `Supplier`;
  - **Вузли-атрибути (кола `((...))`):** підпорядковані своїм класам як кінцеві властивості (описи вузлів).

---

### 2. Діаграма ієрархічної моделі даних мовою Mermaid

Повний опис схеми розміщено у файлі [`Tree-Model.md`](./Tree-Model.md):

```mermaid
graph TD
  %% ===== Ієрархічна модель: Client → Order → Furniture → (Manufacturer, Supplier) =====

  %% Root
  CLIENT[Client]
  CLIENT --> c_fullname((FullName))
  CLIENT --> c_phone((Phone))
  CLIENT --> c_address((Address))

  %% Order (child of Client)
  CLIENT --> ORDER[Order]
  ORDER --> o_orderdate((OrderDate))
  ORDER --> o_executionstatus((ExecutionStatus))
  ORDER --> o_deliveryaddress((DeliveryAddress))
  ORDER --> o_totalamount((TotalAmount))

  %% Contract (child of Order)
  ORDER --> CONTRACT[Contract]
  CONTRACT --> cnt_contractdate((ContractDate))
  CONTRACT --> cnt_terms((Terms))

  %% Receipt (child of Order)
  ORDER --> RECEIPT[Receipt]
  RECEIPT --> rcp_paymentdate((PaymentDate))
  RECEIPT --> rcp_amount((Amount))

  %% Manager (child of Order)
  ORDER --> MANAGER[Manager]
  MANAGER --> m_fullname((FullName))
  MANAGER --> m_phone((Phone))
  MANAGER --> m_position((Position))
  MANAGER --> m_qualification((Qualification))

  %% Furniture (child of Order)
  ORDER --> FURNITURE[Furniture]
  FURNITURE --> f_name((Name))
  FURNITURE --> f_category((Category))
  FURNITURE --> f_material((Material))
  FURNITURE --> f_color((Color))
  FURNITURE --> f_dimensions((Dimensions))
  FURNITURE --> f_price((Price))
  FURNITURE --> f_availabilitystatus((AvailabilityStatus))
  FURNITURE --> f_productiontime((ProductionTime))

  %% Manufacturer (child of Furniture)
  FURNITURE --> MANUFACTURER[Manufacturer]
  MANUFACTURER --> mfr_name((Name))
  MANUFACTURER --> mfr_country((Country))
  MANUFACTURER --> mfr_contacts((Contacts))

  %% Supplier (child of Furniture)
  FURNITURE --> SUPPLIER[Supplier]
  SUPPLIER --> sup_name((Name))
  SUPPLIER --> sup_contactperson((ContactPerson))
  SUPPLIER --> sup_phone((Phone))
  SUPPLIER --> sup_address((Address))
  SUPPLIER --> sup_supplyterms((SupplyTerms))
```

---

## Завдання 3. Процес створення Pull Request (Code Review)

Для проходження процедури рецензування (Code Review) виконано запит на злиття змін до основної гілки репозиторію з такими встановленими параметрами:
- **Title (Name):** `DB-CW-4`
- **Reviewers:** `Oleksandr Blazhko` (`oleksandrblazhko`)
- **Labels:** `documentation`

> **Важлива примітка:** Злиття гілки (`Merge pull request`) самостійно не виконується — відповідно до правил регламенту це здійснює викладач після перевірки та погодження змін.
