#include <iostream>
#include <vector>
#include <memory>
#include <fstream>
#include <string>
using namespace std;

// Base Class
class MediaItem {
protected:
    int id;
    string title;
    bool checkedOut;

public:
    MediaItem(int i, string t)
        : id(i), title(t), checkedOut(false) {}

    virtual ~MediaItem() {}

    int getId() const {
        return id;
    }

    string getTitle() const {
        return title;
    }

    bool isCheckedOut() const {
        return checkedOut;
    }

    void checkout() {
        checkedOut = true;
    }

    void returnItem() {
        checkedOut = false;
    }

    // Virtual functions demonstrate polymorphism
    virtual void display() const = 0;

    virtual int getLoanDays() const = 0;

    virtual double calculateFine(int overdueDays) const = 0;
};


// Derived Class: Book
class Book : public MediaItem {
private:
    string author;

public:
    Book(int i, string t, string a)
        : MediaItem(i, t), author(a) {}

    void display() const override {
        cout << "\nType: Book";
        cout << "\nID: " << id;
        cout << "\nTitle: " << title;
        cout << "\nAuthor: " << author;
        cout << "\nStatus: "
             << (checkedOut ? "Checked Out" : "Available")
             << endl;
    }

    int getLoanDays() const override {
        return 14;
    }

    double calculateFine(int overdueDays) const override {
        return overdueDays * 2.0;
    }
};


// Derived Class: Journal
class Journal : public MediaItem {
private:
    string issue;

public:
    Journal(int i, string t, string is)
        : MediaItem(i, t), issue(is) {}

    void display() const override {
        cout << "\nType: Journal";
        cout << "\nID: " << id;
        cout << "\nTitle: " << title;
        cout << "\n# library-management-system-