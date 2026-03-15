#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// 定义图书节点结构体
typedef struct BookNode {
    int bookID;              // 图书编号
    char bookName[50];       // 图书名称
    int borrowerID;          // 借阅人学号
    int status;              // 状态：0表示未借出，1表示已借出
    struct BookNode *next;   // 指向下一个节点的指针
} BookNode;

// 函数声明
BookNode* InitBookList();
void CreateBookList(BookNode **head, int n);
void PrintBookList(BookNode *head);
BookNode* SearchBookByID(BookNode *head, int id);
BookNode* SearchBookByName(BookNode *head, const char *name);
void BorrowBook(BookNode *head, int id, int studentID);
void ReturnBook(BookNode *head, int id);
void FreeBookList(BookNode *head);

int main() {
    BookNode *bookList = NULL;
    int choice, n, bookID, borrowerID;
    char bookName[50];
    BookNode *result = NULL;  // 查找结果

    // 初始化图书信息表
    bookList = InitBookList();
    
    printf("=== 简易图书借阅管理系统 ===\n");

    while (1) {
        // 显示主菜单
        printf("\n请选择操作：\n");
        printf("1. 创建图书信息表（添加n本图书）\n");
        printf("2. 显示所有图书信息\n");
        printf("3. 按书号查找图书\n");
        printf("4. 按书名查找图书\n");
        printf("5. 借阅图书\n");
        printf("6. 归还图书\n");
        printf("0. 退出系统\n");
        printf("请输入选项（0-6）：");
        
        scanf("%d", &choice);
        getchar();  // 清除输入缓冲区中的换行符

        switch (choice) {
            case 1:
                // 创建图书信息表
                printf("请输入要添加的图书数量：");
                scanf("%d", &n);
                if (n <= 0) {
                    printf("数量必须大于0！\n");
                    break;
                }
                CreateBookList(&bookList, n);
                printf("成功添加 %d 本图书。\n", n);
                break;

            case 2:
                // 显示所有图书信息
                printf("\n======= 所有图书信息 =======\n");
                PrintBookList(bookList);
                break;

            case 3:
                // 按书号查找图书
                if (bookList == NULL) {
                    printf("当前没有图书信息，请先添加图书！\n");
                    break;
                }
                
                printf("请输入要查找的书号：");
                scanf("%d", &bookID);
                
                result = SearchBookByID(bookList, bookID);
                if (result != NULL) {
                    printf("\n========= 找到图书 =========\n");
                    printf("书号：%d\n", result->bookID);
                    printf("书名：%s\n", result->bookName);
                    printf("借阅人学号：%d\n", result->borrowerID);
                    printf("状态：%s\n", result->status ? "已借出" : "未借出");
                    printf("==========================\n");
                } else {
                    printf("未找到书号为 %d 的图书！\n", bookID);
                }
                break;

            case 4:
                // 按书名查找图书
                if (bookList == NULL) {
                    printf("当前没有图书信息，请先添加图书！\n");
                    break;
                }
                
                printf("请输入要查找的书名：");
                fgets(bookName, sizeof(bookName), stdin);
                // 移除fgets读取的换行符
                bookName[strcspn(bookName, "\n")] = '\0';

                result = SearchBookByName(bookList, bookName);
                if (result != NULL) {
                    printf("\n========= 找到图书 =========\n");
                    printf("书号：%d\n", result->bookID);
                    printf("书名：%s\n", result->bookName);
                    printf("借阅人学号：%d\n", result->borrowerID);
                    printf("状态：%s\n", result->status ? "已借出" : "未借出");
                    printf("==========================\n");
                } else {
                    printf("未找到书名为 \"%s\" 的图书！\n", bookName);
                }
                break;

            case 5:
                // 借阅图书
                if (bookList == NULL) {
                    printf("当前没有图书信息，请先添加图书！\n");
                    break;
                }
                
                printf("请输入要借阅的书号：");
                scanf("%d", &bookID);
                printf("请输入您的学号：");
                scanf("%d", &borrowerID);
                
                BorrowBook(bookList, bookID, borrowerID);
                break;

            case 6:
                // 归还图书
                if (bookList == NULL) {
                    printf("当前没有图书信息，请先添加图书！\n");
                    break;
                }
                
                printf("请输入要归还的书号：");
                scanf("%d", &bookID);
                
                ReturnBook(bookList, bookID);
                break;

            case 0:
                // 退出系统
                printf("\n感谢使用图书借阅管理系统！\n");
                printf("正在释放内存...\n");
                FreeBookList(bookList);
                printf("程序已退出，再见！\n");
                return 0;

            default:
                printf("无效的选择，请输入0-6之间的数字！\n");
        }
    }
    
    return 0;
}

