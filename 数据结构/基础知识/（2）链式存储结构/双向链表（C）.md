#双向链表Demo
```c
#include<stdio.h>
#include<stdlib.h>

#define OK 1
#define ERROR 0
typedef  int Item;  
typedef int Status;
/*定义节点类型*/  
typedef struct Node  
{  
    Item data;      /*数据域*/  
    struct Node *previous; /*指向前驱*/  
    struct Node *next;     /*指向后继*/  
}Node,*pNODE;  
//创建双向链表：
pNODE createList(){
	 
	pNODE tail =NULL;
	pNODE head = (pNODE)malloc(sizeof(Node));
	if(NULL==head){
		 printf("内存分配失败！\n"); 
	}
	head->data=0;
	head->previous=NULL;
	head->next=NULL;
	tail=head;
	return head;
} 
//打印链表  
void TraverseDbLinkList(pNODE pHead)  
{  
    pNODE pt = pHead->next;  

    printf("打印链表如：");  
    while (pt != NULL)  
    {  
        printf("%d ", pt->data);  
        pt = pt->next;  
    }  
    putchar('\n');  
}  
//判断链表是否为空  
int IsEmptyDbLinkList(pNODE pHead)  
{  
    pNODE pt = pHead->next;  

    if (pt == NULL)  
        return 1;  
    else  
        return 0;  
}  
 //计算链表的长度  
int GetLengthDbLinkList(pNODE pHead)  
{  
    int length = 0;  
    pNODE pt = pHead->next;  
      
    while (pt != NULL)  
    {  
        length++;  
        pt = pt->next;  
    }  
    return length;  
}   
int insertNode(pNODE pHead,int position,int data){
	pNODE pt =NULL,p_new=NULL;
	p_new=(pNODE)malloc(sizeof(Node));
	if(p_new==NULL){
		 printf("内存分配失败！\n");  
	}
	int j=1;
	while(j<position){
		j++;
		pHead = pHead->next;
	}
	//先处理后序结点指针 
	pt = pHead->next;
	p_new->data=data;
	p_new->next=pt;
	//再处理前指针 
	if(pt!=NULL){
		pt->previous=p_new;
	}
	p_new->previous=pHead;
	pHead->next=p_new;
}
int deleteNode(pNODE pHead,int position){
	pNODE pt =NULL;
	int j=1;
	while(j<position){
		j++;
		pHead = pHead->next;
	}
	//同样，先处理 
	pt=pHead->next->next;
	pHead->next=pt;
	free(pHead->next);
	if(pt!=NULL){
		pt->previous=pHead;
	}
	return OK;
} 
//删除整个链表，释放内存  
void FreeMemory(pNODE *ppHead)  
{  
    pNODE pt = NULL;  

    while (*ppHead != NULL)  
    {  
        pt = (*ppHead)->next;  
        free(*ppHead);  
        if (NULL != pt)  
            pt->previous = NULL;  
        *ppHead = pt;  
    }  
}  
int main(void)  
{  
	int flag = 0,length=0;
	 int position = 0, value = 0; 
	pNODE head = NULL;  
	  
	head = createList();  
	flag = IsEmptyDbLinkList(head);  
	if (flag)  
	    printf("双向链表为空！\n");  
	else{
	 length = GetLengthDbLinkList(head);  
	    printf("双向链表的长度为：%d\n", length);  
	    TraverseDbLinkList(head);  
	}
	 printf("请输入要插入节点的位置和元素值(两个数用空格隔开)：");  
	 scanf("%d %d", &position, &value); 
	flag = insertNode(head, position, value);  
	TraverseDbLinkList(head); 
	if (flag)  
	{  
	    printf("插入节点成功！\n");  
	    TraverseDbLinkList(head);  
	}     
	else {
		printf("插入节点失败！\n");  
	} 
	 flag = IsEmptyDbLinkList(head);  
	if (flag)  
	    printf("双向链表为空，不能进行删除操作！\n");  
	else  
	{  
	    printf("请输入要删除节点的位置：");  
	    scanf("%d", &position);  
	    flag = deleteNode(head, position);  
	    if (flag)  
	    {  
	        printf("删除节点成功！\n");  
	        TraverseDbLinkList(head);  
	    }     
	    else  
	        printf("删除节点失败！\n");  
	}     
	
	return OK; 
} 
```