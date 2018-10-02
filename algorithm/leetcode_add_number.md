### leetcode 2

```
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode *t1 = l1, *t2 = l2;
        int carry = 0;
        ListNode *head = new ListNode(0);
        ListNode *t3 = head;
        while(t1 != nullptr || t2 != nullptr || carry == 1)
        {
            if(t1 != nullptr)
            {
                carry += t1->val;
                t1 = t1->next;
            }
            if(t2 != nullptr)
            {
                carry += t2->val;
                t2 = t2->next;
            }
            ListNode *t = new ListNode(carry % 10);
            t3->next = t;
            t3 = t3->next;
            carry /= 10;
        }
        t3->next = NULL;
        return head->next;
    }
};
```

### leetcode 67
```
class Solution {
public:
    string addBinary(string a, string b) {
        string sum = "";
        int flag = 0;
        int i = a.length() - 1;
        int j = b.length() - 1;
        while (flag==1 || i>=0 || j>=0)
        {
            if (i >= 0)
                flag = flag + a[i--] - '0';
            if (j >= 0)
                flag = flag + b[j--] - '0';
            sum = char(flag%2+'0') + sum;
            flag = flag / 2;
        }
        return sum;
    }
}; 
```

### 总结
结题结构都是相同的，while循环里进行判断即可
