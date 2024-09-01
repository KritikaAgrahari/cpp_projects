
#include<iostream>
#include<fstream>
#include<sstream>
#include<string>

using namespace std;

int main() {
    int a;
    string text, oldPassword, newPassword1, newPassword2, storedPassword, storedUsername, enteredUsername, enteredPassword, name, age;

    cout << "     SECURITY SYSTEM    " << endl;

    cout << "----------1. Register------------" << endl;
    cout << "----------2. Login---------------" << endl;
    cout << "----------3. Change Password------------" << endl;
    cout << "----------4. End Program--------------" << endl << endl;

    do {
        cout << "\nEnter your choice: ";
        cin >> a;

        switch (a) {
            case 1: {  // Registration
                cout << "---------Register---------" << endl;
                cout << "Enter username: ";
                cin >> name;
                cout << "Enter password: ";
                cin >> storedPassword;
                cout << "Enter age: ";
                cin >> age;

                // Save to file
                ofstream outFile("users.txt", ios::app);
                if (outFile.is_open()) {
                    outFile << name << "\n" << storedPassword << "\n" << age << "\n";
                    outFile.close();
                    cout << "Registration successful." << endl;
                } else {
                    cout << "Error: Unable to open file for registration." << endl;
                }
                break;
            }

            case 2: {  // Login
                cout << "-------------Login-----------" << endl;
                cout << "Enter username: ";
                cin >> enteredUsername;
                cout << "Enter password: ";
                cin >> enteredPassword;

                // Read file for login
                ifstream inFile("users.txt");
                bool loginSuccess = false;
                if (inFile.is_open()) {
                    while (getline(inFile, storedUsername) && getline(inFile, storedPassword) && getline(inFile, age)) {
                        if (enteredUsername == storedUsername && enteredPassword == storedPassword) {
                            loginSuccess = true;
                            cout << "Login successful!" << endl;
                            cout << "Username: " << storedUsername << "\nAge: " << age << endl;
                            break;
                        }
                    }
                    inFile.close();
                } else {
                    cout << "Error: Unable to open file for login." << endl;
                }

                if (!loginSuccess) {
                    cout << "Login failed: Incorrect username or password." << endl;
                }
                break;
            }

            case 3: {  // Change password
                cout << "--------------Change Password------------" << endl;
                cout << "Enter your username: ";
                cin >> enteredUsername;
                cout << "Enter your old password: ";
                cin >> oldPassword;

                // Store all users temporarily
                ifstream inFile("users.txt");
                ofstream tempFile("temp.txt");
                bool passwordChanged = false;

                if (inFile.is_open() && tempFile.is_open()) {
                    while (getline(inFile, storedUsername) && getline(inFile, storedPassword) && getline(inFile, age)) {
                        if (enteredUsername == storedUsername && oldPassword == storedPassword) {
                            cout << "Enter new password: ";
                            cin >> newPassword1;
                            cout << "Confirm new password: ";
                            cin >> newPassword2;

                            if (newPassword1 == newPassword2) {
                                tempFile << storedUsername << "\n" << newPassword1 << "\n" << age << "\n";
                                cout << "Password changed successfully." << endl;
                                passwordChanged = true;
                            } else {
                                cout << "Error: Passwords do not match." << endl;
                                tempFile << storedUsername << "\n" << storedPassword << "\n" << age << "\n";
                            }
                        } else {
                            tempFile << storedUsername << "\n" << storedPassword << "\n" << age << "\n";
                        }
                    }
                    inFile.close();
                    tempFile.close();

                    // Replace old file with new file
                    remove("users.txt");
                    rename("temp.txt", "users.txt");

                    if (!passwordChanged) {
                        cout << "Error: Username or old password is incorrect." << endl;
                    }
                } else {
                    cout << "Error: Unable to open files for password change." << endl;
                }
                break;
            }

            case 4: {
                cout << "Thank you for using the security system!" << endl;
                break;
            }

            default:
                cout << "Invalid choice, please enter a valid option." << endl;
        }

    } while (a != 4);

    return 0;
}
