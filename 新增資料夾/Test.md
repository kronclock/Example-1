```cpp
#include <iostream>
using namespace std;

class MinHeap {
private:
	int heap[100];
	int size;

	void swap(int& a, int& b) {
		int t = a;
		a = b;
		b = t;
	}

	void heapifyUp(int i) {
		while (i > 0 && heap[(i - 1) / 2] > heap[i]) {
			swap(heap[(i - 1) / 2], heap[i]);
			i = (i - 1) / 2;
		}
	}

	void heapifyDown(int i) {
		int small = i;
		int left = i * 2 + 1;
		int right = i * 2 + 2;

		if (left < size && heap[left] < heap[small])
			small = left;
		if (right < size && heap[right] < heap[small])
			small = right;
		if (small != i) {
			swap(heap[small], heap[i]);
			heapifyDown(small);
		}
	}

public:
	MinHeap() {
		size = 0;
	}

	void push(int val) {
		heap[size++] = val;
		heapifyUp(size - 1);
	}

	int pop() {
		int minVal = heap[0];
		heap[0] = heap[--size];
		heapifyDown(0);
		return minVal;
	}

	int getSize() {
		return size;
	}
};

int main() {
	int n;
	cin >> n;

	int a[100];
	for (int i = 0; i < n; i++)
		cin >> a[i];

	MinHeap h;
	for (int i = 0; i < n; i++)
		h.push(a[i]);

	while (h.getSize() > 1) {
		int x = h.pop();
		int y = h.pop();
		int sum = x + y;
		cout << x << " + " << y << " = " << sum << endl;
		h.push(sum);
	}
	return 0;
}

```
