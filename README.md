#include<stdio.h>

#include<conio.h>

#include<string.h>

#include<stdlib.h>

#define rw 80

#define cl 50

FILE*fp,*fp1,*f1,*f2;

int s,z;

char fn1[]="opd12.patient";

char fn2[]="oopd12.patient";

struct hospital{

        char name[20],address[20],ch;

        int age,roomno,sn;

        char disease[30],department[20],date[15];

        char recommendation[50],category[30];

        char test[15][20];

        float testfee[15];

        float totalfee;

        float balance;

        }p,q;

char string[20];

typedef struct hospital alka;

void newrecord(int l)

void print()

void displaytest()

void mainscreen()

void newrecord1()

void displaydepartment()

void edit1()

void editrecord()

void switch1()

void main()

{

    int a,i,n,y;

    char

    clrscr();

    mainscreen();

    label3:

    textcolor(3);

    gotoxy(23,15);

    cprintf("Enter today's Date(yyyy/mm/dd)");

    fflush(stdin);gotoxy(28,19);

    scanf("%[^\n]",date2);

    if((date2[4]!='/')||(date2[7]!='/')||(date2[5]>'3')||(date2[8]>'3'))

    {

        clrscr();

        mainscreen();

        gotoxy(23,13);textcolor(4+128);

        cprintf("Wrong Entry");

        goto label3;

    }

    clrscr();

    mainscreen();

    label1:

    textcolor(15);

    lowvideo();gotoxy(22,15);textcolor(14);

    cprintf("Enter the corresponding no");gotoxy(22,19);textcolor(10);

    cprintf("1.Add new patient record");gotoxy(22,21);

    cprintf("2.Search  or edit record");gotoxy(22,23);

    cprintf("3.Know the records of patients");gotoxy(22,25);

    cprintf("4.Delete the records");gotoxy(22,27);

    cprintf("5.Exit from the program");gotoxy(25,30);

    fflush(stdin);

    scanf("%c",&d);

    switch(d)

    {

        case '1':

              {

            {

                if((fp=fopen(fn1,"rb"))==NULL)

                s=1;

                else

                {

                while(fread(&p,sizeof(alka),1,fp))

                s=1+p.sn;

                }

                fclose(fp);

            }

            clrscr();

            mainscreen();

            label:

            gotoxy(22,19);textcolor(7);

            cprintf("Enter `o' for O.P.D. & `e'for Emergency");

            gotoxy(35,21);

            fflush(stdin);

            scanf("%c",&c);

            if(c=='o')

            {

                clrscr();

                mainscreen();

                textcolor(11);gotoxy(23,11);

                cprintf("ADDING NEW O.P.D.PATIENT RECORD");textcolor(15);

                gotoxy(21,12);

                cprintf("~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~");

                newrecord(s);

                newrecord1();

                if((fp=fopen(fn1,"ab+"))==NULL)

                {

                    printf("Cannot open the file f1");

                    getch();

                    exit(1);

                }

                for(a=0;a<15;a++)

                p.testfee[a]=0;

                strcpy(&p.test[1][0],"0");

                p.totalfee=0;p.balance=0;

                strcpy(&p.test[0][0],"O.P.D. charge");

                p.testfee[0]=200;

                p.totalfee=200;

                strcpy(p.category,"O.P.D.Patient");

                p.balance=200;

                strcpy(p.recommendation,"Admitted to O.P.D.");

                strcpy(p.date,date2);

                fwrite(&p,sizeof(p),1,fp);

                fclose(fp);

                if((fp=fopen(fn2,"ab+"))==NULL)

                {

                        printf("Cannot open the file f1");

                        getch();

                        exit(1);

                }

                fwrite(&p,sizeof(p),1,fp);

                fclose(fp);

            }

            else if(c=='e')

                   {

                 clrscr();

                 mainscreen();

                 textcolor(11);

                 gotoxy(23,11);

                 cprintf("ADDING NEW EMERGENCY PATIENT RECORD");

                 textcolor(15);

                 gotoxy(23,12);

                 cprintf("~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~");

                 newrecord(s);

                 newrecord1();

                 if((fp=fopen(fn1,"ab+"))==NULL)

                    {

                        printf("Cannot open the file f1");

                        getch();

                        exit(1);

                    }

                    for(a=0;a<15;a++)

                    p.testfee[a]=0;

                    strcpy(&p.test[1][0],"0");

                    p.totalfee=0;p.balance=0;

                   p.totalfee=250;

                   strcpy(p.date,date2);

                   strcpy(&p.test[0][0],"Emergency Charge");

                   strcpy(p.category,"Emergency Patient");

                   strcpy(p.recommendation,"Admitted to Emergency");

                   p.testfee[0]=250;

                   p.balance=250;

                   fwrite(&p,sizeof(p),1,fp);

                   fclose(fp);

                  if((fp=fopen(fn2,"ab+"))==NULL)

                {

                        printf("Cannot open the file f1");

                        getch();

                        exit(1);

                }

                fwrite(&p,sizeof(p),1,fp);

                fclose(fp);

                   }

            else

            {

                clrscr();

                mainscreen();

                gotoxy(22,15);textcolor(128+5);

                cprintf("Wrong choice");

                textcolor(15);

                goto label;

            }

            break;

              }

        case '2':

              {

               clrscr();

               mainscreen();

               editrecord();

               break;

              }

        case '5':

              {

            clrscr();

            mainscreen();

            textcolor(14); gotoxy(30,24);

            cprintf("THANK U");gotoxy(30,26);

               //    cprintf("SAVING UR SETTINGS"); gotoxy(30,28);

            cprintf("BYE...........");

            getch();

            exit(1);

            break;

            }

        case '4':

            {

                if((fp=fopen(fn1,"rb"))==NULL)

                {

                    printf("cannot open the file");

                    getch();

                    exit(1);

                }

                if((f1=fopen("delete","wb"))==NULL)

                {

                    printf("cannot open the file");

                    getch();

                    exit(1);

                }

                clrscr();

                mainscreen();

                gotoxy(30,25);

                cprintf("Enter the patient no");

                gotoxy(40,27);

                   fflush(stdin);

                scanf("%d",&y);

                while(fread(&p,sizeof(alka),1,fp))

                    if(p.sn!=y)

                    fwrite(&p,sizeof(alka),1,f1);

                clrscr();

                mainscreen();

                fseek(fp,(y-1)*sizeof(alka),SEEK_SET);

                fread(&p,sizeof(alka),1,fp);

                print();

                edit1();

                gotoxy(25,46);

                cprintf("Press `ENTER' to delete this record");

                getch();

                fclose(fp);

                fclose(f1);

                remove(fn1);

                rename("delete",fn1);

                if((fp=fopen(fn2,"rb"))==NULL)

                {

                    printf("cannot open the file");

                    getch();

                    exit(1);

                }

                if((f1=fopen("delete","wb"))==NULL)

                {

                    printf("cannot open the file");

                    getch();

                    exit(1);

                }

                while(fread(&p,sizeof(alka),1,fp))

                    if(p.sn!=y)

                    fwrite(&p,sizeof(alka),1,f1);

                fclose(fp);

                fclose(f1);

                remove(fn2);

                rename("delete",fn2);

                clrscr();

                mainscreen();

                gotoxy(25,25);textcolor(3);

                cprintf("Record succesfully Deleted");

                getch();

                gotoxy(37,30);

                break;

            }

        case '3':

            {       label6:

                clrscr();

                mainscreen();

                gotoxy(22,15);textcolor(12);

                cprintf("Enter the corresponding no");gotoxy(22,19);textcolor(3);

                cprintf("1.Records of patients in alphabatecal order");gotoxy(22,21);

                cprintf("2.Records of Emergency patients");gotoxy(22,23);

                cprintf("3.Records of O.P.D. patients");gotoxy(22,25);

                cprintf("4.Recordsin paricular date");gotoxy(22,27);

                cprintf("5.Return to main menu");gotoxy(25,30);

                fflush(stdin);

                scanf("%c",&d);

                switch(d)

                {

                case '1':

                    {

                     if((fp=fopen(fn2,"rb+"))==NULL)

                          {

                        printf("Cannot open the file");

                        getch();

                        exit(1);

                          }

                     fseek(fp,0,SEEK_END);

                     tsz=ftell(fp);

                     n=(int)(tsz/sizeof(alka));

                     for(i=0;i<(n-1);i++)

                     {

                        for(a=i+1;a<n;a++)

                        {

                        fseek(fp,i*sizeof(alka),SEEK_SET);

                        fread(&p,sizeof(alka),1,fp);

                        fseek(fp,a*sizeof(alka),SEEK_SET);

                        fread(&q,sizeof(alka),1,fp);

                        if(strcmp(p.name,q.name)>0)

                            {

                            fseek(fp,i*sizeof(alka),SEEK_SET);

                            fwrite(&q,sizeof(alka),1,fp);

                            fseek(fp,a*sizeof(alka),SEEK_SET); fflush(stdin);

                            fwrite(&p,sizeof(alka),1,fp);

                            }

                        }

                    }

                    rewind(fp);

                    clrscr();

                    mainscreen();

                    gotoxy(3,20);

                    textcolor(11);

                    cprintf("Ready to Display the patient records according to alphabatecal order of names");

                    gotoxy(27,25);textcolor(3);

                    cprintf("Press");textcolor(15+128);

                    cprintf(" `Enter' ");    textcolor(3);

                    cprintf("to continue");

                    getch();

                    while(fread(&p,sizeof(alka),1,fp))

                    {

                    clrscr();

                    mainscreen();

                    print();

                    gotoxy(17,10);  textcolor(7);

                    cprintf("DISPLAYING-RECORD-ACCORDING-TO-PATIENTS-NAMES");

                    gotoxy(16,11);textcolor(15);

                    cprintf("---------------------------------------------");

                    edit1();

                    textcolor(11);

                    gotoxy(20,46);

                    cprintf("Press");textcolor(15+128);

                    cprintf(" `Enter'"); textcolor(11);

                    cprintf(" for next and `r' to quit: ");

                    scanf("%c",&c);

                    if(c=='r')

                    {

                    goto label6;

                    }

                    gotoxy(60,46);

                    getch();

                }

                clrscr();

                mainscreen();

                textcolor(11);

                gotoxy(30,25);

                cprintf("::No Further Records::");   gotoxy(40,30);

                getch();

                fclose(fp);

                break;

                }

            case '5':

                {

                clrscr();

                mainscreen();

                 goto label1;

                 }

            case '2':

                {

                clrscr();

                mainscreen();

                if((fp=fopen(fn1,"rb"))==NULL)

                          {

                        printf("Cannot open the file");

                        getch();

                        exit(1);

                          }

                gotoxy(15,20);

                textcolor(2);

                cprintf("Ready to Display records of Emergency Patients");

                gotoxy(27,25);textcolor(3);

                cprintf("Press");textcolor(15+128);

                cprintf(" `Enter' ");    textcolor(3);

                cprintf("to continue");

                getch();

                while(fread(&p,sizeof(alka),1,fp))

                {

                    if(strcmp(p.category,"Emergency Patient")==NULL)

                    {

                    clrscr();

                    mainscreen();

                    print();

                    gotoxy(17,10);  textcolor(7);

                    cprintf("::DISPLAYING-RECORDS-OF-EMERGENCY-PATIENTS::");

                    gotoxy(16,11);textcolor(15);

                    cprintf("---------------------------------------------");

                    edit1();

                    textcolor(11);

                    gotoxy(20,45);

                    cprintf("Press");textcolor(15+128);

                    cprintf(" `Enter'"); textcolor(11);

                    cprintf(" for next and `r' to quit: ");

                    scanf("%c",&c);

                    if(c=='r')

                    {

                    goto label6;

                    }

                    gotoxy(60,46);

                    getch();

                    }

                }

                clrscr();

                mainscreen();

                textcolor(11);

                gotoxy(30,25);

                cprintf("::No Further Records::");   gotoxy(40,30);

                getch();

                fclose(fp);

                break;

                }

            case '3':

                {

                clrscr();

                mainscreen();

                if((fp=fopen(fn1,"rb"))==NULL)

                          {

                        printf("Cannot open the file");

                        getch();

                        exit(1);

                          }

                gotoxy(15,20);

                textcolor(2);

                cprintf("Ready to Display records of O.P.D Patients");

                gotoxy(27,25);textcolor(3);

                cprintf("Press");textcolor(15+128);

                cprintf(" `Enter' ");    textcolor(3);

                cprintf("to continue");

                getch();

                while(fread(&p,sizeof(alka),1,fp))

                {

                    if(strcmp(p.category,"O.P.D.Patient")==NULL)

                    {

                    clrscr();

                    mainscreen();

                    print();

                    gotoxy(17,10);  textcolor(7);

                    cprintf("::DISPLAYING-RECORDS-OF-OPD-PATIENTS::");

                    gotoxy(16,11);textcolor(15);

                    cprintf("---------------------------------------------");

                    edit1();

                        textcolor(11);

                    gotoxy(20,46);

                    cprintf("Press");textcolor(15+128);

                    cprintf(" `Enter'"); textcolor(11);

                    cprintf(" for next and `r' to quit: ");

                    scanf("%c",&c);

                    if(c=='r')

                    {

                    goto label6;

                    }

                    gotoxy(60,46);

                    getch();

                    }

                }

                clrscr();

                mainscreen();

                textcolor(11);

                gotoxy(30,25);

                cprintf("::No Further Records::");   gotoxy(40,30);

                getch();

                fclose(fp);

                break;

                }

        case '4':

                {

                clrscr();

                mainscreen();

                if((fp=fopen(fn1,"rb"))==NULL)

                          {

                        printf("Cannot open the file");

                        getch();

                        exit(1);

                          }

                label8:

                gotoxy(27,20);

                textcolor(3);

                cprintf("Enter the `Date' of a paricular day(yyyy/mm/dd)");

                gotoxy(35,25);fflush(stdin);

                scanf("%s",string);

                if((string[4]!='/')||(string[7]!='/')||(string[5]>'3')||(string[8]>'3'))

                {

                clrscr();

                mainscreen();

                gotoxy(23,13);textcolor(4+128);

                cprintf("Wrong Entry");

                goto label8;

                }

                   //    getch();

                while(fread(&p,sizeof(alka),1,fp))

                {

                    if(strcmp(string,p.date)==NULL)

                    {

                    clrscr();

                    mainscreen();

                    print();

                    gotoxy(17,10);  textcolor(7);

                    cprintf("::DISPLAYING-RECORDS-OF-");

                    cprintf("DATE >%s",p.date);

                    gotoxy(16,11);textcolor(15);

                    cprintf("---------------------------------------------");

                    edit1();

                    textcolor(11);

                    gotoxy(20,46);

                    cprintf("Press");textcolor(15+128);

                    cprintf(" `Enter'"); textcolor(11);

                    cprintf(" for next and `r' to quit: ");

                    scanf("%c",&c);

                    if(c=='r')

                    {

                    goto label6;

                    }

                    gotoxy(60,46);

                    getch();

                    }

                }

                clrscr();

                mainscreen();

                textcolor(11);

                gotoxy(30,25);

                cprintf("::No Further Records::");   gotoxy(40,30);

                getch();

                fclose(fp);

                break;

                }

            default:

                {

                clrscr();

                mainscreen();

                textcolor(12+128);gotoxy(22,11);

                cprintf("Wrong choice");gotoxy(22,13);textcolor(15);

                 cprintf("Retype choice");

                goto label6;

                }

            }

        }break;

        default:

               {

            clrscr();

            mainscreen();

            textcolor(12+128);gotoxy(22,11);

            cprintf("Wrong choice");gotoxy(22,13);textcolor(15);

             cprintf("Retype choice");

            goto label1;

            }

    }

    clrscr();

    mainscreen();

    goto label1;

}

