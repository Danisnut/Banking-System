# Banking-System

class User:
    def __init__(self, first_name, last_name, gender, street_address, city, email, cc_number, cc_type, balance, account_no):
        self.first_name = first_name
        self.last_name = last_name
        self.gender = gender
        self.street_address = street_address
        self.city = city
        self.email = email
        self.cc_number = cc_number
        self.cc_type = cc_type
        self.balance = balance
        self.account_no = account_no
        userList.append(self)

    def display_info(self):
        print("#############################")
        print(f"Name: {self.first_name}, {self.last_name}")
        print("#############################")
        print(f"Gender: {self.gender}")
        print(f"Address: {self.street_address}")
        print(f"City: {self.city}")
        print(f"Email: {self.email}")
        print(f"CC Type: {self.cc_type}")
        print(f"Balance: {self.balance}")
        print(f"Account Number: {self.account_no}")
        print()


def generateUsers():
    import csv
    with open('bankUsers.csv', newline='') as csvfile:
        filereader = csv.reader(csvfile, delimiter=',', quotechar="'")
        for line in filereader:
            User(line[0], line[1], line[2], line[3], line[4], line[5], line[6], line[7], float(line[8]), line[9])

def findUser(text):
    name = input(text).title()
    for user in userList:
        full_name = f"{user.first_name} {user.last_name}"
        if full_name == name:
            user.display_info()
            return user
    if name not in userList:
        print(f"\nWe have no user by the name '{name}' on our "
              f"records\n")
        return None

    True

def overdrafts():
    overdraft_count = 0
    for user in userList:
        if user.balance < 0:
            overdraft_count += 1  
            print("#############################")
            print(f"{user.first_name} {user.last_name} has an overdraft of ${user.balance}")
    print(f"")
    print(f"There is a total of {overdraft_count} users with overdrafts")

    True

def missingEmails():
    count = 0
    for user in userList:
        if not user.email:
            print(f"{user.first_name} {user.last_name} does not have an email")
            count += 1
    print(f"There are {count} users missing an email")

    True

def bankDetails():
    total_number = len(userList)
    total_balance = sum(user.balance for user in userList)

    highest_bal = max(userList, key=lambda user: user.balance)
    lowest_bal = min(userList, key=lambda user: user.balance)

    print(f"Total number of users: {total_number}")
    print(f"Total balance of users: {total_balance}")
    print(f"User with highest balance: {highest_bal.first_name} {highest_bal.last_name}. Balance: {highest_bal.balance}")
    print(f"User with lowest balance: {lowest_bal.first_name} {lowest_bal.last_name}. Balance: {lowest_bal.balance}")

    True

def transfer():
    # I don't know, I give up. Thank you!

    True


userList = []
generateUsers()

userChoice = ""
print("Welcome")

while userChoice != "Q":
    print("What function would you like to run?")
    print("Type 1 to find a user")
    print("Type 2 to print overdraft information")
    print("Type 3 to print users with missing emails")
    print("Type 4 to print bank details")
    print("Type 5 to transfer money")
    print("Type Q to quit")
    userChoice = input("Enter choice: ")
    print()

    if userChoice == "1":
        findUser("Which user are you trying to find? (First and Last Name): ")
    elif userChoice == "2":
        overdrafts()
    elif userChoice == "3":
        missingEmails()
    elif userChoice == "4":
        bankDetails()
    elif userChoice == "5":
        transfer()
    print()
