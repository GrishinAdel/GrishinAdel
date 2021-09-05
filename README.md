
#include <iostream>
#include <string>
#include <Windows.h>
#include <list>     
using namespace std;

void intro() // Заставка
{
    cout << "                                 КУРСОВАЯ РАБОТА" << endl;
    cout << "                 по дисциплине «Алгоритмизация и программирование»" << endl;
    cout << "     на тему <<Динамическая структура данных. Двунапрвленный линейный список>>" << endl;
    cout << "                             Гришин Адель Ревалевич" << endl;
    cout << "                                Добро пожаловать!" << endl;
    cout << endl;
};

int menu() //Меню выбора команд
{
    setlocale(LC_ALL, "Russian");
    int program;
    cout << "---------------------------------------Меню---------------------------------------\n"
        << "  |1 Создание пустого списка (старый список удаляется).                          |\n"
        << "  |2 Подсчёт количества элементов списка.                                        |\n"
        << "  |3 Вывод на экран сожеримого списка.                                           |\n"
        << "  |4 Вставка элемента в начало или в конец списка.                               |\n"
        << "  |5 Исключение элемента из начала или конца списка.                             |\n"
        << "  |6 Уничтожение списка с освобождением памяти.                                  |\n"
        << "  |7 Исключить элемент перед элементом с заданным ключом.                        |\n"
        << "  |8 Выход                                                                       |\n"
        << "----------------------------------------------------------------------------------\n";
    cin >> program;
    return program;
};

void end()
{
    cout << "" << endl;
    cout << "Программа завершила работу!" << endl;
    cout << "С Уважением, разработчик программы, Гришин Адель!" << endl;
};

struct Friends {
    int data;
    string name;
    string familia;
    Friends* next;
    Friends* prev;
};
Friends* head;
Friends* tail;

void zero() // Создание пустого списка
{
    head = NULL;
    tail = head;
    cout << "Пустой список готов!" << endl;
};

void FIO(int i, string name, string familia)
{
    Friends* nFriends = new Friends;
    head = nFriends;
    tail = nFriends;
    nFriends->data = i;
    nFriends->name = name;
    nFriends->familia = familia;
    nFriends->next = NULL;
    nFriends->prev = NULL;
};

void dobavlenie_v_nachalo() //Функция добавления элемента в начало списка
{
    string name, familia;
    int i = 0;
    cout << "Введите возраст: ";
    cin >> i;
    cout << "Введите имя: ";
    cin >> name;
    cout << "Введите фамилию: ";
    cin >> familia;
    if (head == NULL)
    {
        FIO(i, name, familia);
    }
    else
    {
        Friends* nFriends = new Friends;
        nFriends->prev = NULL;
        nFriends->data = i;
        nFriends->name = name;
        nFriends->familia = familia;
        nFriends->next = head;
        head->prev = nFriends;
        head = nFriends;
        tail->next = NULL;
        head->prev = NULL;
    }
    cout << "Участник успешно добавлен" << endl;
    cout << " " << endl;
};
void dobavlenie_v_konets() //Функция добавления элемента в конец списка
{
    string name;
    string familia;
    int i = 0;
    int on = 0;
    cout << "Возраст : ";
    cin >> i;
    cout << "Введите имя: ";
    cin >> name;
    cout << "Введите фамилию: ";
    cin >> familia;
    cout << "---------------------------------------------------" << endl;
    if (head == NULL)
    {
        FIO(i, name, familia);
    }
    else
    {
        Friends* nFriends = new Friends;
        nFriends->next = NULL;
        nFriends->data = i;
        nFriends->name = name;
        nFriends->familia = familia;
        tail->next = nFriends;
        tail = nFriends;
        tail->next = NULL;
    }
    cout << "Участник успешно добавлен" << endl;
    cout << " " << endl;
};
Friends* udalenie_nachalo() //Функция удаления первого элемента списка
{
    if (head != NULL)
    {
        int on;
        cout << "Вы уверены, что хотите удалить участника?" << endl;
        cout << "1. Да  2. Нет" << endl;
        cout << "Выберите действие: ";
        cin >> on;
        if (on == 1)
        {
            if (head->next == head) head = NULL;
            else if (head->next == tail)
            {
                delete head;
                head = tail;
                head->next = head;
            }
            else
            {
                Friends* nFriends = head;
                Friends* nnFriends = nFriends->next;
                head = nnFriends;
                nnFriends->prev = NULL;
                delete nFriends;
            }
            cout << "Участник успешно удален";
            cout << endl;
        }
    }
    else
    {
        cout << "Список пуст" << endl;
    }
    return head;
};

void udalenie_konets() //Функция удаления последнего элемента списка
{
    if (head != NULL)
    {
        int on;
        cout << "Вы уверены, что хотите удалить участника?" << endl;
        cout << "1. Да                    2. Нет" << endl;
        cout << "Выберите действие: ";
        cin >> on;
        if (on == 1)
        {
            if (head == tail)
                head = NULL;
            else if (head->next == tail)
            {
                delete tail;
                tail = head;
                tail->next = NULL;
            }
            else
            {
                Friends* nFriends = head;
                while (nFriends->next != tail)
                    nFriends = nFriends->next;
                swap(tail, nFriends);
                delete nFriends;
                tail->next = NULL;
            }
            cout << "Участник успешно удален";
            cout << endl;
        }
    }
    else
        cout << "Список пуст" << endl;
};

