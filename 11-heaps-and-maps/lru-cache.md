# ⭐ LRU Cache

{% embed url="https://www.interviewbit.com/problems/lru-cache/" %}

```cpp
#include <bits/stdc++.h>
using namespace std;

void print(int d) { cout << d << endl; }
void print(string s) { cout << s << endl; }

class Node {
public:
  int key;
  int value;
  Node *next;
  Node *prev;

  Node(int key, int value) {
    this->key = key;
    this->value = value;
    this->next = nullptr;
    this->prev = nullptr;
  }
};

Node *head = new Node(0, 0);
Node *tail = new Node(0, 0);

void show() {

  cout << "{ ";
  Node *ptr = head->next;
  while (ptr != tail) {
    cout << "{" << ptr->key << ", " << ptr->value << "} ";
    ptr = ptr->next;
  }

  cout << "}\n";
}

void deleteNode(Node *node) {
  Node *before = node->prev;
  Node *after = node->next;
  before->next = after;
  after->prev = before;
}

void insertAtHead(Node *node) {
  Node *before = head;
  Node *after = head->next;

  before->next = node;
  node->prev = before;

  after->prev = node;
  node->next = after;
}

unordered_map<int, Node *> keyToNode;
int capacity;

void put(int key, int value) {
  if (capacity <= keyToNode.size()) {
    int key = tail->prev->key;
    keyToNode.erase(key);
    deleteNode(tail->prev);
  }

  keyToNode[key] = new Node(key, value);
  insertAtHead(keyToNode[key]);
  show();
}

int get(int key) {
  if (keyToNode.find(key) != keyToNode.end()) {
    Node *node = keyToNode[key];
    deleteNode(node);
    insertAtHead(node);
    cout << node->value << endl;
    return node->value;
  }
  cout << -1 << endl;
  return -1;
}

int main() {
  head->next = tail;
  tail->prev = head;

  capacity = 1;
  put(2, 1);
  get(2);
  put(3, 2);
  get(2);
  get(3);

  return 0;
}
```

Time Complexity: $$O(1)$$​

Space Complexity: $$O(capacity)$$​
