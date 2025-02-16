# 数据结构

- 数据结构的职责就是增删查改，再无其他。

## 数组
### 静态数组
- 「静态数组」就是一块连续的内存空间，我们可以通过索引来访问这块内存空间中的元素，这才是数组的原始形态。

```C++
// 定义一个大小为 10 的静态数组
int arr[10];
// 1、在内存中开辟了一段连续的内存空间，大小是 10 * sizeof(int) 字节。一个 int 在计算机内存中占 4 字节，也就是总共 40 字节。
// 2、定义了一个名为 arr 的数组指针，指向这段内存空间的首地址。

// 用 memset 函数把数组的值初始化为 0
memset(arr, 0, sizeof(arr));

// 使用索引赋值
arr[0] = 1;
arr[1] = 2;
// 1、计算 arr 的首地址加上 1 * sizeof(int) 字节（4 字节）的偏移量，找到了内存空间中的第二个元素的首地址。
// 2、从这个地址开始的 4 个字节的内存空间中写入了整数 2。

// 使用索引取值
int a = arr[0];
```

- 数组的插入
- 对于指定索引插入，直接赋值即可，时间复杂度为 O(1)
- 对于中间插入，需要将插入位置后的元素后移，时间复杂度为 O(n)

- 数组的删除
- 对于指定索引删除，直接赋值为默认值即可，时间复杂度为 O(1)

综上，静态数组的增删查改操作的时间复杂度是：

- 增：
  - 在末尾追加元素：O(1)。
  - 在中间（非末尾）插入元素：O(N)。
- 删：
  - 删除末尾元素：O(1)。
  - 删除中间（非末尾）元素：O(N)。
- 查：给定指定索引，查询索引对应的元素的值，时间复杂度 O(1)。
- 改：给定指定索引，修改索引对应的元素的值，时间复杂度 O(1)。

![image.png](image.png)

### 动态数组

C++常用函数
```C++
// 创建动态数组
// 不用显式指定数组大小，它会根据实际存储的元素数量自动扩缩容
vector<int> arr;

for (int i = 0; i < 10; i++) {
    // 在末尾追加元素，时间复杂度 O(1)
    arr.push_back(i);
}

// 在中间插入元素，时间复杂度 O(N)
// 在索引 2 的位置插入元素 666
arr.insert(arr.begin() + 2, 666);

// 在头部插入元素，时间复杂度 O(N)
arr.insert(arr.begin(), -1);

// 删除末尾元素，时间复杂度 O(1)
arr.pop_back();

// 删除中间元素，时间复杂度 O(N)
// 删除索引 2 的元素
arr.erase(arr.begin() + 2);

// 根据索引查询元素，时间复杂度 O(1)
int a = arr[0];

// 根据索引修改元素，时间复杂度 O(1)
arr[0] = 100;

// 根据元素值查找索引，时间复杂度 O(N)
int index = find(arr.begin(), arr.end(), 666) - arr.begin();
```

## 链表
- 常见 LeetCode 单链表
```C++
class ListNode {
    public:
        int val;
        ListNode *next; 
        ListNode(int x) : val(x), next(NULL) {}
};
```
- 基于数组创建的单链表
```C++
class ListNode {
public:
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};

// 输入一个数组，转换为一条单链表
ListNode* createLinkedList(std::vector<int> arr) {
    if (arr.empty()) {
        return nullptr;
    }
    ListNode* head = new ListNode(arr[0]);
    ListNode* cur = head;
    for (int i = 1; i < arr.size(); i++) {
        cur->next = new ListNode(arr[i]);
        cur = cur->next;
    }
    return head;
}
```
- 基于数组创建的双链表
```C++
class DoublyListNode {
public:
    int val;
    DoublyListNode *next, *prev;
    DoublyListNode(int x) : val(x), next(NULL), prev(NULL) {}
};

DoublyListNode* createDoublyLinkedList(vector<int>& arr) {
    if (arr.empty()) {
        return NULL;
    }
    DoublyListNode* head = new DoublyListNode(arr[0]);
    DoublyListNode* cur = head;
    // for 循环迭代创建双链表
    for (int i = 1; i < arr.size(); i++) {
        DoublyListNode* newNode = new DoublyListNode(arr[i]);
        cur->next = newNode;
        newNode->prev = cur;
        cur = cur->next;
    }
    return head;
}
```

