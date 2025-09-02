# Chain of Responsibility Design Pattern in Java

## Overview

The **Chain of Responsibility Pattern** is a **behavioral design pattern** that allows a request to be passed along a chain of handlers. Each handler decides either to process the request or to pass it to the next handler in the chain.  

This pattern decouples the **sender** of a request from its **receivers**, giving multiple objects the chance to handle the request.

---

## Key Points

- A **request flows through a chain** of handlers.
- Each handler decides if it can **handle the request**.
- If not, it **forwards** the request to the next handler.
- Promotes the **Open/Closed Principle** by allowing new handlers without modifying existing code.

---

## Real-world Example

Consider **payment processing**:

1. **Bank Account** can handle payments up to **$500**.  
2. **Credit Card** can handle payments up to **$1000**.  
3. **PayPal** can handle payments up to **$1500**.  
4. If no handler can process the request, it is **rejected**.

---

## Components

1. **Handler (Abstract):** Declares the method for handling requests and maintains a reference to the next handler.  
   Example: `PaymentHandler`  

2. **Concrete Handlers:** Implement request handling logic and forward unhandled requests.  
   Examples: `BankPaymentHandler`, `CreditCardPaymentHandler`, `PayPalPaymentHandler`  

3. **Client:** Creates the chain and sends requests into it.  
   Example: `Main`  

---

## UML Diagram

```mermaid
classDiagram
    direction LR

    PaymentHandler <|-- BankPaymentHandler
    PaymentHandler <|-- CreditCardPaymentHandler
    PaymentHandler <|-- PayPalPaymentHandler
    Main --> PaymentHandler : uses

    class PaymentHandler {
        -next: PaymentHandler
        +setNext(next: PaymentHandler)
        +handlePayment(amount: double)
    }

    class BankPaymentHandler {
        +handlePayment(amount: double)
    }

    class CreditCardPaymentHandler {
        +handlePayment(amount: double)
    }

    class PayPalPaymentHandler {
        +handlePayment(amount: double)
    }

    class Main {
        +main()
    }
