# 1 System Summary

Canteen SmartCard System is a cashless payment system that used in xxx canteen

## 1.1 Functional Summary

- A SmartCard is issued to every consumer in the system.
- Consumer recharge the credit in the Management Center
- Administrator of Management Center manage the card holders' balance and identity.

## 1.2 Non-functional Summary

- Data backup is required in case of system failure.

# 2 Use Cases

## 2.1 Management Center

- A customer can register an account in the system.
- Customer can recharge his/her balance by Credit Card or Cash
- A administrator can mange customer profile
- A administrator can query customer transactions
- A administrator can charge customer by credit card to the canteen's bank account.
- A administrator can charge customer by cash.


```plantuml
@startuml
left to right direction
actor "Customer" as customer
actor "Administrator" as administrator
package "Management Centre" {
  usecase "Register" as UC_Register
  usecase "Recharge Credit" as UC_RechargeCredit
  usecase "Manage Customer Profile" as UC_MangeCustomerProfile
  usecase "Query Transcations" as UC_QueryTranscations
  usecase "Restore Backup" as UC_RestoreBackup
}
package "Bank Account" {
  usecase "CreditCard Payment" as UC_CreditCardPayment
}

package "Casher" {
  usecase "Cash Payment" as UC_CashPayment
}


customer --> UC_Register
customer --> UC_RechargeCredit
administrator --> UC_MangeCustomerProfile
administrator --> UC_CreditCardPayment
administrator --> UC_CashPayment
administrator --> UC_QueryTranscations
administrator --> UC_RestoreBackup
@enduml

```

## 2.2 Canteen

- Customer purchase the meal
- Canteen staff input the amount of the Meal
- Canteen staff scan customer's smart card

```plantuml
@startuml
left to right direction
actor "Customer" as customer
actor "Canteen Staff" as staff
package "Canteen" {
  usecase "Input Amount" as UC_InputAmount
  usecase "Scan SmartCard" as UC_ScanSmartCard
  usecase "Purchase Meal" as UC_PurchaseMeal
}

staff --> UC_InputAmount
staff --> UC_ScanSmartCard
customer --> UC_PurchaseMeal
@enduml

```

# 3 System deployment and overall design


## 3.1 Deployment Diagram

```plantuml
@startuml
cloud External {
  actor "Administrator" as administrator
  component "CardReader" as card_reader
}

frame "Canteen System" {
  node "Application" as app
  database "Database" as db
}

frame "OffSite Backup" {
  storage "Backup" as storage
}

card_reader --> app
administrator --> app
app --> db
db --> storage
@enduml

```

## 3.2 Management Center Sequence diagram

### 3.2.1 Open new account

```plantuml
@startuml
actor Customer
actor Administrator
entity CardReader as reader
collections "Canteen System" as app
Customer -> Administrator : To Register
Administrator -> app : Create New Account
reader -> app : Link SmartCard Serial No.
Administrator -> Customer : Give SmartCard
@enduml
```

### 3.2.2 Customer recharge credit

```plantuml
@startuml
actor Customer
actor Administrator
entity "POS terminal" as pos
collections "Canteen System" as app
Customer -> Administrator : Present SmartCard
Customer -> Administrator : Make Payment
pos -> app : retrieve user account
Administrator -> app : Increase balance
@enduml
```

## 3.3 Canteen Sequence diagram

```plantuml
@startuml
actor Customer
actor Staff
entity "POS terminal" as pos
collections "Canteen System" as app
Customer -> Staff : Present SmartCard
Staff -> pos : Scan SmartCard
pos -> app : Request Balance
app -> pos : Return Balance
Staff -> pos : Enter Amount
pos -> app : Deduct Credit
Staff -> Customer : Return SmartCard
@enduml
```

# 4 Class Diagram

```plantuml
@startuml
class User {
  + username
  + passwordHash
  + firstName
  + lastName
  + email
}

class Customer {
  + firstName
  + lastName
  + getBalance()
}

class SmartCard {
  + serialNumber
  + customerId
  + Balance
}

class Transcations {
  + dateTime
  + type
  + smartCardId
  + userId
  + Amount
}

SmartCard "1" --> "1" Customer
SmartCard "1" --> "many" Transcations
@enduml
```