// 函数定义

// 初始化图书信息表
BookNode* InitBookList() {
    return NULL;  // 返回空链表
}

// 创建图书信息表（添加n本图书）
void CreateBookList(BookNode **head, int n) {
    for (int i = 0; i < n; i++) {
        BookNode *newNode = (BookNode *)malloc(sizeof(BookNode));
        
        printf("\n=== 输入第 %d 本书的信息 ===\n", i + 1);
        
        // 输入书号
        printf("书号：");
        scanf("%d", &newNode->bookID);
        getchar();  // 清除输入缓冲区中的换行符
        
        // 输入书名
        printf("书名：");
        fgets(newNode->bookName, sizeof(newNode->bookName), stdin);
        newNode->bookName[strcspn(newNode->bookName, "\n")] = '\0';  // 移除换行符
        
        // 初始化借阅信息
        newNode->borrowerID = 0;  // 初始化为未借出
        newNode->status = 0;      // 初始化为未借出
        
        // 头插法插入链表
        newNode->next = *head;
        *head = newNode;
    }
}

// 输出图书信息表
void PrintBookList(BookNode *head) {
    if (head == NULL) {
        printf("当前没有图书信息！\n");
        return;
    }
    
    BookNode *current = head;
    int count = 1;
    
    printf("序号\t书号\t书名\t\t\t借阅人学号\t状态\n");
    printf("----------------------------------------------------------\n");
    
    while (current != NULL) {
        printf("%d\t", count);
        printf("%d\t", current->bookID);
        printf("%-20s\t", current->bookName);
        printf("%d\t\t", current->borrowerID);
        printf("%s\n", current->status ? "已借出" : "未借出");
        
        current = current->next;
        count++;
    }
    printf("总共 %d 本图书\n", count - 1);
}

// 按书号查找图书
BookNode* SearchBookByID(BookNode *head, int id) {
    BookNode *current = head;
    
    while (current != NULL) {
        if (current->bookID == id) {
            return current;
        }
        current = current->next;
    }
    
    return NULL;
}

// 按书名查找图书
BookNode* SearchBookByName(BookNode *head, const char *name) {
    BookNode *current = head;
    
    while (current != NULL) {
        if (strcmp(current->bookName, name) == 0) {
            return current;
        }
        current = current->next;
    }
    
    return NULL;
}

// 借阅图书
void BorrowBook(BookNode *head, int id, int studentID) {
    BookNode *book = SearchBookByID(head, id);
    
    if (book == NULL) {
        printf("未找到书号为 %d 的图书！\n", id);
        return;
    }
    
    if (book->status == 1) {
        printf("图书《%s》已被学号 %d 的读者借出，无法再次借阅！\n", 
               book->bookName, book->borrowerID);
        return;
    }
    
    book->borrowerID = studentID;
    book->status = 1;
    printf("图书《%s》已成功借阅给学号为 %d 的读者。\n", book->bookName, studentID);
}

// 归还图书
void ReturnBook(BookNode *head, int id) {
    BookNode *book = SearchBookByID(head, id);
    
    if (book == NULL) {
        printf("未找到书号为 %d 的图书！\n", id);
        return;
    }
    
    if (book->status == 0) {
        printf("图书《%s》未被借出，无需归还！\n", book->bookName);
        return;
    }
    
    int oldBorrower = book->borrowerID;
    book->borrowerID = 0;
    book->status = 0;
    printf("图书《%s》（学号 %d 借阅）已成功归还。\n", book->bookName, oldBorrower);
}

// 释放链表内存
void FreeBookList(BookNode *head) {
    BookNode *current = head;
    BookNode *temp = NULL;
    int count = 0;
    
    while (current != NULL) {
        temp = current;
        current = current->next;
        free(temp);
        count++;
    }
    
    printf("成功释放 %d 本图书的内存\n", count);
}
        