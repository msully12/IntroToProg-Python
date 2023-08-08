# IntroToProg-Python
# Initialize an empty list to store ToDo tasks and priorities
table = []

# Read data from the ToDo text file (if it exists) and populate the list
try:
    with open("ToDo.txt", "r") as file:
        for line in file:
            task, priority = line.strip().split(',')
            table.append({"Task": task, "Priority": priority})
except FileNotFoundError:
    print("ToDo file not found. Starting with an empty list.")

while True:
    print("\nMenu:")
    print("1. Show current data")
    print("2. Add a new item")
    print("3. Remove an existing item")
    print("4. Save Data to File")
    print("5. Exit Program")

    choice = input("Enter your choice (1/2/3/4/5): ")

    if choice == "1":
        print("\nToDo List:")
        print("-----------")
        for index, row in enumerate(table, start=1):
            print(f"{index}. Task: {row['Task']}, Priority: {row['Priority']}")

    elif choice == "2":
        task = input("Enter the task: ")
        priority = input("Enter the priority: ")
        table.append({"Task": task, "Priority": priority})
        print("Task added successfully!")

    elif choice == "3":
        if not table:
            print("The list is empty. Nothing to delete.")
        else:
            try:
                task_index = int(input("Enter the task number to delete: "))
                if 1 <= task_index <= len(table):
                    deleted_task = table.pop(task_index - 1)
                    print(f"Deleted task: {deleted_task['Task']}, Priority: {deleted_task['Priority']}")
                else:
                    print("Invalid task number. Please try again.")
            except ValueError:
                print("Invalid input. Please enter a valid task number.")

    elif choice == "4":
        # Save the data to the text file
        with open("ToDo.txt", "w") as file:
            for row in table:
                file.write(f"{row['Task']},{row['Priority']}\n")

        print("Data saved to 'ToDo.txt'.")

    elif choice == "5":
        print("Exiting the program.")
        break

    else:
        print("Invalid choice. Please choose again.")