void newrecord(int l)

{

    char q;

    p.sn=l;

    displaydepartment();

    gotoxy(5,14);textcolor(10);

    cprintf("Record of patient no:");

    printf(" %d",l);

    gotoxy(5,17);

    cprintf("Name:");

    gotoxy(5,20);

    cprintf("Address:");

    gotoxy(5,23);

    cprintf("Age: ");

    gotoxy(5,26);

    cprintf("Sex(m/f): ");

    gotoxy(5,29);

    cprintf("Disease Descrp:");

    gotoxy(9,30);

    cprintf("(In Short)");

    gotoxy(5,33);

    cprintf("Reff. Specialist no:");

    fflush(stdin);gotoxy(10,17);

    scanf("%[^\n]",p.name);

    p.name[0]=toupper(p.name[0]);

    gotoxy(14,20);

    fflush(stdin);

    scanf("%[^\n]",p.address);

    gotoxy(10,23);

    fflush(stdin);

    scanf("%d",&p.age);

    gotoxy(15,26);

    fflush(stdin);

    scanf("%c",&p.ch);

    fflush(stdin);gotoxy(22,29);

    scanf("%[^\n]",p.disease);

}

void newrecord1()

{

      char q;

     fflush(stdin);

     gotoxy(25,33);

    scanf("%c",&q);

    switch(q)

    {

        case '1':

            {          gotoxy(5,36);

                   cprintf("Reff.Specialist:");

                   printf("Generalphysician");

                   strcpy(p.department,"General Physician");

                   gotoxy(5,39);

                cprintf("Room no:");

                fflush(stdin);

                scanf("%d",&p.roomno);

                   //    getch();

                break;
                }

        
