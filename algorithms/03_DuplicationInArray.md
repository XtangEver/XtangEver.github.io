##### 3-1

###### **题目描述：**

在一个长度为n的数组里的所有数字都在0到n-1的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。例如，如果输入长度为7的数组{2, 3, 1, 0, 2, 5, 3}， 那么对应的输出是重复的数字2或者3。

###### **核心代码**

```c++
//加入存在一个数组为number,元素个数为length.

//遍历当前的数组
for(int i = 0;i < length;++ i){
    while(number[i] != i){
        if(number[i]  == number[number[i]]){
            返回当前的值，即为重复
        }
        //交换二者的位置
        int temp = number[i];
        number[i] = number[temp];
        number[temp] = temp;
    }       
}
```

###### **时间复杂度**

O(n)

###### **空间复杂度**

O(1)

###### **完整代码**

```c++
#include <cstdio>
#include <iostream>

using namespace std;

//是否含有重复的数字
bool duplicate(int numbers[], int length, int* duplication) {
	//不符合条件的意外情况
	if (numbers == NULL || length < 0)
		return false;
	for (int i = 0; i < length; ++i) {
		if (numbers[i] < 0 || numbers[i] > length - 1)
			return false;
	}

	for (int i = 0; i < length; ++i) {
		while (numbers[i] != i) {
			if (numbers[i] == numbers[numbers[i]]) {
				*duplication = numbers[i];
				return true;
			}
			int temp = numbers[i];
			numbers[i] = numbers[temp];
			numbers[temp] = temp;
		}
	}

	return false;
}

//是否包含某一个number
bool contains(int array[], int length, int number) {
	for (int i = 0; i < length; ++i) {
		if (array[i] == number)
			return true;
	}
	return false;
}

//用来输出结果的函数
void test(char* testName, int numbers[], int lengthNumber, int expected[], int expectedExpected, bool validArgument) {
	printf("%s begins :", testName);
	int duplication;
	//为什么不可以直接写一个指针呢？
	bool validInput = duplicate(numbers, lengthNumber, &duplication);

	if (validArgument == validInput) {
		if (validArgument) {
			if (contains(expected, expectedExpected, duplication))
				printf("Passed!");
			else
			{
				printf("Failed!");
			}
		}
		else
			printf("Passed!");
	}
	else
		printf("Failed!");
}

//重复的数字是最小的数字
void test1() {
	int array[] = { 2,1,3,1,4 };
	int duplication[] = { 1 };
	test("Test1", array, sizeof(array) / sizeof(int),duplication,sizeof(duplication) / sizeof(int),true);
}

//重复数字是最大的数字
void test2() {
	int array[] = { 2,4,3,1,4 };
	int duplication[] = { 4 };
	test("Test2", array, sizeof(array) / sizeof(int), duplication, sizeof(duplication) / sizeof(int), true);
}

//数组中存在多个重复的数字
void test3() {
	int array[] = { 2,4,2,1,4 };
	int duplication[] = { 2,4 };
	test("Test3", array, sizeof(array) / sizeof(int), duplication, sizeof(duplication) / sizeof(int), true);
}

//数组中没有重复的数字
void test4() {
	int array[] = { 2, 1, 3, 0, 4 };
	int duplication[] = { -1 };
	test("Test4", array, sizeof(array) / sizeof(int), duplication, sizeof(duplication) / sizeof(int), false);
}

void test5() {
	int* array = nullptr;
	int duplication[] = { -1 };
	test("Test5", array,0 , duplication, sizeof(duplication) / sizeof(int), false);
}

int main() {
	test1();
	cout << endl;
	test2();
	cout << endl;
	test3();
	cout << endl;
	test4();
	cout << endl;
	test5();
	cout << endl;
}

```

##### 3-2

###### 题目描述

在一个长度为n+1的数组里的所有数字都在1到n的范围内，所以数组中至 少有一个数字是重复的。请找出数组中任意一个重复的数字，但不能修改输入的数组。例如，如果输入长度为8的数组{2, 3, 5, 4, 3, 2, 6, 7}，那么对应的输出是重复的数字2或者3。

###### **核心代码**

```c++
//计算数组中某一数值范围中元素的个数
int countRange(const int* number, int length, int start, int end) {
	if (number == nullptr)
		return 0;
	int count = 0;
	for (int i = 0; i < length; ++i) {
		if (number[i] >= start && number[i] <= end)
			++count;
	}

	return count;
}
//找到重复的数字
int getDuplication(const int* number, int length) {
	if (number == nullptr || length <= 0)
		return -1;


	int start = 1;
	int end = length - 1;
	while (start <= end) {
		int middle = ((end - start) >> 1) + start;
		int count = countRange(number, length, start, middle);
		if (start == end) {
			if (count > 1)
				return start;
			else
				break;
		}
		if (count > 1)
			end = middle;
		else
			start = middle + 1;
	}
	return -1;
}

```

###### **时间复杂度：**

$O(nlog_2n)$

###### **空间复杂度**

$O(1)$

###### **完整代码**

```c++
#include <iostream>

using namespace std;

//计算数组中某一数值范围中元素的个数
int countRange(const int* number, int length, int start, int end) {
	if (number == nullptr)
		return 0;
	int count = 0;
	for (int i = 0; i < length; ++i) {
		if (number[i] >= start && number[i] <= end)
			++count;
	}

	return count;
}
//找到重复的数字
int getDuplication(const int* number, int length) {
	if (number == nullptr || length <= 0)
		return -1;


	int start = 1;
	int end = length - 1;
	while (start <= end) {
		int middle = ((end - start) >> 1) + start;
		int count = countRange(number, length, start, middle);
		if (start == end) {
			if (count > 1)
				return start;
			else
				break;
		}
		if (count > 1)
			end = middle;
		else
			start = middle + 1;
	}
	return -1;
}

void test(const char* testName, int* numbers, int length, int* duplications, int dupLength) {
	int result = getDuplication(numbers, length);
	for (int i = 0; i < dupLength; ++i) {
		if (result == duplications[i]) {
			cout << testName << "  Passed!" << endl;
			return;
		}
	}

	cout << testName << " Failed!" << endl;
}

//多个重复的数字
void test1() {
	int array[] = { 2, 3, 5, 4, 3, 2, 6, 7 };
	int duplication[] = { 2,3 };
	test("test1", array, sizeof(array) / sizeof(int), duplication, sizeof(duplication) / sizeof(int));
}

//没有重复的数字
void test2() {
	int array[] = { 1,2,3,4,9,8 };
	int duplication[] = { -1 };
	test("Test2", array, sizeof(array) / sizeof(int), duplication, sizeof(duplication) / sizeof(int));

}

//无效输入
void test3() {
	int* array = nullptr;
	int duplication[] = { 1,2 };
	test("Test3", array, 0, duplication, sizeof(duplication) / sizeof(int));
}

int main() {
	test1();
	test2();
	test3();
}


```

