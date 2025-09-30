class Product:
      def __init__(self, name, price, deal_price, ratings):
        self.name = name
        self.price = price
        self.deal_price = deal_price
        self.ratings = ratings
        self.you_saved = price - deal_price

  def display_product_details(self, quantity=1):
        print(f"🛒 Product: {self.name}")
        print(f"   Original Price: ₹{self.price}")
        print(f"   Deal Price: ₹{self.deal_price}")
        print(f"   Ratings: ⭐ {self.ratings}/5")
        print(f"   You Save: ₹{self.you_saved}")
        print(f"   Quantity: {quantity}")
        print(f"   Total Price: ₹{self.get_deal_price() * quantity}")

  def get_deal_price(self):
        return self.deal_price


class ElectronicItem(Product):
    def __init__(self, name, price, deal_price, ratings, warranty_in_months):
        super().__init__(name, price, deal_price, ratings)
        self.warranty_in_months = warranty_in_months

  def display_product_details(self, quantity=1):
        super().display_product_details(quantity)
        print(f"   Warranty: {self.warranty_in_months} months")


class GroceryItem(Product):
    def __init__(self, name, price, deal_price, ratings, expiry_date):
        super().__init__(name, price, deal_price, ratings)
        self.expiry_date = expiry_date

  def display_product_details(self, quantity=1):
        super().display_product_details(quantity)
        print(f"   Expiry Date: {self.expiry_date}")


class Laptop(ElectronicItem):
    def __init__(self, name, price, deal_price, ratings,
                 warranty_in_months, ram, storage):
        super().__init__(name, price, deal_price, ratings, warranty_in_months)
        self.ram = ram
        self.storage = storage

  def display_product_details(self, quantity=1):
        super().display_product_details(quantity)
        print(f"   RAM: {self.ram}")
        print(f"   Storage: {self.storage}")


class Order:
    delivery_charges = {
        "Normal": 0,
        "Prime Delivery": 100
    }

  def __init__(self, delivery_method, delivery_address):
        self.items_in_cart = []
        self.delivery_method = delivery_method
        self.delivery_address = delivery_address

  def add_item(self, product, quantity):
        self.items_in_cart.append((product, quantity))

  def display_order_details(self):
        print("\n========== ORDER SUMMARY ==========")
        print(f"🚚 Delivery Method: {self.delivery_method}")
        print(f"📍 Delivery Address: {self.delivery_address}")
        print("\nItems in your cart:")
        print("-----------------------------------")

  for product, quantity in self.items_in_cart:
            product.display_product_details(quantity)
            print("-----------------------------------")
				total_bill = self.get_total_bill()
        print(f"💰 Total Bill (including delivery): ₹{total_bill}")
        print("===================================\n")

    
def get_total_bill(self):
        total_bill = sum(product.get_deal_price() * quantity
                         for product, quantity in self.items_in_cart)
        total_bill += Order.delivery_charges[self.delivery_method]
        return total_bill

  @classmethod
    def update_delivery_charges(cls, delivery_method, charges):
        cls.delivery_charges[delivery_method] = charges


# ---------- Example Usage ----------
tv = ElectronicItem("Samsung Smart TV", 65000, 60000, 4.5, 24)
milk = GroceryItem("Amul Milk", 40, 30, 4.8, "Jan 2030")
laptop = Laptop("Lenovo IdeaPad 123", 100000, 80000, 4.5, 24, "16 GB", "1 TB SSD")

my_order = Order("Normal", "Hyderabad")
my_order.add_item(tv, 1)
my_order.add_item(milk, 3)
my_order.add_item(laptop, 1)

Order.update_delivery_charges("Normal", 10)

my_order.display_order_details()
