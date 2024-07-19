# community-  
#include <iostream>
#include <string>

using namespace std;

class Person {
protected:
    string name;
    int age;
    string gender;
    string address;

public:
    Person() : name(""), age(0), gender(""), address("") {}

    void setName(const string &n) { name = n; }
    void setAge(int a) { age = a; }
    void setGender(const string &g) { gender = g; }
    void setAddress(const string &addr) { address = addr; }

    string getName() const { return name; }
    int getAge() const { return age; }
    string getGender() const { return gender; }
    string getAddress() const { return address; }

    virtual void saveInfo() = 0;
    virtual void displayInfo() const = 0;

    virtual ~Person() {}
};

class Teacher : public Person {
private:
    string phoneNumber;
    string qualification;
    double salary;

public:
    Teacher() : phoneNumber(""), qualification(""), salary(0.0) {}

    void setPhoneNumber(const string &pn) { phoneNumber = pn; }
    void setQualification(const string &q) { qualification = q; }
    void setSalary(double s) { salary = s; }

    string getPhoneNumber() const { return phoneNumber; }
    string getQualification() const { return qualification; }
    double getSalary() const { return salary; }

    void saveInfo() override {
        cout << "Enter Name: ";
        getline(cin, name);
        cout << "Enter Gender: ";
        getline(cin, gender);
        cout << "Enter Age: ";
        cin >> age;
        cin.ignore();
        cout << "Enter Address: ";
        getline(cin, address);
        cout << "Enter Phone Number: ";
        getline(cin, phoneNumber);
        cout << "Enter Qualification: ";
        getline(cin, qualification);
        cout << "Enter Salary: ";
        cin >> salary;
        cin.ignore();
    }

    void displayInfo() const override {
        cout << "Teacher's Name: " << name << endl;
        cout << "Gender: " << gender << endl;
        cout << "Age: " << age << endl;
        cout << "Address: " << address << endl;
        cout << "Phone Number: " << phoneNumber << endl;
        cout << "Qualification: " << qualification << endl;
        cout << "Salary: " << salary << endl;
    }
};

class Student : public Person {
private:
    string major;
    double gpa;

public:
    Student() : major(""), gpa(0.0) {}

    void setMajor(const string &m) { major = m; }
    void setGpa(double g) { gpa = g; }

    string getMajor() const { return major; }
    double getGpa() const { return gpa; }

    void saveInfo() override {
        cout << "Enter Name: ";
        getline(cin, name);
        cout << "Enter Gender: ";
        getline(cin, gender);
        cout << "Enter Age: ";
        cin >> age;
        cin.ignore();
        cout << "Enter Address: ";
        getline(cin, address);
        cout << "Enter Major: ";
        getline(cin, major);
        cout << "Enter GPA: ";
        cin >> gpa;
        cin.ignore();
    }

    void displayInfo() const override {
        cout << "Student's Name: " << name << endl;
        cout << "Gender: " << gender << endl;
        cout << "Age: " << age << endl;
        cout << "Address: " << address << endl;
        cout << "Major: " << major << endl;
        cout << "GPA: " << gpa << endl;
    }
};

int main() {
    Person *people[10];
    int choice;
    int count = 0;
    char moreData;

    do {
        cout << "Enter Choice: T for Teacher, S for Student: ";
        char type;
        cin >> type;
        cin.ignore();

        if (type == 'T' || type == 't') {
            people[count] = new Teacher();
        } else if (type == 'S' || type == 's') {
            people[count] = new Student();
        } else {
            cout << "Invalid choice!" << endl;
            continue;
        }

        people[count]->saveInfo();
        count++;

        cout << "Do you want to enter more data (Y for Yes, N for No): ";
        cin >> moreData;
        cin.ignore();
    } while (moreData == 'Y' || moreData == 'y');

    for (int i = 0; i < count; i++) {
        cout << "\nDisplaying Information:\n";
        people[i]->displayInfo();
        delete people[i];
    }

    return 0;
}
