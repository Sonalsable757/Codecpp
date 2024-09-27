#include <iostream>



using namespace std;



struct ListNode

 {

    int val;

    ListNode *next;

    ListNode(int x) 

           {

              val = x;

              next= nullptr; 

            }

};



ListNode* mergeKLists(ListNode** lists, int k) 

{

    ListNode* mergedList = nullptr;

    ListNode* tail = nullptr;



    while (true)

 {

        int minIndex = -1;



        

        for (int i = 0; i < k; i++) {

            if (lists[i] != nullptr) {

                if (minIndex == -1 || lists[i]->val < lists[minIndex]->val) {

                    minIndex = i;

                }

            }

        }



       

        if (minIndex == -1) {

            break;

        }



        

        ListNode* smallest = lists[minIndex];

        lists[minIndex] = lists[minIndex]->next;



      

        if (mergedList == nullptr) 

        {

            mergedList = smallest;

            tail = smallest;

        } 

       else

       {

            tail->next = smallest;

            tail = tail->next;

        }

    }



    return mergedList;

}





void printList(ListNode* head) 

 {

    while (head) {

        cout << head->val << " -> ";

        head = head->next;

    }

    cout << "nullptr" << endl;

}





ListNode* createList() {

    ListNode* head = nullptr;

    ListNode* tail = nullptr;

    int value;



    cout << "Enter values for the list (end with -1): ";

    while (cin >> value && value != -1) {

        ListNode* newNode = new ListNode(value);

        if (head == nullptr) {

            head = newNode;

            tail = newNode;

        } else {

            tail->next = newNode;

            tail = tail->next;

        }

    }

    return head;

}



int main() {

    int k;



    cout << "Enter the number of lists: ";

    cin >> k;

    ListNode** lists = new ListNode*[k];



    for (int i = 0; i < k; i++) {

        cout << "Creating list " << i + 1 << endl;

        lists[i] = createList();

    }



    ListNode* mergedList = mergeKLists(lists, k);

    cout << "Merged list: ";

    printList(mergedList);

}

