# 结构体

C 语言提供结构体来管理不同类型的数据组合



### 1.结构体的定义，引用，初始化

```c
struct student{
    int num;
    char name[20];
    char sex;
    int age;
};
//结构体类型声明，注意最后一定要加分号

int main()
{
    struct student s = {1001,"lele",'m',20};
    printf("%d%s%c%d\n",s.num,s.name,s.sex,s.age);
    //结构体数组的建立
    //数组的每一个位置存放一个结构体
    struct student sarr[3];
    int i;
    for (i=0;i<3;i++)
    {
        scanf("%d%s %c%d",&sarr[i].num,&sarr[i].num,&sarr[i].name,&sarr[i].sex,&sarr[i].age)            
    }    
    return 0;
}
```



### 2. 结构体对齐

**结构体的大小必须是其最大成员的整数倍**

```c
#include <stdio.h>
struct student_type1{
    double score; // double 8字节
    short age;
}

struct student_type2{ 
    double score;
	int height;
	short age; 
};

struct student_type3{ 
    int height;
	char sex;
	short age;
};

int main(){
    struct student_type1 s1;
	struct student_type2 s2;
	struct student_type3 s3; 
	printf("s1 size=%d\n",sizeof(s1)); 
	printf("s2 size=%d\n",sizeof(s2));
	printf("s3 size=%d\n",sizeof(s3)); 
	return 0;
}
```

```
s1 size=16
s2 size=16
s3 size=8

Process finished with exit code 0
```



### 3. 结构体指针

一个结构体变量的指针就是该变量所占据的内存段的起始地址。

可以设置一个指针变量， 用它指向一个结构体变量，**此时该指针变量的值是结构体变量的起始地址**。

指针变量也可以用来 指向结构体数组中的元素，从而能够通过结构体指针快速访问结构体内的每个成员。

```c
struct student{
    int num;
    char name[20];
    char sex;
};

int main()
{
    struct student s = {1001,"lele",'m'};
    struct student *p;
    p = &s;
    printf("%d%s%c\n",(*p).num,(*p).name,(*p).sex);
    //在c语言的优先级规则中，.（成员运算符的优先级高于取值运算符），
    //需要加括号改变优先级
    
    //结构体指针访问每一个成员
    printf("%d%s%c\n",p->num,p->name,p->sex);
    return 0;
}
```

结构体指针的成员选择

```c
printf("%d%s%c\n",p->num,p->name,p->sex);
```



### 4. typedef

typedef的作用是起别名

```c
#include <stdio.h>

typedef struct student{
    int num;
    char name[20];
    char sex;
}stu,*pstu;
//结构体和结构体指针

typedef int INTERGER;

int main()
{
    stu s = {1001,"lele",'m'};
    pstu p;
    
}
```

```c
#include <stdio.h>

typedef struct student{
    int num;
    char name[20];
    char sex;
}stu,*pstu;

int main() {
    stu s = {1,"wupeiqi",'1'};
    stu *p = &s;
    pstu pointer = &s;
    printf("stu->num=%d\n",p->num);
    printf("pointer->num=%d\n",pointer->num);
    return 0;
}
```

```
stu->num=1
pointer->num=1

Process finished with exit code 0
```



### 5. C++ 引用

```cpp
#include <stdio.h>

//把&写到形参的位置是C++的语法，称为引用
void modifynum(int &b) //传入的是引用
{
    b = b + 1;
}

int main()
{
    int a = 10;
    modifynum(a);
    return 0;
}
```

