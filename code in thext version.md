
in case you cannot open the .cs file here is a full code ( someome mentioned receiving a 404)


using System;
using System.Collections.Generic;

class Inventory
{
    static List<Product> products = new List<Product>();

    static void Main(string[] args)
    {
        while (true)
        {
            Console.WriteLine("Welcome to the Inventory Management System!");
            Console.WriteLine("Choose an option:");
            Console.WriteLine();
            Console.WriteLine("View Inventory (1)");
            Console.WriteLine("Add New Product (2)");
            Console.WriteLine("Update Product Stock (3)");
            Console.WriteLine("Remove Product From Inventory (4)");
            Console.WriteLine("Exit (5)");
            Console.WriteLine();
            int choice;
            if (int.TryParse(Console.ReadLine(), out choice))
            {
                switch (choice)
                {
                    case 1:
                        ViewInventory();
                        break;
                    case 2:
                        AddNewProduct();
                        break;
                    case 3:
                        UpdateProductStock();
                        break;
                    case 4:
                        RemoveProductFromInventory();
                        break;
                    case 5:
                        Console.WriteLine("Exiting the program.");
                        return;
                    default:
                        Console.WriteLine("Invalid choice. Please select a valid option.");
                        break;
                }
            }
            else
            {
                Console.WriteLine("Invalid input. Please enter a number between 1 and 5.");
            }
        }
    }

    static void ViewInventory()
    {
        Console.WriteLine("Inventory List:");
        if (products.Count == 0)
        {
            Console.WriteLine("No products available in the inventory.");
        }
        else
        {
            for (int i = 0; i < products.Count; i++)
            {
                Console.WriteLine($"{i + 1}. {products[i].Name} - Price: {products[i].Price}. Quantity: {products[i].Quantity}");
            }
            Console.WriteLine();
        }
    }

    class Product
    {
        public string Name { get; set; }
        public decimal Price { get; set; }
        public int Quantity { get; set; }

        public Product(string name, decimal price, int quantity)
        {
            Name = name;
            Price = price;
            Quantity = quantity;
        }
    }

    static void AddNewProduct()
    {
        Console.WriteLine("Enter the product name:");
        string productName = Console.ReadLine();

        Console.WriteLine("Enter the product price:");
        decimal productPrice;
        if (!decimal.TryParse(Console.ReadLine(), out productPrice))
        {
            Console.WriteLine("Invalid price. Please enter a valid decimal number and try again.");
            return;
        }

        Console.WriteLine("Enter the product quantity:");
        int productQuantity;
        if (!int.TryParse(Console.ReadLine(), out productQuantity))
        {
            Console.WriteLine("Invalid quantity. Please enter a valid integer and try again.");
            return;
        }

        products.Add(new Product(productName, productPrice, productQuantity));
        Console.WriteLine("Product added successfully.");
    }

    static void UpdateProductStock()
    {
        if (products.Count == 0)
        {
            Console.WriteLine("No products available to update.");
            return;
        }

        Console.WriteLine("Select the product to update:");
        for (int i = 0; i < products.Count; i++)
        {
            Console.WriteLine($"{i + 1}. {products[i].Name} (Current Quantity: {products[i].Quantity})");
        }

        int index;
        if (!int.TryParse(Console.ReadLine(), out index) || index < 1 || index > products.Count)
        {
            Console.WriteLine("Invalid selection.");
            return;
        }

        Console.WriteLine("Enter the new quantity:");
        int newQuantity;
        if (!int.TryParse(Console.ReadLine(), out newQuantity))
        {
            Console.WriteLine("Invalid quantity. Please enter a valid integer and try again.");
            return;
        }

        products[index - 1].Quantity = newQuantity;
        Console.WriteLine($"Product '{products[index - 1].Name}' quantity updated to {newQuantity}.");
    }

    static void RemoveProductFromInventory()
    {
        if (products.Count == 0)
        {
            Console.WriteLine("No products available to remove.");
            return;
        }

        Console.WriteLine("Select the product to remove:");
        for (int i = 0; i < products.Count; i++)
        {
            Console.WriteLine($"{i + 1}. {products[i].Name}");
        }

        int index;
        if (!int.TryParse(Console.ReadLine(), out index) || index < 1 || index > products.Count)
        {
            Console.WriteLine("Invalid selection.");
            return;
        }

        Console.WriteLine($"Are you sure you want to remove '{products[index - 1].Name}'? (yes/no)");
        string confirmation = Console.ReadLine();
        if (confirmation.ToLower() != "yes")
        {
            Console.WriteLine("Product removal cancelled.");
            return;
        }

        string removedProduct = products[index - 1].Name;
        products.RemoveAt(index - 1);
        Console.WriteLine($"{removedProduct} removed from inventory.");
    }
}
