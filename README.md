Problem Statement

Given an array of integers, count the number of inversions in the array.

An inversion occurs when:

arr[i] > arr[j] and i < j

This means a larger element appears before a smaller element in the array.

🧠 Example

Input

arr = [2, 4, 1, 3, 5]

Inversions

(2,1)
(4,1)
(4,3)

Output

3
🚀 Approach

A naive solution would check every pair of elements, resulting in O(n²) time complexity.

A more efficient approach uses Merge Sort, which reduces the complexity to O(n log n).

Key Idea

While merging two sorted arrays:

If a[i] <= b[j] → No inversion

If a[i] > b[j] → Inversions exist

All remaining elements in the left array will also be greater than b[j].

So we add:

count += (a.length - i)
💻 Java Implementation
class Solution {
    static int count;

    static int inversionCount(int arr[]) {
        count = 0;
        mergeSort(arr);
        return count;
    }

    static void mergeSort(int arr[]) {
        int n = arr.length;
        if (n <= 1) return;

        int[] a = new int[n / 2];
        int[] b = new int[n - n / 2];

        for (int i = 0; i < a.length; i++) {
            a[i] = arr[i];
        }

        for (int i = 0; i < b.length; i++) {
            b[i] = arr[i + a.length];
        }

        mergeSort(a);
        mergeSort(b);

        merge(a, b, arr);
    }

    static void merge(int[] a, int[] b, int[] c) {
        int i = 0, j = 0, k = 0;

        while (i < a.length && j < b.length) {
            if (a[i] <= b[j]) {
                c[k++] = a[i++];
            } else {
                c[k++] = b[j++];
                count += (a.length - i);
            }
        }

        while (i < a.length) {
            c[k++] = a[i++];
        }

        while (j < b.length) {
            c[k++] = b[j++];
        }
    }
}
⏱ Time Complexity
Operation	Complexity
Merge Sort	O(n log n)
Counting Inversions	O(n)

Overall Complexity

O(n log n)

Author

Sanjeev Sharma

💻 DSA & Java Developer

🚀 Passionate about Problem Solving

📚 Currently practicing Data Structures & Algorithms
