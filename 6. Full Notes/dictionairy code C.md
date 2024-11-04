
2024-10-17 14:39

Status:

Tags:[[C]], [[Two sum]],

# dictionary code C

```
// Define the size of the hash map

#define HASH_SIZE 1000

  

// Define a struct for each node in the hash map for chaining (to handle collisions)

typedef struct HashNode {

    int key;    // The value in nums array

    int value;  // The index of the value

    struct HashNode* next;

} HashNode;

  

// Hash function to map keys to a valid index

int hash(int key) {

    return abs(key) % HASH_SIZE;

}

  

// Insert a key-value pair into the hash map

void insert(HashNode** hashMap, int key, int value) {

    int idx = hash(key);

    HashNode* newNode = (HashNode*)malloc(sizeof(HashNode));

    newNode->key = key;

    newNode->value = value;

    newNode->next = hashMap[idx];

    hashMap[idx] = newNode;

}

  

// Find a key in the hash map

int find(HashNode** hashMap, int key) {

    int idx = hash(key);

    HashNode* current = hashMap[idx];

    while (current) {

        if (current->key == key) {

            return current->value;  // Return the index (value) if found

        }

        current = current->next;

    }

    return -1;  // Return -1 if not found

}

  

int* twoSum(int* nums, int numsSize, int target, int* returnSize) {

    // Initialize the hash map

    HashNode* hashMap[HASH_SIZE] = { NULL };

    *returnSize = 2;

    // Allocate space for the result

    int* res = (int*)malloc(2 * sizeof(int));

  

    // Traverse the array

    for (int i = 0; i < numsSize; i++) {

        int complement = target - nums[i];  // The number we need to find

        int complementIndex = find(hashMap, complement);  // Look for the complement in the hash map

  

        if (complementIndex != -1) {

            // If the complement is found, return the indices

            res[0] = complementIndex;

            res[1] = i;

            return res;

        }

        // Insert the current number and its index into the hash map

        insert(hashMap, nums[i], i);

    }

  

    // If no solution, return NULL

    *returnSize = 0;

    free(res);

    return NULL;

}

  

// Free the memory allocated for the hash map

void freeHashMap(HashNode** hashMap) {

    for (int i = 0; i < HASH_SIZE; i++) {

        HashNode* current = hashMap[i];

        while (current) {

            HashNode* temp = current;

            current = current->next;

            free(temp);

        }

    }

}
```
