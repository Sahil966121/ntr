CRC
##include<stdio.h>
#include<conio.h>
int dg=16,dm,dt,data[50],gen[17]={1,0,0,0,0,1,0,0,0,0,0,0,1,0,0,0,1};
int si[16],so[16],tx;
void main() {
void crc(int msg[]);
int i,j,k;
printf("\n Enter your choice (1/2)\n");
printf("1 for CRC-CCITT \n");
printf("2 for generalised generator polynomial\n");
printf("\n Choice:");
if(getchar()=='2') {
printf("\n Enter the degree of generator polynomial\n");
scanf("%d",&dg);
printf("\n Enter the generator polynomial\n");
for(i=dg;i>=0;i--) scanf("%d",&gen[i]);
}
printf("\n The generator polynomial is \n");
for(i=dg;i>=0;i--) printf("%d",gen[i]);
printf("\n Enter the degree of message\n");
scanf("%d",&dm);
printf("\n Enter the message\n");
for(i=dm;i>=0;i--) scanf("%d",&data[i]);
dt=dm+dg;
for(i=0;i<=dm;i++) data[dt-i]=data[dm-i];
for(i=1;i<=dg;i++) data[dg-i]=0;
tx=1;
crc(data);
printf("\n Enter the received message\n");
for(i=dt;i>=0;i--)scanf("%d",&data[i]);
tx=0;
crc(data);
}
void crc(int msg[]) {
int i,j,k,flag;
for(i=0;i<dg;i++) {
so[i]=0;
si[i]=0;

}
for(i=dt;i>=0;i--) {

if(gen[0]==1) si[0]=so[dg-1]^msg[i];
else si[0]=msg[i];
for(j=1;j<=dg-1;j++)
if(gen[j]==1) si[j]=so[dg-1]^so[j-1];
else si[j]=so[j-1];
printf("\n");
for(k=dg-1;k>=0;k--) {
so[k]=si[k];
printf("%d",so[k]);
}
}
if(tx) {
printf("\n CRC code is \n");
for(k=dg-1;k>=0;k--) {
printf("%d",so[k]);
msg[k]=so[k];
}
printf("\n Message to be transmitted\n");
for(i=dt;i>=0;i--)printf("%d",msg[i]);
}
if(!tx) {
flag=0;
for(i=0;i<=dg-1;i++)
if(so[i]==1) {
flag=1;
break;
}
if(flag==0) printf("\nResult: No error");
else printf("\n Result: Error in the received msg");
}
}


SHORTEST 4 NODE

#include<stdio.h>
#include<stdlib.h>
#define nodes 4
#define infinity 100
int n;
int dist[nodes][nodes]=
{0,100,10,2,
100,0,3,4,
10,3,0,100,
2,4,100,0};
void main(){
int i,s,j,t;
void shrt();
printf("\n Enter the no of nodes");
scanf("%d",&n);
printf("\n enter the source & dest nodes");
scanf("%d%d",&s,&t);
if(s==t){
printf("\n Source is same as the destination \t Hence the Distance is 0");
exit(0);
}
shrt(s,t);
}
void shrt(int s,int t){
struct state {
int predecessor;
int length;
enum{per,tent}label;
}state[nodes];
int i,k,min;
struct state *p;
for(p=&state[0];p<&state[n];p++){
p->predecessor=-1;
p->length=infinity;
p->label=tent;
}
state[t].length=0;state[t].label=per;
k=t;
do {
for(i=0;i<n;i++)
if(dist[k][i]!=0 && state[i].label==tent) {
if(state[k].length+dist[k][i]<state[i].length) {
state[i].predecessor=k;
state[i].length=state[k].length+dist[k][i];
}
}
k=0;
min=infinity;
for(i=0;i<n;i++)
if(state[i].label==tent && state[i].length<min) {

min=state[i].length;
k=i;
}
state[k].label=per;
}while(k!=s);
k=s;
do {
printf("%d",k);
if (k!=t) printf("--->");
k=state[k].predecessor;
}while(k>=0);
printf("\n The total distance is %d",state[s].length);
}



SHORTEST 8 NIODE
#include<stdio.h>
#include<stdlib.h>
#define nodes 8
#define infinity 100
int n;
int dist[nodes][nodes]=
{0,2,100,1,100,100,100,100,
2,0,2,100,9,100,100,100,
100,2,0,7,100,2,100,100,
1,100,7,0,100,100,7,100,
100,9,100,100,0,4,100,6,
100,100,2,100,4,0,2,100,
100,100,100,7,100,2,0,2,
100,100,100,100,6,100,2,0};

