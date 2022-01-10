# -readyPcbtail=(PCB*)malloc(sizeof(PCB));

readyPcb=readyPcbtail;

readyPcbtail->id=0;

readyPcbtail->priority=0;

readyPcbtail->time=0;

readyPcbtail->next=NULL;

do

{/*创建程序控制界面*/

printf("******************************\n");

printf("\t1.创建一个PCB进程\n\t2.销毁运行PCB进程\n\t3.就绪队列打印输出\n\t4.退出系统\n");

printf("******************************\n");

scanf("%d",&on);//设置开关按钮

switch(on)

{

case 1: p=Create(nullPcb); InsertReadyPcb(readyPcb,p);break; //执行创建PCB进程

case 2: printf("请输入销毁的进程的id值");scanf("%d",&deleteId);Delete(deleteId,readyPcb,nullPcb);break;

case 3: PrintPCB(readyPcb);break;

case 4: exit(0);

default:

printf("请输入1-4之间的序号\n");

}

}while(on!=4);

}

void InitPcb(PCBList &nullPcb)//初始化空闲队列

{

nullPcb=&pcb[0];

for(int i=0;i<PCBSIZE-1;i++){

pcb[i].id=i;

pcb[i].next=&pcb[i+1];

}

pcb[PCBSIZE-1].next=NULL;

printf("进程块初始化成功\n");

}

PCBList Create(PCBList &nullPcb)//用于创建一个pcb进程

{

if(nullPcb){//将空闲队列的第一个赋值给就绪队列，并将它放置在就绪队列的队尾

pcbP=nullPcb;

nullPcb=nullPcb->next;

printf("请输入创建pcb的序号id\n");

scanf("%d",&pcbP->id);

printf("请输入创建它的名字\n");

scanf("%s",&pcbP->name);

printf("请输入它的优先级\n");

scanf("%d",&pcbP->priority);

printf("请输入它运行所需时间\n");

scanf("%d",&pcbP->time);

pcbP->next=NULL;

}

return pcbP;

}

int Delete(int id,PCBList &readyPcb,PCBList &nullPcb)//用于销毁一个pcb进程

{

if(pcbT) {

while(pcbT) {

if(pcbT->id==id) {

pcbF->next=pcbT->next;

pcbT->next=nullPcb;

nullPcb=pcbT;

printf("销毁成功\n");

return OK;

}

pcbT=pcbT->next;

pcbF=pcbF->next;

}

if(!pcbT) {

printf("没有要删除的pcb进程\n");

} }

else{

printf("没有要删除的pcb进程\n");

}

return OK;

}

void PrintPCB(PCBList &readyPcb)//打印pcb就绪序列

{

printf("就绪队列中的进程，按照优先级排序的序列为:\n");

printf("\t\t序号\t名字\t优先级\t运行时间\n");

PCBList pcbP=readyPcb->next;

while(pcbP)

{

printf("\t\t%d\t%s\t%d\t%d\n",pcbP->id,pcbP->name,pcbP->priority,pcbP->time);

pcbP=pcbP->next;

}

}

void InsertReadyPcb(PCBList &readyPcb,PCBList &pcb)

{

PCBList pcbF=readyPcb;

PCBList pcbT=readyPcb->next;

if(pcbT)

{

while(pcbT)

{

if(pcbT->priority<pcb->priority)

{

pcb->next=pcbT;

pcbF->next=pcb;

printf("创建成功并将进程插入到了就绪队列中了\n");

return;
简单的，容易的
