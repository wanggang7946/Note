
```java
package queuelist;

import java.util.Scanner;

class DATA4 {
	String name;
	int age;
}

class SQType implements Queue{
	static final int QUEUELEN = 15; 			// 队列大小
	DATA4[] data = new DATA4[QUEUELEN]; 			// 队列数组
	int head; 						// 队头
	int tail; 						// 队尾
	
	//队列初始化
	SQType SQTypeInit() {
		SQType q;
	
		if ((q = new SQType()) != null) { 				// 创建对象，申请内存，申请成功就返回该对象
			q.head = 0; 			// 设置队头
			q.tail = 0; 			// 设置队尾
			return q;
		} else {
			return null; 				// 返回空
		}
	}
	//释放队列
	void SQTypeFree(SQType q){
		if(q!=null){
			q=null;						//在java的回收机制中，把队列对象至null，回收机制会把他至于弱引用状态，当系统垃圾回收机制运行就会回收他
		}
	}
	// 判断空队列
	@Override
	public boolean isEmpty() {
		
		return (head == tail);// 如果队头标志跟队尾标志相等就为空
	}
	
	// 判断满队列
	int SQTypeIsFull(SQType q) {
		int temp = 0;
		if (q.tail == QUEUELEN) { 						// 如果队列中没有多余的控件保存额外数据，就不可进行入队列操作
			temp = 1;
		}
		return temp;
	}
	
	// 入队列
	@Override
	public void append(Object data4) {
		if (tail == QUEUELEN) {
			System.out.print("队列已满！操作失败！\n"); 			// 如果队尾标志等于队列分配的大小
		} else {
			data[tail++] = (DATA4) data4; 				// 如果队列没满，则插入到队尾中（队尾tail标记最后队列当前最后一个元素）。
		}
	
	}
	//出队列操作
	@Override
	public Object delete(){
		if(head==tail){
			System.out.print("\n队列已空！操作失败！\n");			//先判断队头和队尾，如果相等则表示空队列
			System.exit(0);
			
		}else{												//如果不相同，那就把数据在队头那里移出。在返回数据时，把队头那边返回的数据减一位
			return data[head++];
		}
		return null;
		
	}
	//读取结点数据，然而只可以读取队头的数据
	@Override
	public Object getHead(){
		if(isEmpty()==true){
			System.out.print("\n空队列!\n");
			return null;
		}else{
			return data[head];
		}
		
	}
	//计算队列长度
	int SQType(SQType q){
		int temp;
		temp=q.tail-q.head;
		return (temp);
	}
}

public class QueueList {
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		SQType st = new SQType();
		DATA4 data1;
	
		Scanner input = new Scanner(System.in);
		SQType queue = st.SQTypeInit();					 // 初始化队列
		System.out.print("入队列操作：\n");
		while (true) {
			System.out.print("输入名字  年龄进行入队列操作：");
			DATA4 data = new DATA4();
			data.name = input.next(); 	
			data.age=input.nextInt();			// 输入年龄
			if (data.name.equals("0")) {
				break; 									// 如果输入年龄等于0，就退出
			} else {
				st.append(data); 					// 如果不等于0就插入队列
			}
			if(queue.isEmpty()!=true){				//打印队头数据
				System.out.printf("队头数据是:(%s,%d)\n",queue.getHead(),queue.getHead());
			}
	
		}
		System.out.println("下面进行出队列操作");
		String temp="1";
		System.out.println("出队列操作：按任意非0键进行出栈操作");
		temp=input.next();							
		while(!temp.equals("0")){
			data1=(DATA4) st.delete();						//出栈操作，每次出栈出一个
			System.out.printf("出队列的数据是(%s,%d)\n",data1.name,data1.age);
			temp=input.next();								//出栈操作执行的决定因素
			if(queue.isEmpty()!=true){				//打印队头数据
				System.out.printf("出栈后队头数据是:(%s,%d)\n",queue.getHead(),queue.getHead());
			}
		}
		System.out.print("测试结束！队列全空。\n");
		st.SQTypeFree(queue);								//释放队列所占用的空间
	}
}
```