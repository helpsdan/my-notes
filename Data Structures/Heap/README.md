# Binary Tree

## Objective

Explain some concepts about binary heaps. Talk about its definitions. Also implement an MinHeap and a MaxHeap using C#.

## Description

- Rules about Heaps
    1. The parent must be lower/greater than all children nodes.
    2. Is an binary tree.
    3. Must be complete. Which means all nodes should have both left and right children. Except for the bottom level.

## Pros

- Always have an semi sorted structure.
- Min or max values always accessible.
- Both insertion and deletion have log*n complexity.

## Cons

- Complex code, not so simple to understand.

## Examples

- C#  

    ```c#
    class MinHeap<T> {
        int capacity;
        int size;
        Array<T> heapArray;

        public MinHeap(int n){
            this.heapArray = new Array<T>(n);
            this.size = 0;
            this.capacity = n;
        }

        public static void Swap<T>(ref T node_1, ref T node_2)
        {
            T temp = node_1;
            node_1 = node_2;
            node_2 = temp;
        }

        public void Insert(T value) {
            if (size >= n) {
                throw Error("Heap max capacity exceeded");
            }

            int i = size;
            heapArray[i] = value;
            size++;

            while(i != 0 && heapArray[i] < heapArray[Parent(i)]){
                Swap(ref heapArray[i], ref heapArray[Parent(i)]);
                i = Parent(i);
            }
        }

        public T GetMin() {
            return heapArray[0];
        }

        public T ExtractMin() {
            if(size <= 0) {
                throw Error("Cannot extract empty heap");
            }

            if (size == 1)
            {
                size--;
                return heapArray[0];
            }

            T min = heapArray[0];
            heapArray[0] = heapArray[size - 1];
            size--;
            Heapify(0);

            return min;
        }

        public void Heapify(int Key) {
            int left_index = Left(Key);
            int right_index = Right(Key);

            int min_index = Key;

            if(left_index < size && heapArray[left_index] < heapArray[min_index]) {
                smallest = left_index;
            }
            if(right_index < size && heapArray[right_index] < heapArray[min_index]) {
                smallest = right_index;
            }

            if(smallest != key) {
                Swap(ref heapArray[Key], ref heapArray[min_index]);
                Heapify(min_index);
            }
        }

        public int Parent(int Key) {
            return (Key - 1) / 2;
        }

        public int Left(int Key) {
            return 2 * Key + 1;
        }

        public int Right(int Key) {
            return 2 * Key + 2;
        }
    }
    ```

The Implementation to the max heap is the same the only modification is the comparison operator.

## References

- [Binary Heap](https://www.geeksforgeeks.org/binary-heap/)
- [IMPLEMENTANDO uma ÁRVORE BINÁRIA Estruturas de dados #10](https://www.youtube.com/watch?v=6E169kShoNU)
