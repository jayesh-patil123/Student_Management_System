def sign_up():
    username = input("Enter a Username: ")
    password = input("Enter a Password: ")

    with open("users.txt", "a") as user_file:
        user_file.write(f"{username}:{password}\n")
    print("Sign Up SuccessfulLy !")
    user_file.close()

def sign_in():
    username = input("Enter your Username: ")
    password = input("Enter your Password: ")

    with open("users.txt", "r") as user_file:
        users = user_file.readlines()
        for user in users:
            u, p = user.strip().split(':')
            if u == username and p == password:
                print("Sign In successfully !")
                return
    print("Invalid Username or Password. Please Try Again.")
    user_file.close()

def forgot_password():
    username = input("Enter your Username: ")
    new_password = input("Enter a New password: ")

    with open("users.txt", "r") as user_file:
        users = user_file.readlines()
    
    updated_users = []
    found = False

    for user in users:
        u, p = user.strip().split(':')
        if u == username:
            updated_users.append(f"{u}:{new_password}\n")
            found = True
        else:
            updated_users.append(user)

    if found:
        with open("users.txt", "w") as user_file:
            user_file.writelines(updated_users)
        print("Password Updated Successfully !")
    else:
        print("User Not Found. ")
    user_file.close()

def add_student_details():
    student_name = input("Enter student Name: ")
    student_roll = input("Enter student Roll Number: ")
    
    with open("student_details.txt", "a") as student_file:
        student_file.write(f"{student_name},{student_roll}\n")
    print("Student Details Added Successfully !")
    student_file.close()

def update_student_details():
    student_roll = input("Enter the Roll Number of the student to Update: ")
    
    with open("student_details.txt", "r") as student_file:
        students = student_file.readlines()
    
    updated_students = []
    found = False
    
    for student in students:
        name, roll = student.strip().split(',')
        if roll == student_roll:
            new_name = input(f"Enter new name for {name}: ")
            student = f"{new_name},{roll}\n"
            found = True
        updated_students.append(student)
    
    with open("student_details.txt", "w") as student_file:
        student_file.writelines(updated_students)
    
    if found:
        print("Student Details Updated Successfully !")
    else:
        print("Student Not Found.")
    student_file.close()

def delete_student_details():
    student_roll = input("Enter the roll number of the student to Delete: ")
    
    with open("student_details.txt", "r") as student_file:
        students = student_file.readlines()
    
    updated_students = []
    found = False
    
    for student in students:
        name, roll = student.strip().split(',')
        if roll == student_roll:
            found = True
        else:
            updated_students.append(student)
    
    with open("student_details.txt", "w") as student_file:
        student_file.writelines(updated_students)
    
    if found:
        print("Student Details Deleted Successfully !")
    else:
        print("Student Not Found.")
    student_file.close()

def show_student_details():
    with open("student_details.txt", "r") as student_file:
        students = student_file.readlines()
    
    if students:
        print("Student Details:")
        for student in students:
            name, roll = student.strip().split(',')
            print(f"Name: {name}, Roll Number: {roll}")
    else:
        print("No Student Details Available.")
    student_file.close()

def search_student_details():
    student_roll = input("Enter the Roll Number to Search For: ")
    
    with open("student_details.txt", "r") as student_file:
        students = student_file.readlines()
    
    found = False
    
    for student in students:
        name, roll = student.strip().split(',')
        if roll == student_roll:
            print(f"Student Details - Name: {name}, Roll Number: {roll}")
            found = True
    
    if not found:
        print("Student Not Found.")
    student_file.close()

while True:
    print("\nWelcome to the Student Management System")
    print("1. Sign Up")
    print("2. Sign In")
    print("3. Forgot Password")
    print("4. Add Student Details")
    print("5. Update Student Details")
    print("6. Delete Student Details")
    print("7. Show Student Details")
    print("8. Search Student Details")
    print("9. Exit")
    
    choice = input("Enter your choice: ")
  
    if choice == "1": sign_up() # For Sign Up
    elif choice == "2": sign_in() # For Sign In
    elif choice == "3": forgot_password() # When Forgot Password
    elif choice == "4": add_student_details() # Add Student Details
    elif choice == "5": update_student_details() # Update Student Details
    elif choice == "6": delete_student_details() # Delete Student Details
    elif choice == "7": show_student_details() # Show Student Details
    elif choice == "8": search_student_details() # Search Student Details through there Roll No
    elif choice == "9": # Exit
        print("Goodbye!")
        break
    else:
        print("Invalid choice. Please try again.")