void main(){
int i,s,j,t;
void shrt();
printf("\n Enter the no of nodes");
scanf("%d",&n);
printf("\n enter the source & dest nodes");
scanf("%d%d",&s,&t);
if(s==t){
printf("\n Source is same as the destination \t
Hence the Distance is 0");
exit(0);
}
shrt(s,t);
}
void shrt(int s,int t){
struct state {
int predecessor;
int length;
enum{per,tent}label;
}state[nodes];
int i,k,min;
struct state *p;
for(p=&state[0];p<&state[n];p++){
p->predecessor=-1;
p->length=infinity;
p->label=tent;
}
state[t].length=0;state[t].label=per;
k=t;
do {
for(i=0;i<n;i++)
if(dist[k][i]!=0 && state[i].label==tent) {
if(state[k].length+dist[k][i]<state[i].length) {
state[i].predecessor=k;
state[i].length=state[k].length+dist[k][i];
}
}
k=0;
min=infinity;
for(i=0;i<n;i++)
if(state[i].label==tent && state[i].length<min) {
min=state[i].length;
k=i;
}
state[k].label=per;
}while(k!=s);
k=s;
do {
printf("%d",k);
if (k!=t) printf("--->");

k=state[k].predecessor;
}while(k>=0);
printf("\n The total distance is %d",state[s].length);
}





BIT STUFFING AND DESTUFFING
#include<stdio.h>
#include<string.h>
#include<stdlib.h>
int main()
{
int i,j=0,count=0,temp=0,beg_msg=0,end_msg=0;
char msg[100],smsg[100],bsmsg[100],rmsg[100],omsg[100];
printf("\n Enter the message:\n");
scanf("%s",msg);
for(i=0,j=0;msg[i]!='\0';i++,j++){
smsg[j]=msg[i];
if(msg[i]=='1') /* count the no of successive ones */
count++;
else
count=0;
if(count==5){ /* stuff a zero after 5 ones */
j++;
smsg[j]='0';
count=0;
}
}
smsg[j]='\0';
printf("\n The stuffed message :\n %s",smsg);
strcpy(bsmsg,"01111110"); /* add header bits */
strcat(bsmsg,smsg);
strcat(bsmsg,"01111110"); /* add the tailor bits*/
printf("\n The frame to be transmitted :\n %s",bsmsg);
/* destuffing */

printf("\n Enter the received message :\n");
scanf("%s",rmsg);
temp=0;
i=j=0;
for(i=0;rmsg[i+7]!='\0';i++){
if(rmsg[i]=='0' && rmsg[i+7]=='0'){ /* check for header & tailor*/
for(j=1;j<7;j++){

if(rmsg[i+j]=='1')
temp++;
else {

temp=0;
break;
}

}
if(temp==6){ /* if 01111110 bit stream found */
if(beg_msg==0) /* for the first time,msg begins */
beg_msg=i+8;
else{
end_msg=i; /* for the second time msg ends */
break;
}
}
}
else
temp=0;
}
if((beg_msg==0)||(end_msg==0)){
printf("\n framing error");
exit(0);
}
count=0;
for(i=beg_msg,j=0;i<end_msg;i++,j++){
omsg[j]=rmsg[i];
if(rmsg[i]=='1')
count++; /* check for consecutive ones */
else
count=0; /* if 0 is found after 5 ones */
if(count==5){
i++; /* ignore it */
count=0;
}
}
omsg[j]='\0';
printf("\n The original message :\n %s",omsg);
return 0;
}


CHARACTER STUD=FIFING 
#include<stdio.h>
#include<string.h>
#include<stdlib.h>
void main()
{
int i,j=0,hfound=0,tfound=0,error=0;
char msg[100],smsg[100],tmsg[100],rmsg[100],dmsg[100];
printf("\nEnter the message:\n");
scanf("%s",msg);
*(smsg)='\0';
*(dmsg)='\0';

for(i=0,j=0;msg[i]!='\0';i++,j++){
if(!strncmp(msg+i,"DLE",3))
{
smsg[j]='\0';
strcat(smsg,"DLEDLE");
i+=2;
j+=5;
}
else smsg[j]=msg[i];
}
smsg[j]='\0';
strcpy(tmsg,"DLESTX");
strcat(tmsg,smsg);
strcat(tmsg,"DLEETX");
printf("\nThe stuffed message is :\n%s",tmsg);
/* Destuffing */
printf("\nEnter the received message :\n");
scanf("%s",rmsg);
for(i=0,j=0;rmsg[i]!='\0';i++)
{
if(!strncmp(rmsg+i,"DLE",3))
{
i+=3;
if(!strncmp(rmsg+i,"STX",3))
{
if(!hfound) hfound=1;
else error=1;
i+=2;
continue;
}
else if(!strncmp(rmsg+i,"ETX",3))
{
tfound=1;
break;
}
else if(!strncmp(rmsg+i,"DLE",3));
else error=1;
}
if(hfound==1)
{
dmsg[j]=rmsg[i];
dmsg[j+1]='\0';
j++;
}
}
dmsg[j]='\0';
if(error||!hfound||!tfound)
{
printf("\nFraming Error\n ");
exit(0);
}
printf("\nThe destuffed message is :\n%s",dmsg);
}




ENCRYPTION TRANSPOSITION 
#include<stdio.h>
#include<string.h>
#include<conio.h>
#include<stdlib.h>
void main()
{
char txt[50],kw[10],kw1[10],temp,txt1[10][10],encr[10][10],decr[10][10];
int lenm,lenk,order[10],i,j,k,temp1,c=0,r,b,count;
printf("\nEnter the message to be enrypted: ");
scanf("%s",txt);
lenm=strlen(txt);
printf("\nEnter the keyword: ");
scanf("%s",kw);
lenk=strlen(kw);
strcpy(kw1,kw);
for(i=0;i<lenk;i++)
order[i]=i;

//sort the keyword

for(i=0;i<lenk;i++)
for(j=0;j<lenk;j++) {
if(kw1[j]>kw1[i]) {
temp=kw1[j];
kw1[j]=kw1[i];
kw1[i]=temp;
temp1=order[j];
order[j]=order[i];
order[i]=temp1;
}
}
printf("\n Order of letters after sorting: ");
for(i=0;i<lenk;i++)
printf("%d ",order[i]);
r=lenm/lenk; //no. of rows

b=lenm%lenk;
if(b!=0) r++;
//convert message to matrix
count=0;
for(i=0;i<r;i++) {
for(j=0;j<lenk && count<=lenm;j++)
txt1[i][j]=txt[count++];
if(count>lenm) {
while(b!=lenk) {
txt1[i][b]='a'+c++;
b++;
}
}
}

//encryption

printf("\nThe encrypted message :\n");
for(k=0;k<lenk;k++) {
for(i=0;i<r;i++) {
j=order[k];
encr[i][k]=txt1[i][j];
printf("%c",encr[i][k]);
}
}
//at the receiver
printf("\nEnter the keyword: ");
scanf("%s",kw1);
if(strcmp(kw,kw1)) {
printf("Wrong Key!!");
exit(0);
}

//decryption

for(i=0;i<lenk;i++) {
j=order[i];
for(k=0;k<r;k++)
decr[k][j]=encr[k][i];
}
printf("\n The original message is: ");
for(i=0;i<r;i++)
for(j=0;j<lenk;j++) {
if(((i*lenk)+j)==lenm){
break;
}
printf("%c",decr[i][j]);
}
}



EDNCRYPTION SUBSTIOYUION 
#include<stdio.h>
#include<string.h>
void main()
{
char msg[100],encr[100],decr[100],rec[100];

int i;
printf("\n Enter the message for encryption:\n ");
scanf("%s",msg);
for(i=0;*(msg+i)!='\0';i++) {
if((*(msg+i)>='a' && *(msg+i)<='w')||(*(msg+i)>='A' && *(msg+i)<='W'))
*(encr+i)=*(msg+i)+3;
else
if((*(msg+i)>='x' && *(msg+i)<='z')||(*(msg+i)>='X' && *(msg+i)<='Z'))
*(encr+i)=*(msg+i)+3-26;
else
*(encr+i)=*(msg+i)+3;
}
*(encr+i)='\0';
printf("\n Encrypted message: %s\n",encr);
/* Decryption */
printf("\n Enter the message for decryption:\n ");
scanf("%s",rec);
for(i=0;*(rec+i)!='\0';i++) {
if((*(rec+i)>='d' && *(rec+i)<='z')||(*(rec+i)>='D' && *(rec+i)<='Z'))
*(decr+i)=*(rec+i)-3;
else
if((*(rec+i)>='a' && *(rec+i)<='c')||(*(rec+i)>='A' && *(rec+i)<='C'))
*(decr+i)=*(rec+i)-3+26;
else
*(decr+i)=*(rec+i)-3;

}
*(decr+i)='\0';
printf("\n The decrypted message:\n %s",decr);
}










