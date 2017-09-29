#include "iostream"
#include "string"
#include "stdio.h"

using namespace std;

FILE *file;
int chars=0,words=0,lines=1,symbols=0,s[500];
char c;
//定义全局变量

void index()
{
    cout<<"                ********************主菜单*********************"<<endl;
    cout<<"                *                                          *"<<endl;
    cout<<"                *         1、显示字符数、单词数和行数      *"<<endl;
    cout<<"                *                                          *"<<endl;
    cout<<"                *         2、显示符号数                    *"<<endl;
    cout<<"                *                                          *"<<endl;
    cout<<"                *         3、显示行数及行分类              *"<<endl;
    cout<<"                *                                          *"<<endl;
    cout<<"                *         4、显示所有                      *"<<endl;
    cout<<"                *                                          *"<<endl;
    cout<<"                *         5、退出                           *"<<endl;
    cout<<"                *                                          *"<<endl;
    cout<<"                ***********************************************"<<endl;
    cout<<"                * 请选择需要的功能：";
}//主菜单函数

void analyse()
{
    while((c=fgetc(file))!=EOF) 
    {
        chars++;
        if (((c<='z')&&(c>='a'))||((c<='Z')&&(c>='A'))||((c>='0')&&(c<='9')))
        {
            words++;
            while((c=fgetc(file))!=EOF)
            {    
                chars++;
                if (((c<='z')&&(c>='a'))||((c<='Z')&&(c>='A'))||((c>='0')&&(c<='9')))
                {
                }
                else if (c=='\n')
                {
                    s[lines]=1;
                    lines++;
                    break;
                }
                else if (c==' ')
                    break;
                else
                {
                    symbols++;
                    break;
                }
            }
        }
        else if (c=='/')
        {
            if ((c=fgetc(file))=='/')
            {
                symbols+=2;
                s[lines]=2;
                fseek(file,-1L,SEEK_CUR);
            }
        }
        else if (c=='\n')
        {
            if (s[lines]!=2)
                s[lines]=1;
            lines++;    
        }
        else if (c==' ')
        {
        }
        else
            symbols++;
    }
    if (s[lines]!=2)
        s[lines]=1;
}//分析所有字符数、单词数、行数及行类的函数

int main ()
{
    char name[30],b;
    int a,i,j;
    cout<<"                * 请输入源文件名:";
    for(;;)
    {
        cin>>name;
        if((file=fopen(name,"r"))!=NULL) 
            break;
        else 
            cout<<"                * 文件路径错误！请重新输入源文件名:";
    }
    analyse();
    fclose(file);
    index();
    cin>>a;
    while (a!=5)
    {
        switch (a)
        {
            case 1:cout<<"                * 字符数："<<chars<<endl;
                   cout<<"                * 单词数："<<words<<endl;
                   cout<<"                * 行数  ："<<lines<<endl;
                   cout<<"                * 按任意键返回：";
                   b=getchar();
                   b=getchar();
                   break;
            case 2:cout<<"                * 符号数："<<symbols<<endl;
                   cout<<"                * 按任意键返回：";
                   b=getchar();
                   b=getchar();
                   break;
            case 3:cout<<"                * 行数："<<lines<<endl;
                   for (i=1;i<=lines;i++)
                   {
                       if (s[i]==1)
                       {
                           if (i<10)
                               cout<<"                * 第"<<i<<"行为   代码行"<<endl;
                           else if (i<100)
                               cout<<"                * 第"<<i<<"行为  代码行"<<endl;
                           else
                               cout<<"                * 第"<<i<<"行为 代码行"<<endl;
                       }
                       else if (s[i]==2)
                       {
                           if (i<10) 
                               cout<<"                * 第"<<i<<"行为   注释行"<<endl;
                           else if (i<100)
                               cout<<"                * 第"<<i<<"行为  注释行"<<endl;
                           else
                               cout<<"                * 第"<<i<<"行为 注释行"<<endl;
                       }
                   }
                   cout<<"                * 按任意键返回：";
                   b=getchar();
                   b=getchar();
                   break;
            case 4:cout<<"                * 字符数："<<chars<<endl;
                   cout<<"                * 单词数："<<words<<endl;
                   cout<<"                * 符号数："<<symbols<<endl;
                   cout<<"                * 行数  ："<<lines<<endl;
                   for (j=1;j<=lines;j++)
                   {
                       if (s[j]==1)
                       {
                           if (j<10)
                               cout<<"                * 第"<<j<<"行为   代码行"<<endl;
                           else if (j<100)
                               cout<<"                * 第"<<j<<"行为  代码行"<<endl;
                           else
                               cout<<"                * 第"<<j<<"行为 代码行"<<endl;
                       }
                       else if (s[j]==2)
                       {
                           if (j<10)
                               cout<<"                * 第"<<j<<"行为   注释行"<<endl;
                           else if (j<100)
                               cout<<"                * 第"<<j<<"行为  注释行"<<endl;
                           else
                               cout<<"                * 第"<<j<<"行为 注释行"<<endl;
                       }
                   }
                   cout<<"                * 按任意键返回：";
                   b=getchar();
                   b=getchar();
                   break;
        }
        system("cls");