void display() //Функция вывода списка на экран
{
    int count = 0;
    if (head != NULL)
    {
        cout << " №" << "\t|| Возраст:" << "\t|| Фамилия, Имя:" << endl;
        Friends* nFriends = head;
        do
        {
            count++;
            cout << "[" << count << "]" << "\t|| " << nFriends->data << "\t\t|| " << nFriends->familia << " " << nFriends->name << endl;
            nFriends = nFriends->next;
        } while (nFriends != NULL);
        cout << "-----------------------------------------------------------------" << endl;
        cout << "В списке " << count << " элемент/а/ов" << endl;
    }
    else if (head == NULL)
        cout << "Список пуст\n";
};

void count_element() //Функция подсчёта количества элементов
{
    int count = 0;
    if (head != NULL)
    {
        Friends* nFriends = head;
        do
        {
            count++;
            nFriends = nFriends->next;
        } while (nFriends != head);
        cout << "В списке " << count << " элемент/а/ов" << endl;
    }
    else if (head == NULL)
        cout << "Список пуст\n";
};

void udalenie() // Функция уничтожение списка
{
    if (head == NULL)
        head = NULL;
    else if (head == tail)
        delete head;
    else if (head->next == NULL)
    {
        delete tail;
        delete head;
    }
    else if (head->next != tail)
    {
        while (head->next != tail)
        {
            Friends* nFriends = head;
            nFriends = nFriends->next;
            head->next = nFriends->next;
            delete nFriends;

        }
        delete tail;
        delete head;
    }
    cout << "Список удален" << endl;
    head = NULL;
    tail = head;
};


Friends* udalenie_key() //Функция исключения элемента перед элементом заданным с ключом
{
    cout << " " << endl;
    if (head == NULL)
        cout << "Список пуст\n";
    else
    {
        cout << "Ключи: " << endl;
        Friends* nFriends = head;
        int count = 0;
        do
        {
            count++;
            cout << count << ") " << nFriends->data << endl;
            nFriends = nFriends->next;
        } while (nFriends != NULL);
        if (count < 2) cout << endl << "Недостаточно элементов" << endl << endl;
        else
        {
            cout << " " << endl;
            cout << "Укажите номер ключа элемента, перед которым требуется ислкючить элемент (кроме 1): ";
            cout << " " << endl;
            int udal = 0;
            cin >> udal;
            while ((udal == 1) || (udal > count))
            {
                cout << "Введите правильное значение индекса: ";
                cin >> udal;
            }
            udal = udal - 1; // Элемент, который следует исключить
            if (udal == 1)
            {
                udalenie_nachalo();
            }
            else
            {
                Friends* nFriends = head;
                int count = 1;
                while (count != udal+1)
                {
                    if (count == udal)
                    {
                        Friends* Udal = nFriends;
                        Udal->next->prev = nFriends-> prev;
                        Udal->prev->next = nFriends-> next;
                        delete Udal;
                    }
                    nFriends = nFriends->next;
                    count++;
                }
                cout << "Участник успешно удален";
                cout << endl;
            }
        }
    }
    return head;
};

int main() //Основной код
{
    SetConsoleCP(1251);
    SetConsoleOutputCP(1251);
    intro();
    int choose = 0;
    bool Friends = false;
    int proga = menu();
    while (proga != 8)
    {
        switch (proga) {
        case 1:
        {
            zero();
            break;
        }
        case 2:
        {
            count_element();
            break;
        }
        case 3:
        {
            display();
            break;
        }
        case 4:
        {
            cout << "\n1. Добавить нового участника в начало списка";
            cout << "\n2. Добавить нового участника в конец списка";
            cout << "\n3. Вернуться в меню" << endl << endl;;
            cout << "Выберите действие: ";
            cin >> choose;
            if (choose == 1) dobavlenie_v_nachalo();
            else if (choose == 2) dobavlenie_v_konets();
            break;
        }
        case 5:
        {
            cout << "\n1. Удалить первого участника списка";
            cout << "\n2. Удалить последнего участника списка";
            cout << "\n3. Вернуться в меню" << endl << endl;;
            cout << "Выберите действие: ";
            cin >> choose;
            if (choose == 1) udalenie_nachalo();
            else if (choose == 2) udalenie_konets();
            break;
        }
        case 6:
        {
            cout << "Вы уверены, что хотите удалить список?" << endl;
            cout << "1. Да  2. Нет " << endl;
            cin >> choose;
            if (choose == 1)
            {
                udalenie();
                Friends = false;
            }
            break;
        }
        case 7:
        {
            udalenie_key();
            break;
        }
        default: cout << "Выберите пункт из меню\n";
        }
        proga = menu();
    }
    end();
    return 0;
}


