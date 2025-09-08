# 📝 C Pointer Cheatsheet

## 📌 Basics
- **Pointer declaration:**
  ```c
  int *p;   // pointer to int
  char *c;  // pointer to char
  ```
- **Address-of (`&`)**: gives the address.
  ```c
  int x = 10;
  int *p = &x;   // p holds address of x
  ```
- **Dereference (`*`)**: access the value at that address.
  ```c
  printf("%d", *p); // prints 10
  *p = 20;          // modifies x
  ```

---

## 📌 Pointer Arithmetic
- Works in **units of type size**, not bytes.
  ```c
  int arr[5] = {1,2,3,4,5};
  int *p = arr;
  printf("%d", *(p+2)); // 3
  ```
- Difference between pointers → number of elements:
  ```c
  int n = (&arr[4] - &arr[0]); // n = 4
  ```

---

## 📌 Arrays & Pointers
- `arr` **decays** to pointer to first element (`&arr[0]`).
- But `sizeof(arr)` ≠ `sizeof(p)`:
  ```c
  int arr[10];
  int *p = arr;
  sizeof(arr); // 40 (if int = 4 bytes)
  sizeof(p);   // 8 (on 64-bit system)
  ```

---

## 📌 Common Pointer Tricks
1. **Swap using pointers**
   ```c
   void swap(int *a, int *b) {
       int temp = *a;
       *a = *b;
       *b = temp;
   }
   ```

2. **Dynamic memory allocation**
   ```c
   int *p = malloc(5 * sizeof(int));
   free(p);
   ```

3. **Pointer to pointer**
   ```c
   int x = 5;
   int *p = &x;
   int **pp = &p;
   printf("%d", **pp); // 5
   ```

---

## 📌 Pitfalls 🚩
- **Uninitialized pointers (wild pointers):**
  ```c
  int *p;  // undefined value
  *p = 10; // crash
  ```
  ✅ Always initialize to `NULL` or valid address.

- **Dangling pointers:**
  Using freed memory.
  ```c
  int *p = malloc(4);
  free(p);
  *p = 10; // ❌ undefined
  ```

- **Out-of-bounds access:**
  ```c
  int arr[3];
  int *p = arr;
  printf("%d", *(p+5)); // ❌ UB
  ```

- **Mixing malloc/free with new/delete (C++ only).**
  Stick to one style.

---

## 📌 Best Practices ✅
- Always initialize pointers:
  ```c
  int *p = NULL;
  ```
- Check before dereferencing:
  ```c
  if (p != NULL) { ... }
  ```
- Use `sizeof(*p)` when allocating:
  ```c
  int *p = malloc(10 * sizeof(*p));
  ```
- Free memory once and set to `NULL`.
- Use `const` with pointers to protect values:
  ```c
  const int *p;    // value read-only
  int * const p;   // address read-only
  ```

---

## 📌 Quick Reference
- `*p` → value at address  
- `&x` → address of variable  
- `p[i]` ⇔ `*(p+i)`  
- `**pp` → value at pointer-to-pointer  

---

⚡ **Pointers are powerful but dangerous.**  
Think of them like loaded guns: precise in skilled hands, catastrophic otherwise.
