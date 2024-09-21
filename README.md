- #include <iostream>
#include <string>
using namespace std;

class student {
    int roll;
    string name;
    float marks;

public:
    void read(student s[], int n);
    void in_sort(student s[], int n);
    void display(student s[], int n);
    void shell_sort(student s[], int n);
    int getRoll() const { return roll; }
    string getName() const { return name; }
    void setData(int r, const string& n, float m) {
        roll = r;
        name = n;
        marks = m;
    }
};

void student::read(student s[], int n) {
    for (int i = 0; i < n; i++) {
        int r;
        string n;
        float m;
        cout << "Enter roll number, name, and marks: ";
        cin >> r >> n >> m;
        s[i].setData(r, n, m);
    }
}

void student::in_sort(student s[], int n) {
    for (int i = 1; i < n; i++) {
        student val = s[i];
        int j = i - 1;
        while (j >= 0 && s[j].getRoll() > val.getRoll()) {
            s[j + 1] = s[j];
            j--;
        }
        s[j + 1] = val;
    }
}

void student::display(student s[], int n) {
    for (int i = 0; i < n; i++) {
        cout << s[i].getRoll() << " " << s[i].getName() << " " << s[i].marks << endl;
    }
}

void student::shell_sort(student s[], int n) {
    for (int gap = n / 2; gap >= 1; gap /= 2) {
        for (int j = gap; j < n; j++) {
            for (int i = j - gap; i >= 0; i -= gap) {
                if (s[i + gap].getName() > s[i].getName()) {
                    break;
                } else {
                    student temp = s[i + gap];
                    s[i + gap] = s[i];
                    s[i] = temp;
                }
            }
        }
    }
}

int main() {
    int n;
    cout << "Enter the number of records: ";
    cin >> n;

    student s[n], x;
    int choice;

    do {
        cout << "1. ENTER RECORD\n2. DISPLAY RECORD\n3. ARRANGE ORDER USING INSERTION SORT\n4. ARRANGE USING SHELL SORT\n5. EXIT" << endl;
        cout << "Enter the choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                cout << "Enter record:" << endl;
                x.read(s, n);
                break;

            case 2:
                x.display(s, n);
                break;

            case 3:
                cout << "After insertion sort:" << endl;
                x.in_sort(s, n);
                x.display(s, n);
                break;

            case 4:
                cout << "After shell sort:" << endl;
                x.shell_sort(s, n);
                x.display(s, n);
                break;

            case 5:
                cout << "EXIT" << endl;
                break;

            default:
                cout << "Invalid choice. Please try again." << endl;
                break;
        }

        if (choice != 5) {
            cout << "Press 1 to continue or any other key to exit." << endl;
            int cont;
            cin >> cont;
            if (cont != 1) choice = 5;  // Exit loop
        }

    } while (choice != 5);

    return 0;
}

