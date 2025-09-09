# Project-1
# The Developers Arena

# Contact Book Application
# Stores user details in a text file
# Features: Add, View, Search, Delete Contacts

import os

CONTACTS_FILE = "contacts.txt"

# Function to add a contact
def add_contact():
    name = input("Enter Name: ")
    phone = input("Enter Phone: ")
    email = input("Enter Email: ")
    contact = f"{name},{phone},{email}\n"

    with open(CONTACTS_FILE, "a") as f:
        f.write(contact)
    print("✅ Contact added successfully!\n")

# Function to view all contacts
def view_contacts():
    if not os.path.exists(CONTACTS_FILE):
        print("No contacts found.\n")
        return []

    with open(CONTACTS_FILE, "r") as f:
        contacts = f.readlines()

    if not contacts:
        print("No contacts available.\n")
        return []

    print("\n📒 Contact List:")
    for idx, line in enumerate(contacts, start=1):
        name, phone, email = line.strip().split(",")
        print(f"{idx}. Name: {name}, Phone: {phone}, Email: {email}")
    print()
    return contacts

# Function to search for a contact
def search_contact():
    search_name = input("Enter name to search: ").lower()

    if not os.path.exists(CONTACTS_FILE):
        print("No contacts found.\n")
        return

    with open(CONTACTS_FILE, "r") as f:
        contacts = f.readlines()

    found = False
    for line in contacts:
        name, phone, email = line.strip().split(",")
        if search_name in name.lower():
            print(f"🔍 Found → Name: {name}, Phone: {phone}, Email: {email}")
            found = True

    if not found:
        print("No matching contact found.\n")

# Function to delete a contact
def delete_contact():
    contacts = view_contacts()
    if not contacts:
        return

    try:
        index = int(input("Enter the number of the contact to delete: "))
        if 1 <= index <= len(contacts):
            removed = contacts.pop(index - 1)
            with open(CONTACTS_FILE, "w") as f:
                f.writelines(contacts)
            name, phone, email = removed.strip().split(",")
            print(f"🗑️ Deleted → Name: {name}, Phone: {phone}, Email: {email}\n")
        else:
            print("❌ Invalid index. Please try again.\n")
    except ValueError:
        print("❌ Invalid input. Please enter a number.\n")

# Main menu
def main():
    while True:
        print("==== Contact Book Menu ====")
        print("1. Add Contact")
        print("2. View Contacts")
        print("3. Search Contact")
        print("4. Delete Contact")
        print("5. Exit")

        choice = input("Enter your choice (1-5): ")

        if choice == "1":
            add_contact()
        elif choice == "2":
            view_contacts()
        elif choice == "3":
            search_contact()
        elif choice == "4":
            delete_contact()
        elif choice == "5":
            print("👋 Exiting Contact Book. Goodbye!")
            break
        else:
            print("❌ Invalid choice. Please try again.\n")

if __name__ == "__main__":
    main()







