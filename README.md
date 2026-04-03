# [cite_start]Teachers' Assessment-02 A [cite: 4]
[cite_start]**Course:** Database Management Systems [cite: 3]
[cite_start]**Topic:** Extendible Hashing [cite: 6]
[cite_start]**Roll Number (RN):** 14 [cite: 11]

---

## 1. Initial Setup and Set Formulation

[cite_start]As per the instructions, the initial key set is modified by substituting the roll number (RN = 14)[cite: 10, 11, 23].

[cite_start]**Original Set:** K = {69, 22, 16, 27, 50, 23, RN, 70, 25} [cite: 10]

**Modified Set:** K = {69, 22, 16, 27, 50, 23, **14**, 70, 25}

*Note: The hash table uses the Least Significant Bits (LSB) of the binary representation for directory mapping. Bucket capacity is 3.*

---

## 2. Step-by-Step Insertion Process

**Initial State:** Global Depth (GD) = 1
* [cite_start]Directory `0` -> Bucket 0 (LD=1): [24, 30, 88] [cite: 13, 14, 15, 16]
* [cite_start]Directory `1` -> Bucket 1 (LD=1): [49, 87, 29] [cite: 17, 19, 20, 21]

**Step 1: Insert 69** (Binary: 1000101 -> ends in `01`)
* Maps to `1`. Bucket is full. 
* Split Bucket 1 (Local Depth becomes 2). Global Depth becomes 2.
* `01` -> [49, 29, 69]
* `11` -> [87]

**Step 2: Insert 22** (Binary: 10110 -> ends in `10`)
* Maps to `0`. Bucket is full. 
* Split Bucket 0 (Local Depth becomes 2). Global Depth remains 2.
* `00` -> [24, 88]
* `10` -> [30, 22]

**Step 3: Insert 16** (Binary: 10000 -> ends in `00`)
* Maps to `00`. Inserted directly. 
* `00` -> [24, 88, 16] (Bucket full)

**Step 4: Insert 27** (Binary: 11011 -> ends in `11`)
* Maps to `11`. Inserted directly. 
* `11` -> [87, 27]

**Step 5: Insert 50** (Binary: 110010 -> ends in `10`)
* Maps to `10`. Inserted directly. 
* `10` -> [30, 22, 50] (Bucket full)

**Step 6: Insert 23** (Binary: 10111 -> ends in `11`)
* Maps to `11`. Inserted directly. 
* `11` -> [87, 27, 23] (Bucket full)

**Step 7: Insert 14 (RN)** (Binary: 1110 -> ends in `110`)
* Maps to `10`. Bucket is full. 
* Split Bucket `10` (Local Depth becomes 3). Global Depth becomes 3.
* `010` -> [50]
* [cite_start]`110` -> [30, 22, **==14==**] *(Insertion of RN Highlighted)* [cite: 24]

**Step 8: Insert 70** (Binary: 1000110 -> ends in `110`)
* Maps to `110`. Bucket is full. 
* Split Bucket `110` (Local Depth becomes 4). Global Depth becomes 4.
* `0110` -> [22, 70]
* [cite_start]`1110` -> [30, **==14==**] *(Insertion of RN Highlighted)* [cite: 24]

**Step 9: Insert 25** (Binary: 11001 -> ends in `001`)
* Maps to `01`. Bucket is full. 
* Split Bucket `01` (Local Depth becomes 3). Global Depth remains 4.
* `001` -> [49, 25]
* `101` -> [29, 69]

---

## 3. Final Extendible Hash Table Diagram

**GLOBAL DEPTH = 4**

```text
Directory                               Buckets (Capacity = 3)
---------                               ----------------------
[0000] \
[0100] ------>  [ 24 | 88 | 16 ]  Local Depth = 2
[1000] ------>  
[1100] /

[0011] \
[0111] ------>  [ 87 | 27 | 23 ]  Local Depth = 2
[1011] ------>  
[1111] /

[0001] ------>  [ 49 | 25 |    ]  Local Depth = 3
[1001] /

[0101] ------>  [ 29 | 69 |    ]  Local Depth = 3
[1101] /

[0010] ------>  [ 50 |    |    ]  Local Depth = 3
[1010] /

[0110] ------>  [ 22 | 70 |    ]  Local Depth = 4

[1110] ------>  [ 30 | 14 |    ]  Local Depth = 4