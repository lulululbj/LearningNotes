最基本的几种数据结构。




# 背包、队列和栈

## 集合数据类型的定义

### 背包（Bag）

背包是一种不支持从中删除元素的集合数据类型——它的目的是帮助用例收集元素并迭代遍历所有收集到的元素（用例也可以检查背包是否为空或者获取背包中元素的数量）。迭代的顺序不确定且与用例无关。可以想象成一个装球的背包，我们可以放入球，获取球的数量，遍历球。

### 先进先出队列（Queue）

先进先出队列是一种基于先进先出（FIFO）策略的集合类型。队列在保存元素的同时保存它们的相对顺序：使它们入列顺序和出列顺序相同。队列在生活和编程中极其常见，就像排队，先进入队伍的总是先出去。

### 下压栈（Stack）

下压栈是一种基于后进先出（LIFO）策略的集合类型，当使用 foreach 语句遍历栈中的元素时，元素的处理顺序和它们被压入的顺序正好相反。就像我们的邮箱，后进来的邮件总是会先看到。

## 集合数据类型的实现

### 栈的简单数组实现

下面是一个下压栈的简单数组实现，比较简单，直接看代码：

	public class Stack<T> implements Iterable<T> {

    	private T[] a = (T[]) new Object[1]; // 栈元素
    	private int n = 0; // 元素数量

    	public boolean isEmpty() {
        	return n == 0;
    	}

    	public int size() {
        	return n;
    	}

    	// 向栈顶添加元素
    	public void push(T item) {
        	if (n == a.length) resize(n*2);
        	a[n++] = item;
    	}

    	// 从栈顶删除元素
    	public T pop() {
        	T t = a[--n];
        	a[n] = null; // 释放已删除对象
        	if (n > 0 && n == a.length / 4) resize(a.length / 2);
        	return t;
    	}

    	// 扩容
    	private void resize(int max) {
        	T[] temp = (T[]) new Object[max];
        	for (int i = 0; i < n; i++) {
            	temp[i] = a[i];
        	}
        	a = temp;
    	}

    	// 支持 foreach
    	@Override
    	public Iterator<T> iterator() {
        	return new ReverseArrayIterator();
    	}


    	private class ReverseArrayIterator implements Iterator<T> {
        	int i = n;

        	@Override
        	public boolean hasNext() {
        	    return i > 0;
        	}

        	@Override
        	public T next() {
        	    return a[--i];
        	}
    	}
	}

典型的 **Arraylist** 的实现机制就类似于此。这个下压栈的缺点是 push 和 pop 会调整数组的大小，耗时和栈大小成正比。就像 ArrayList 在队首进行插入操作。相对应的可以快速进行插入和删除操作的数据结构就是 **链表** 了。

### 链表

链表是一种递归的数据结构，它或者为空（null），或者是指向一个结点（node）的引用，该结点含有一个泛型的元素和一个指向另一条链表的引用。下图是单链表的简单表示：

![单链表的简单表示](http://ofdkfbou7.bkt.clouddn.com/blog/lianbiao.png)

链表表示的是一列元素。在列表中向序列插入元素或是删除元素很方便。例如在表头插入一个结点，在数组实现的队列中，需要将队列中的每一位元素后移。而在链表中，只需新建一个结点，将结点的引用指向原来的 First 结点就可以了，它所需的时间与链表长度无关。同理，在表头删除一个元素更加简单，只需要解除第一个结点的引用即可。

### 下压堆栈的链表实现（后进先出）

	public class Stack2<T> implements Iterable<T> {

    	private Node first; // 栈顶（最近添加的元素）
    	private int n; // 元素数量

    	private class Node {
    	    T t; // 当前节点元素
    	    Node next; // 下一节点的引用
    	}

    	private boolean isEmpty() {
    	    return n == 0;
    	}

    	private int size() {
    	    return n;
    	}

    	public void push(T t) {
    	    Node oldFirst = first;
    	    first = new Node();
    	    first.t = t;
    	    first.next = oldFirst;
    	    n++;
    	}

    	public T pop() {
    	    T t = first.t;
    	    first = first.next;
    	    n--;
    	    return t;
    	}

    	@Override
    	public Iterator<T> iterator() {
    	    return new ListIterator();
    	}


    	private class ListIterator implements Iterator<T> {

    	    private Node current = first;

    	    @Override
    	    public boolean hasNext() {
    	        return current != null;
    	    }

    	    @Override
    	    public T next() {
    	        T t = current.t;
    	        current = current.next;
    	        return t;
    	    }
    	}
	}

### 先进先出队列的链表实现


	public class Queue<T> implements Iterable<T> {

	    private Node first;
	    private Node last;
	    private int n;

	    private class Node {
	        T t;
	        Node next;
	    }

	    public boolean isEmpty() {
	        return n == 0;
	    }

	    public int size() {
	        return n;
	    }

	    // 队尾添加元素
	    public void enqueue(T t) {
	        Node oldLast = last;
	        last = new Node();
	        last.t = t;
	        last.next = null;

	        if (isEmpty()) first = last;
	        else oldLast.next = last;

	        n++;
	    }

	    // 队首删除元素
	    public T dequeue() {
	        T t = first.t;
	        first = first.next;
	        if (isEmpty()) last = null;
	        n--;
	        return t;
	    }

	    @Override
	    public Iterator<T> iterator() {
		        return new QueueIterator();
	    }

	    public class QueueIterator implements Iterator<T> {

	        private Node current = first;

	        @Override
	        public boolean hasNext() {
	            return current != null;
	        }

	        @Override
	        public T next() {
	            T t = current.t;
	            current = current.next;
	            return t;
	        }
	    }
	}

数组和链表是两种非常基础的数据结构，常被称为顺序存储和链式存储。对于数组而言，通过索引就可以直接访问任意元素，但在初始化时就需要知道元素的数量，不可避免的要进行相应的扩容操作。对于链表而言，使用的空间大小和元素数量成正比，但是需要通过引用访问任意元素。
