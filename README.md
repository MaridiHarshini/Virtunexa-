inventory = []

def main_menu():
    while True:
        print("\n=== Welcome to the Python Adventure App ===")
        print("1. Play Adventure Game")
        print("2. Use Calculator")
        print("3. Exit")
        choice = input("Choose an option (1/2/3): ").strip()

        if choice == "1":
            play_game()
        elif choice == "2":
            calculator()
        elif choice == "3":
            print("Goodbye!")
            break
        else:
            print("Invalid choice. Please enter 1, 2, or 3.")


def play_game():
    global inventory
    inventory = []
    print("\nYou wake up in a mysterious forest.")
    print("There is a path to your LEFT and RIGHT.")
    while True:
        choice = input("Which way do you go? (left/right): ").strip().lower()
        if choice in ['left', 'l']:
            left_path()
            break
        elif choice in ['right', 'r']:
            right_path()
            break
        else:
            print("Invalid choice. Please type 'left' or 'right'.")

def left_path():
    global inventory
    print("\nYou find a shiny sword on the ground and pick it up.")
    inventory.append("sword")
    print("Inventory:", inventory)
    encounter_troll()

def right_path():
    print("\nYou stumble upon a peaceful lake and rest there.")
    encounter_troll()

def encounter_troll():
    print("\nA wild troll appears!")
    if "sword" in inventory:
        print("You use your sword to fight the troll and win!")
    else:
        print("You have no weapon. The troll defeats you.")
    play_again()

def play_again():
    while True:
        again = input("Play again? (yes/no): ").strip().lower()
        if again == 'yes':
            play_game()
            break
        elif again == 'no':
            print("Returning to main menu.")
            break
        else:
            print("Please enter 'yes' or 'no'.")


def calculator():
    print("\n=== Calculator ===")
    try:
        num1 = float(input("Enter first number: "))
        op = input("Enter operation (+, -, *, /): ").strip()
        num2 = float(input("Enter second number: "))

        if op == '+':
            res = num1 + num2
        elif op == '-':
            res = num1 - num2
        elif op == '*':
            res = num1 * num2
        elif op == '/':
            if num2 == 0:
                print("Error: Cannot divide by zero.")
                return
            res = num1 / num2
        else:
            print("Invalid operation.")
            return

        print("Result:", res)
        
        with open("calc_history.txt", "a") as f:
            f.write(f"{num1} {op} {num2} = {res}\n")

    except ValueError:
        print("Invalid input. Please enter numeric values.")

if __name__ == "__main__":
    main_menu()
