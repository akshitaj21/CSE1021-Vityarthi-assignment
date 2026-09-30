# CSE1021-Vityarthi-assignment
   OBJECTIVES 

The main objectives of the Grocery and Inventory Management System are:
•	Stock Tracking - Instantly view product availability and monitor in-stock quantities. 
•	Costumer Billing - Add items to a cart, automatically deduct purchased quantities from stock, and generate an itemized receipt with the grand total. 
•	Inventory Control - Easily restock existing products, update pricing, or register brand-new items into the catalog. 










FEATURES OF SYSTEM

Core concepts involved :-
•	Data Structures: Lists and Dictionaries (list[dict]) for tabular data representation. 
•	 Control Flow: while loop for continuous menu navigation and for loops for item traversal. 
•	Conditionals: Nested if, elif, and else statements for validation and input branching. 
•	String Formatting: Formatted string literals (f-strings) for aligned, table-like terminal output.









Code:-
# ========================================================
# Grocery and Inventory Store Management System
# ========================================================

# Priorly designed set of items stored in a list format
inventory = [
    {"id": 1, "name": "Apples", "price": 2.50, "stock": 20},
    {"id": 2, "name": "Milk", "price": 1.50, "stock": 15},
    {"id": 3, "name": "Bread", "price": 1.20, "stock": 10},
    {"id": 4, "name": "Eggs (12pk)", "price": 3.00, "stock": 25},
    {"id": 5, "name": "Rice (1kg)", "price": 2.00, "stock": 30}
]

while True:
    print("\n" + "=" * 40)
    print(" GROCERY & INVENTORY MANAGEMENT SYSTEM")
    print("=" * 40)
    print("1. View Product Availability")
    print("2. Customer Billing")
    print("3. Add or Update Inventory")
    print("4. Exit")
    print("=" * 40)

    choice = input("Enter your choice (1-4): ")

    # 1. VIEW PRODUCT AVAILABILITY
    if choice == "1":
        print("\n--- Current Inventory ---")
        print(f"{'ID':<5}{'Item Name':<16}{'Price ($)':<12}{'Availability':<12}")
        print("-" * 45)
        for item in inventory:
            if item["stock"] > 0:
                availability = f"{item['stock']} in stock"
            else:
                availability = "Out of Stock"
            print(f"{item['id']:<5}{item['name']:<16}{item['price']:<12.2f}{availability:<12}")

    # 2. CUSTOMER BILLING
    elif choice == "2":
        cart = []
        print("\n--- Customer Checkout ---")
        
        while True:
            item_input = input("\nEnter Product ID to buy (or type 'done' to generate bill): ")
            if item_input.lower() == "done":
                break

            # Search for item in inventory
            selected_item = None
            for item in inventory:
                if str(item["id"]) == item_input:
                    selected_item = item
                    break

            if selected_item is None:
                print("Item not found. Please enter a valid ID from the list.")
            elif selected_item["stock"] <= 0:
                print(f"Sorry, {selected_item['name']} is currently out of stock.")
            else:
                qty = int(input(f"Enter quantity for {selected_item['name']}: "))
                if qty <= 0:
                    print("Quantity must be at least 1.")
                elif qty > selected_item["stock"]:
                    print(f"Insufficient stock! Only {selected_item['stock']} available.")
                else:
                    # Deduct from inventory stock
                    selected_item["stock"] -= qty
                    subtotal = qty * selected_item["price"]

                    cart.append({
                        "name": selected_item["name"],
                        "qty": qty,
                        "price": selected_item["price"],
                        "subtotal": subtotal
                    })
                    print(f"Added {qty} x {selected_item['name']} to cart.")

        # Print Customer Receipt / Bill
        if len(cart) > 0:
            print("\n" + "=" * 45)
            print("                 STORE BILL                  ")
            print("=" * 45)
            print(f"{'Item':<16}{'Qty':<8}{'Unit Price':<12}{'Total ($)':<10}")
            print("-" * 45)
            grand_total = 0.0
            for purchase in cart:
                print(f"{purchase['name']:<16}{purchase['qty']:<8}${purchase['price']:<11.2f}${purchase['subtotal']:<9.2f}")
                grand_total += purchase["subtotal"]
            print("-" * 45)
            print(f"Grand Total: ${grand_total:.2f}")
            print("=" * 45)
            print("      Thank you for shopping with us!        ")
            print("=" * 45)
        else:
            print("No items selected. Billing cancelled.")

    # 3. ADD OR UPDATE INVENTORY
    elif choice == "3":
        print("\n--- Add or Update Product ---")
        name = input("Enter product name: ").strip()

        # Check if the product already exists
        existing_item = None
        for item in inventory:
            if item["name"].lower() == name.lower():
                existing_item = item
                break

        # If it exists, update stock/price
        if existing_item is not None:
            print(f"Found '{existing_item['name']}' (Current stock: {existing_item['stock']}, Price: ${existing_item['price']:.2f})")
            add_stock = int(input("Enter additional stock quantity to add: "))
            existing_item["stock"] += add_stock

            change_price = input("Do you want to update price? (y/n): ")
            if change_price.lower() == "y":
                new_price = float(input("Enter new price: "))
                existing_item["price"] = new_price

            print(f"Updated! Stock: {existing_item['stock']}, Price: ${existing_item['price']:.2f}")

        # If it's a new item, add to inventory
        else:
            price = float(input(f"Enter unit price for '{name}': "))
            stock = int(input(f"Enter initial stock quantity: "))
            new_id = len(inventory) + 1
            inventory.append({
                "id": new_id,
                "name": name.title(),
                "price": price,
                "stock": stock
            })
            print(f"New product '{name.title()}' added with ID {new_id}!")

    # 4. EXIT
    elif choice == "4":
        print("Thank you for using the store system. Goodbye!")
        break

    # INVALID OPTION
    else:
        print("Invalid choice! Please choose an option between 1 and 4.")

PROgram Outputs :- 

On running the programs it opens up with a menu window. For Example :- 
========================================
 GROCERY & INVENTORY MANAGEMENT SYSTEM
========================================
1. View Product Availability
2. Customer Billing
3. Add or Update Inventory
4. Exit
========================================
Enter your choice (1-4):

The program comes with pre-defined set of items already present in the inventory.
 


Sample output on viewing the products in the inventory :-

--- Current Inventory ---
ID   Item Name       Price ($)   Availability
---------------------------------------------
1    Apples          2.50        20 in stock 
2    Milk            1.50        15 in stock 
3    Bread           1.20        10 in stock 
4    Eggs (12pk)     3.00        25 in stock 
5    Rice (1kg)      2.00        30 in stock

Sample Bill generated :-
=============================================
STORE BILL 
=============================================
Item Qty Unit Price Total ($) 
---------------------------------------------
Apples 2 $2.50 $5.00 
Milk 1 $1.50 $1.50 
---------------------------------------------
Grand Total: $6.50
=============================================
Thank you for shopping with us! 
=============================================

--- Current Inventory ---
ID   Item Name       Price ($)   Availability
---------------------------------------------
1    Apples          2.50        20 in stock 
2    Milk            1.50        15 in stock 
3    Bread           1.20        10 in stock 
4    Eggs (12pk)     3.00        25 in stock 
5    Rice (1kg)      2.00        30 in stock
