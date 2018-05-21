---
layout: post
title: "C的练习"
subtitle: "数据结构相关算法或策略"
published: true
---

## 1. 求n的阶乘
```
int function(int number) {
    int result = 1;
    if (number <= 1)
    return result;
    result = number * function(number - 1);
}

int main()
{
    int a = 0;
    cin >> a;
    cout << function(a) << endl;
    return 0;
}
```
## 2. 堆排序
```
void HeapAdjust(int *data, int s, int len) {
	int temp = *(data + s);
	for (int j = 2 * s; j < len; j *= 2) {
		if (j < len && *(data + j) < *(data + j + 1)) {
			j++;
		}
		if (temp > *(data + j)) {
			break;
		}
		*(data + s) = *(data + j);
		s = j;
	}
	*(data + s) = temp;
}

void swap(int *data, int a, int b) {
	int temp = 0;
	temp = *(data + a);
	*(data + a) = *(data + b);
	*(data + b) = temp;
}

int main() {
	int data[8] = { 4,2,3,7,8,1,11,5 };
	int len = 8;
	for (int i = (len - 1) / 2; i >= 0; i--) {
		HeapAdjust(data, i, len);
	}
	for (int i = len - 1; i >= 1; i--) {
		swap(data, 0, i);
		HeapAdjust(data, 0, i - 1);
	}
	for (int i = 0; i < len; i++) {
		cout << data[i] <<endl;
	}

	return 0;
}
```
## 3. 快速排序
```
void swap(int *data, int a, int b) {
	int temp = 0;
	temp = *(data + a);
	*(data + a) = *(data + b);
	*(data + b) = temp;
}

int Partition(int *data, int low, int high) {
	int temp = *(data + low);

	while (low < high) {
		while (low < high && *(data + high) >= temp) {
			high--;
		}
		swap(data, low, high);
		while (low < high && *(data + low) <= temp) {
			low++;
		}
		swap(data, low, high);
	}
	return low;
}

void QuickSort(int *data, int low, int high) {
	int partition_value = 0;
	if (low < high) {
		partition_value = Partition(data, low, high);
		QuickSort(data, low, partition_value - 1);
		QuickSort(data, partition_value + 1, high);
	}
}
```
## 4. 折半查找
```
int BinarySearch(int *data, int len, int key) {
	int mid = 0;
	int low = 0;
	int high = len - 1;

	while (low <= high) {
		mid = (low + high) / 2;

		if (*(data + mid) < key) {
			low = mid + 1;
		}
		else if (*(data + mid) > key) {
			high = mid - 1;
		}
		else {
			return mid;
		}
	}
	return 0;
}

int main() {
	int num[] = { 2,4,6,8,9,12,34 };

	cout << BinarySearch(num, 7, 2) << endl;
}
```
## 5. 二进制数有多少个1
```
int main() {
    unsigned int num = 60;
    int count = 0;
    while (num != 0) {
        if (num % 2 == 1) {
            count++;
        }
        num /= 2;
    }
    cout << count << endl;
    return 0;
}
```
## 6. 最大公约数
```
int gcd(int x, int y) {
    if (y == 0) {
        return x;
    }
    else {
        gcd(y, x%y);
    }
}

int main() {
    int x = 0, y = 0;
    cin >> x >> y;
    cout << gcd(x, y) << endl;
    return 0;
}
```
## 7. 计算字符串的熵
```
int main() {
    #define MAXLENGTH 200
    char input[MAXLENGTH] = { 0 };
    char c = getchar();
    int count = 0;
    int input_len = 0;

    while (c != '\n') {
        input[count] = c;
        c = getchar();
        count++;
    }
    input_len = count;

    char input_spec[MAXLENGTH] = { 0 };
    int input_spec_len[MAXLENGTH] = { 0 };
    int spec_len = 0;

    input_spec[0] = input[0];
    input_spec_len[0] = 1;
    spec_len = 1;

    for (int i = 1; i < input_len; i++) {
        for (int j = 0; j < spec_len; j++) {
        if (input[i] == input_spec[j]) {
            input_spec_len[j]++;
            break;
        }
        if (input[i] != input_spec[j] && j == spec_len - 1) {
            input_spec[spec_len] = input[i];
            input_spec_len[spec_len]++;
            spec_len++;
            break;
        }
        }
    }

    double div_pro = 0;
    for (int i = 0; i < spec_len; i++) {
        double pro = (double)(input_spec_len[i]) / (double)(input_len);
        div_pro += (-1)*pro * log2(pro);
    }

    //cout << div_pro << endl;
    printf("%lf", div_pro);

    return 0;
}
```
