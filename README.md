- 👋 Hi, I’m @154659
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
154659/154659 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
 21:11:58
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
struct Student
{
	char stdName[100];
	int stdAge;
	int stdId;
	struct Student* next;
};
struct Student* headP = NULL;
struct Student* tailP = NULL;

void addstudent()
{
	struct Student* node = (struct Student*)malloc(sizeof(struct Student));
	int i = 0;
	if (node == NULL) 
	{
		exit(-1);
	}//判断malloc申请空间是否成功，消除警告


	printf("请输入学生的年龄：");
	scanf_s("%d", &node->stdAge);
	printf("请输入学生的学号：");
	scanf_s("%d", &node->stdId);
	printf("请输入学生名字：");
	scanf_s("%s", node->stdName, 100);//100是取消NULL对指针的引用，消除警告
	node->next = NULL;
	if (headP == NULL)
	{
		headP = node;
		tailP = node;
	}
	else
	{
		tailP->next = node;
		tailP = node;
	}
	printf("添加成功\n");
}

void findstuddent()
{
	printf("请输入你要查找学生的学号：");
	int id;
	scanf_s("%d", &id);
	struct Student* Id = headP;
	int flag = 0;
	while (Id != NULL)
	{
		if (Id->stdId == id)
		{
			printf("姓名：%s  年龄: %d 学号：%d\n", Id->stdName, Id->stdAge, Id->stdId);
			flag = 1;
			break;
		}
		else
		{
			Id = Id->next;
		}
		if (flag == 0)
			printf("抱歉没找到该学生的信息\n");
	}
}
void delstudent()
{
	printf("请输入你要删除的学生信息的学号:");
	int id;
	scanf_s("%d", &id);
	struct Student* Id = headP;
	if (Id->stdId == id)//目标id是头节点时
	{
		headP = headP->next;
		free(Id);//释放空间
		Id = NULL;
		printf("已成功删除！！！\n");
		return 0;
	}
	struct Student* anterId = Id;
	Id = Id->next;
	while (Id != NULL)//目标id不是头节点时
	{
		if (Id->stdId == id)
		{
			struct Student* next = Id->next;
			anterId->next = next;
			free(Id);
			Id = NULL;
			printf("已成功删除！！！\n");
			return;
		}
		else
		{
			anterId = Id;
			Id = Id->next;
		}
	}
	printf("该学生不存在，无法删除!");
}
void printstudent(struct Student* curp)
{
	if (curp == NULL)
	{
		printf("亲，当前还没有学生哦！");
	}
	else
	{
		while (curp != NULL)
		{
			printf("姓名：%s  年龄: %d 学号：%d\n", curp->stdName, curp->stdAge, curp->stdId);
			curp = curp->next;
		}
	}

}


main()
{
	struct Student* curp = headP;
	printf("------------欢迎使用简易学生系统------------\n");
	printf("------------输入1添加学生信息---------------\n");
	printf("------------输入2查找学生信息---------------\n");
	printf("------------输入3删除学生信息---------------\n");
	printf("------------输入4打印全部学生信息-----------\n");
	printf("------------输入5退出系统-------------------\n");

	if (1)
	{
		char dir = 0;
		dir = getchar();
		switch (dir)
		{
		case '1': addstdent(); break;
		case '2': findstdent(); break;
		case '3': delstdent(); break;
		case '4': printstudent(headP); break;
		case '5':exit(0); break;
		default:break;
		}

	}
	return 0;
}

 21:12:31




