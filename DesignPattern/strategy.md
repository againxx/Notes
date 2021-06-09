# Strategy

> Design a family of algorithms, encapsulate each one, and make them interchangeable.
> Strategy lets the algorithm vary independently from the clients that use it.

![UML for strategy pattern](https://gitee.com/againxx/image-storage/raw/master/images/20210609174358.png =750x)

## Components
* Context
    - Provides a service by delegating some computation to interchangeable components that implement alternative algorithms.
    - In the ecommerce example, the context is an **Order**, which is configured to apply a promotional discount according to one
      of several algorithms
* Strategy
    - The interface common to the components that implement the different algorithms.
    - In our example, this role is played by an abstract class called **Promotion**
* Concrete Strategy
    - One of the concrete subclasses of Strategy.

## Classic Implementation
```python
from abc import ABC, abstractmethod
from collections import namedtuple
from dataclasses import dataclass

Customer = namedtuple('Customer', 'name fidelity')

@dataclass
class LineItem:
    product: str
    quantity: int
    price: float

    def total(self):
        return self.quantity * self.price

class Order:
    def __init__(self, customer, cart, promotion=None):
        self.customer = customer
        self.cart = list(cart)
        self.promotion = promotion

    def total(self):
        if not hasattr(self, '__total'):
            self.__total = sum(item.total() for item in self.cart)
        return self.__total

    def due(self):
        if self.promotion is None:
            discount = 0
        else:
            discount = self.promotion.discount(self)
        return self.total() - discount

    def __repr__(self):
        fmt = '<Order total: {:.2f} due: {:.2f}>'
        return fmt.format(self.total(), self.due())

class Promotion(ABC):

    @abstractmethod
    def discount(self, order):
        """Return discount as a positive dollar amount"""

class FidelityPromo(Promotion):
    """5% discount for customers with 1000 or more fidelity points"""

    def discount(self, order):
        return order.total() * .05 if order.customer.fidelity >= 1000 else 0

class BulkItemPromo(Promotion):
    """10% discount for each LineItem with 20 or more units"""

    def discount(self, order):
        discount = 0
        for item in order.cart:
            if item.quantity >= 20:
                discount += item.total() * .1
        return discount

class LargeOrderPromo(Promotion):
    """7% discount for orders with 10 or more distinct items"""

    def discount(self, order):
        distinct_items = {item.product for item in order.cart}
        if len(distinct_items) >= 10:
            return order.total() * .07
        return 0
```

## Function-Oriented Implementation
```python
# promotions.py
def fidelity_promo(order):
    """5% discount for customers with 1000 or more fidelity points"""
    return order.total() * .05 if order.customer.fidelity >= 1000 else 0

def bulk_item_promo(order):
    """10% discount for each LineItem with 20 or more units"""
    discount = 0
    for item in order.cart:
        if item.quantity >= 20:
            discount += item.total() * .1
    return discount

def large_order_promo(order):
    """7% discount for orders with 10 or more distinct items"""
    distinct_items = {item.product for item in order.cart}
    if len(distinct_items) >= 10:
        return order.total() * .07
    return 0

# main.py
# we can use inspect module to collect all strategy functions
promos = [func for name, func in inspect.getmembers(promotions, inspect.isfunction)]

# and automatically pick the best one
def best_promo(order):
    """Select best discount available"""
    return max(promo(order) for promo in promos)

```

## Why Prefer Functions
* Each concrete strategy only has a single method and has no state
* A function is more lightweight than an instance of a user-defined class
* A plain function is an inborn flyweight
    - flyweight: a shared object that can be used in multiple contexts simultaneously
    - Without flyweight, the strategy instances need to be constructed over and over again
