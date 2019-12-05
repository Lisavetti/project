# project
*****header.h*******
	#pragma once
	#include <iostream>
	#include <conio.h>
	#include <fstream>

	typedef double TE;

	struct L1 {
		TE value1;
		L1* next;
	};
	struct L2 {
		TE value2;
		L2* next;
	};
	struct L {
		TE value3;
		L* next;
	};
	int answer1, count1, answer2;
	TE l;
	L1 *element1;
	L1 *first1 = 0;
	L *element3 = 0;
	L *first3 = 0;
	L2 *first2 = 0;
	L2 *element2;
 ****functions.cpp**** 
#include "pch.h"
#include "Header.h"
using namespace std;
ofstream output1("1.txt");
ofstream output2("2.txt");
ofstream output3("3.txt");
ofstream output4("4.txt");
void menu(); // прототип
void input() {
	cout << "Enter the number of items for the L1 list: ";
	cin >> answer1;
	for (int i = 0; i < answer1; i++)
	{
		cout << "Input " << answer1 - i << " element:";
		element1 = new L1; //создание структуры
		cin >> element1->value1; //обращение к полю структуры VALUE1
		element1->next = first1; // следующий элемент становится первым
		first1 = element1; // ЗАНОСИМ ЭЛЕМЕНТЫ
	}
	cout << "Enter the number of items for the L2 list: ";
	cin >> answer2;
	for (int t = 0; t < answer2; t++)
	{
		cout << "Input " << answer2 - t << " element:";
		element2 = new L2;
		cin >> element2->value2;
		element2->next = first2;
		first2 = element2;
	}
	element2 = first2;
	element1 = first1;
	cout << "L1:";
	while (element1)
	{
		cout << element1->value1 << ' ';
		element1 = element1->next;
	}
	cout << endl;
	cout << "L2:";
	while (element2)
	{
		cout << element2->value2 << ' ';
		element2 = element2->next;
	}
	cout << endl;
}
void task1()
{
	output1 << "Is the item in the list?" << endl;
	element2 = first2;
	element1 = first1;
	for (int i = 0; i < answer1; i++)
	{
		element3 = new L;
		element3->value3 = element1->value1;
		element1 = element1->next;
		element3->next = first3;
		first3 = element3;
	}
	for (int i = 0; i < answer2; i++)
	{
		element3 = new L;
		element3->value3 = element2->value2;
		element2 = element2->next;
		element3->next = first3;
		first3 = element3;
	}
	element3 = first3;
	output1 << "L: ";
	while (element3)
	{
		output1 << element3->value3 << ' ';
		element3 = element3->next;
	}
	while (first3)
	{
		element3 = first3;
		first3 = first3->next; 
		delete element3;
	}
	output1 << endl;
	menu();
}
void task2() {
	output2 << "Is the item in the list at the same time?" << endl;
	element1 = first1;
	element2 = first2;
	output2 << "L: ";
	for (int i = 0; i < answer1; i++)
	{
		l = element1->value1;
		for (int r = 0; r < answer2; r++)
		{
			if (l == element2->value2)
			{
				element3 = new L;
				element3->value3 = l;
				element3->next = first3;
				first3 = element3;
			}
			element2 = element2->next;
		}
		element2 = first2;
		element1 = element1->next;
	}
	element3 = first3;
	while (element3)
	{
		output2 << element3->value3 << ' ';
		element3 = element3->next;
	}
	while (first3)
	{
		element3 = first3;
		first3 = first3->next;
		delete element3;
	}
	output2 << endl;
	menu();
}
void task3() {
	output3 << "Items that are included in the list L1 but not in L2" << endl;
	element1 = first1;
	element2 = first2;
	output3 << "L: ";
	for (int i = 0; i < answer1; i++)
	{
		l = element1->value1;
		element3 = new L; // 3 список заполняется Элементами первого
		element3->value3 = l;
		for (int i = 0; i < answer2; i++)
		{
			if (l == element2->value2)
			{
				free(element3);
			}
			element2 = element2->next;
		}
		if (l == element3->value3)
		{
			element3->next = first3;
			first3 = element3;
		}
		element2 = first2;
		element1 = element1->next;
	}
	element3 = first3;
	while (element3)
	{
		output3 << element3->value3 << ' ';
		element3 = element3->next;
	}
	while (first3)
	{
		element3 = first3;
		first3 = first3->next;
		delete element3;
	}
	output3 << endl;
	menu();
}
void task4()
{
	output4 << "Are included in one of the L1 and L2 lists, but at the same time they are not part of the otherthem." << endl;
	element1 = first1;
	element2 = first2;
	cout << "L: ";
	for (int i = 0; i < answer1; i++)
	{
		l = element1->value1;
		element3 = new L;
		element3->value3 = l;
		for (int i = 0; i < answer2; i++)
		{
			if (l == element2->value2)
			{
				free(element3);
			}
			element2 = element2->next;
		}
		if (l == element3->value3)
		{
			element3->next = first3;
			first3 = element3;
		}
		element2 = first2;
		element1 = element1->next;
	}
	element1 = first1;
	element2 = first2;
	for (int i = 0; i < answer2; i++)
	{
		l = element2->value2;
		element3 = new L;
		element3->value3 = l;
		for (int r = 0; r < answer1; r++)
		{
			if (l == element1->value1)
			{
				free(element3);
			}
			element1 = element1->next;
		}
		if (l == element3->value3)
		{
			element3->next = first3;
			first3 = element3;
		}
		element1 = first1;
		element2 = element2->next;
	}

	element3 = first3;
	output4 << "L: ";
	while (element3)
	{
		output4 << element3->value3 << ' ';
		element3 = element3->next;
	}
	while (first3)
	{
		element3 = first3;
		first3 = first3->next;
		delete element3;
	}
	output4 << endl;
	menu();
}
void menu() {
	cout << "1. First task" << endl << "2. Second task" << endl << "3. Third task" << endl << "4. Fourth task" << endl << "5. Exit" << endl;
	cout << "Enter the menu item number : ";
	cin >> count1;
	switch (count1) {
	case 1:
	{
		task1();
	
	}
	case 2:
	{
		task2();
		break;
	}
	case 3:
	{
		task3();
		break;
	}
	case 4:
	{
		task4();
		break;
	}
	case 5:
	{
		exit(0);
	}
	default:
		cout << "Invalid value" << endl;
	}
}
***Console Application1***
#include "pch.h"
#include "Header.h"
#include "functions.cpp"
#include <iostream>
#include <conio.h>
#include <fstream>
using namespace std;

int main()
{
	setlocale(LC_ALL, "RUS");
	input();
	menu();
	return 0;
}
