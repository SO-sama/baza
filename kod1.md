#include <iostream>
#include <fstream>
#include <string>
using namespace std;


struct struct1 {
    int a;
    double b;
    char c;
};

int main() {
    setlocale(LC_ALL, "rus");
    string filename;


    // 3 
    cout << "FileNAME: ";
    cin >> filename;

    ofstream oStruct(filename, ios::binary);
    if (oStruct.is_open()) {
        struct1 st1 = { 1, 0.2, 'X' };
        struct1 st2 = { 2, 4.21, 'Y' };
        struct1 st3 = { 3, 2.12, 'Z' };

        oStruct.write(reinterpret_cast<char*>(&st1), sizeof(st1));
        oStruct.write(reinterpret_cast<char*>(&st2), sizeof(st2));
        oStruct.write(reinterpret_cast<char*>(&st3), sizeof(st3));

        oStruct.close();
        cout << "ЗАПИСАНО" << endl;
    }
    else {
        cout << "Не удалось открыть файл" << endl;
    }

    // 4 
    cout <<"4" << endl << "FileNAME ";
    cin >> filename;

    ifstream iStruct(filename, ios::binary);
    if (iStruct.is_open()) {
        struct1 st1, st2, st3;

        iStruct.read(reinterpret_cast<char*>(&st1), sizeof(st1));
        iStruct.read(reinterpret_cast<char*>(&st2), sizeof(st2));
        iStruct.read(reinterpret_cast<char*>(&st3), sizeof(st3));

        iStruct.close();
        
        cout << "a = " << st1.a << " b = " << st1.b << " c = " << st1.c << endl;
        cout << "a = " << st2.a << " b = " << st2.b << " c = " << st2.c << endl;
        cout << "a = " << st3.a << " b = " << st3.b << " c = " << st3.c << endl;
    }
    else {
        cout << "Не удалось открыть файл" << endl;
    }

    return 0;
}
