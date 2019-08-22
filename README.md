#include<stdio.h>
#include<stdlib.h>
#include<string.h>

struct book
{
    char code[20];
    char name[20];
    char date[20];
    int cost;

}b;
int seat = 50;

void insert_details();
void viewAll();
void find();
void book_ticket();
void old_record();

void main()
{
    int ch;
    do{
        printf("\n                                              °°°°°°°°°°°°°°°°°°°°°°°°°");
        printf("\n");
        printf("\t                                         Movie ticket booking ");

        printf("\n                                              °°°°°°°°°°°°°°°°°°°°°°°°°\n\n");
        printf("\n                            Press <1> Insert movie");
        printf("\n                            Press <2> View all movie");
        printf("\n                            Press <3> Search movie");
        printf("\n                            Press <4> Book ticket");
        printf("\n                            Press <5> View all transactions");
        printf("\n                            Press <0> Exit\n");
        printf("\n                            Enter your choice ::");
        scanf("%d",&ch);
        switch(ch)
        {
        case 1 :
            insert_details();
            break;
        case 2:
            system("cls");
            viewAll();
            break;
        case 3:
            find();
            break;
        case 4:
            book_ticket();
            break;
        case 5:
            old_record();
            break;

        case 0:
            exit(0);
            break;
        default:
            printf("Wrong choice!");
            break;
        }
    }while(ch!=0);
}
void insert_details()
{
    FILE *fp;
    struct book b;
    printf("Enter movie code:");
    scanf("%s",b.code);
    printf("Enter name:");
    scanf("%s",b.name);
    printf("Enter release date:");
    scanf("%s",b.date);
    printf("Enter ticket price:");
    scanf("%d",&b.cost);
    fp=fopen("data.txt","a");

    if(fp==NULL)
    {
        printf("File not found");
    }
    else
    {
        fprintf(fp,"%s %s %s %d \n",b.code,b.name,b.date,b.cost);
        printf("Record insert successfully");


    }
    printf("\n");
    fclose(fp);
}

void find()
{
    struct book b;
    FILE *fp;



    char ch[20];
    printf("Enter movie code:");
    scanf("%s",ch);
    fp=fopen("data.txt","r");
    if(fp==NULL)
    {
        printf("file does not found !");
        exit(1);
    }
    else
    {
        while(getc(fp)!=EOF)
        {
            fscanf(fp,"%s %s %s %d",b.code,b.name,b.date,&b.cost);
            if(strcmp(b.code,ch)==0)
            {
                printf("\nRecord found\n");
                printf("\n\t\tcode ::%s",b.code);
                printf("\n\t\tmovie name ::%s",b.name);
                printf("\n\t\tmovie date ::%s",b.date);
                printf("\n\t\tprice of ticket ::%d",b.cost);
                break;
            }
        }
    }
    fclose(fp);
}
void viewAll()
{
    char ch;
    FILE *fp;
    fp=fopen("data.txt","r");
    if(fp==NULL)
    {
        printf("file does not found !");
        exit(1);
    }
    else
    {
        system("cls");
        while( (ch=fgetc(fp))!=EOF)
            printf("%c",ch);
    }
    fclose(fp);

}
void book_ticket()
{
    struct book b;
    FILE *fp;
    FILE *ufp;
    int total_seat,mobile,total_amount,change,cP;
    char name[20];
    char ch;
    char movie_code[20];
    fp=fopen("data.txt","r");
    if(fp==NULL)
    {
        printf("file does not found !");
        exit(1);

    }
    else
    {
        system("cls");
        while((ch=fgetc(fp))!=EOF)
           printf("%c",ch);

    }
    fclose(fp);
    printf("\n For Book Ticket choice movie(enter movie code of first letter)");
    printf("\n Enter movie code");
    scanf("%s",movie_code);
    fp=fopen("data.txt","r");
    if(fp == NULL)
    {
        printf("file does not found!");
        exit(1);

    }
    else
    {
        while(getc(fp)!= EOF)
        {
            fscanf(fp,"%s %s %s %d",b.code,b.name,b.date,&b.cost);
            if(strcmp(b.code,movie_code)==0)
            {
                printf("\n Record found\n");
                printf("\n\t\tcode::%s",b.code);
                printf("\n\t\tmovie name::%s",b.name);
                printf("\n\t\tmovie date::%s",b.date);
                printf("\n\t\tprice of ticket::%d",b.cost);


            }
        }
    }
    printf("\n*** Fill details ***");
printf("\n your name :");
scanf("%s",name);
printf("\n mobile number :");
scanf("%d",&mobile);
printf("\nTotal number of tickets:");
scanf("%d",&total_seat);
total_amount=b.cost*total_seat;

 printf("\n***** Enjoy Movie ****\n");

                printf("\n\t\tname::%s",name);
                printf("\n\t\tmobile number ::%d",mobile);
                printf("\n\t\tmovie name::%s",b.name);
                printf("\n\t\tTotal seats :: %d",total_seat);
                printf("\n\t\tcost per ticket ::%d",b.cost);
                printf("\n\t\tTotal amount ::%d",total_amount);

                ufp=fopen("oldTransection.txt","a");
                if(ufp==NULL)
                {
                    printf("File not found");

                }
                else
                {
                    fprintf(ufp,"%s %d %d %d %s %d \n", name,mobile,total_seat,total_amount,b.name,b.cost);
                    printf("\n Record insertion sucessfull to the old record");

                }
                printf("\n");
                fclose(ufp);
                fclose(fp);
}
void old_record()
{
    char ch;
    FILE *fp;

    fp=fopen("oldTransection.txt","r");
    if(fp=NULL)
    {
        printf("file does not found!");
        exit(1);
    }
    else
    {
        system("cls");
        while((ch=fgetc(fp)) !=EOF )
            printf("%c",ch);

    }
    fclose(fp);
}