## 环形数组
- 环形数组技巧利用求模（余数）运算，将普通数组变成逻辑上的环形数组，可以让我们用 O(1) 的时间在数组头部增删元素。
- 环形数组的关键在于，它维护了两个指针 start 和 end，start 指向第一个有效元素的索引，end 指向最后一个有效元素的下一个位置索引。
- 这样，当我们在数组头部添加或删除元素时，只需要移动 start 索引，而在数组尾部添加或删除元素时，只需要移动 end 索引。
- 当 start, end 移动超出数组边界（< 0 或 >= arr.length）时，我们可以通过求模运算 % 让它们转一圈到数组头部或尾部继续工作，这样就实现了环形数组的效果。

代码实现
- 这里的关键在于需要理解左闭右开的概念
    - 因为这样初始化 start = end = 0 时，区间 [0, 0) 中没有元素，但只要让 end 向右移动（扩大）一位，区间 [0, 1) 就包含一个元素 0 了。
- 注意环形数组的取值每次都会计算 %，因此效率上是比较低的
```C++
#include <iostream>
#include <stdexcept>
#include <ostream>

template<typename T>
class CycleArray {
    std::unique_ptr<T[]> arr;
    int start;
    int end;
    int count;
    int size;

    // 自动扩缩容辅助函数
    void resize(int newSize) {
        // 创建新的数组
        std::unique_ptr<T[]> newArr = std::make_unique<T[]>(newSize);
        // 将旧数组的元素复制到新数组中
        for (int i = 0; i < count; ++i) {
            newArr[i] = arr[(start + i) % size];
        }
        arr = std::move(newArr);
        // 重置 start 和 end 指针
        start = 0;
        end = count;
        size = newSize;
    }

public:
    CycleArray() : CycleArray(1) {
    }

    explicit CycleArray(int size) : start(0), end(0), count(0), size(size) {
        arr = std::make_unique<T[]>(size);
    }

    // 在数组头部添加元素，时间复杂度 O(1)
    void addFirst(const T &val) {
        // 当数组满时，扩容为原来的两倍
        if (isFull()) {
            resize(size * 2);
        }
        // 因为 start 是闭区间，所以先左移，再赋值
        start = (start - 1 + size) % size;
        arr[start] = val;
        count++;
    }

    // 删除数组头部元素，时间复杂度 O(1)
    void removeFirst() {
        if (isEmpty()) {
            throw std::runtime_error("Array is empty");
        }
        // 因为 start 是闭区间，所以先赋值，再右移
        arr[start] = T();
        start = (start + 1) % size;
        count--;
        // 如果数组元素数量减少到原大小的四分之一，则减小数组大小为一半
        if (count > 0 && count == size / 4) {
            resize(size / 2);
        }
    }

    // 在数组尾部添加元素，时间复杂度 O(1)
    void addLast(const T &val) {
        if (isFull()) {
            resize(size * 2);
        }
        // 因为 end 是开区间，所以是先赋值，再右移
        arr[end] = val;
        end = (end + 1) % size;
        count++;
    }

    // 删除数组尾部元素，时间复杂度 O(1)
    void removeLast() {
        if (isEmpty()) {
            throw std::runtime_error("Array is empty");
        }
        // 因为 end 是开区间，所以先左移，再赋值
        end = (end - 1 + size) % size;
        arr[end] = T();
        count--;
        // 缩容
        if (count > 0 && count == size / 4) {
            resize(size / 2);
        }
    }

    // 获取数组头部元素，时间复杂度 O(1)
    T getFirst() const {
        if (isEmpty()) {
            throw std::runtime_error("Array is empty");
        }
        return arr[start];
    }

    // 获取数组尾部元素，时间复杂度 O(1)
    T getLast() const {
        if (isEmpty()) {
            throw std::runtime_error("Array is empty");
        }
        // end 是开区间，指向的是下一个元素的位置，所以要减 1
        return arr[(end - 1 + size) % size];
    }

    bool isFull() const {
        return count == size;
    }

    int getSize() const {
        return count;
    }

    bool isEmpty() const {
        return count == 0;
    }
};
```