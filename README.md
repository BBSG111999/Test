## 欢迎光临吴超个人博客
<br />#include "stdio.h"
<br />#define max 10
<br />#define Max 1000
<br />#include "stdlib.h"
<br />//冒泡
<br />void MaoPao(int a[]){
<br />int i,j;
<br />int swap;
<br />for(i=0;i<max-1;i++){
	<br />for(j=0;j<max-1-i;j++){
		<br />if(a[j+1]<a[j]){
			<br />swap=a[j];
			<br />a[j]=a[j+1];
			<br />a[j+1]=swap;
		<br />}
	<br />}
<br />}
<br />}
<br />//插入排序
<br />void Insert(int Data[],int nNum){
	<br />int i,j,k,Temp;
	<br />for(i=0;i<nNum;i++){
		<br />Temp=Data[i];
		<br />for(j=0;j<=i;j++){
			<br />if(Data[j]>Temp){
				<br />for(k=i;k>j;--k)
					<br />Data[k]=Data[k-1];
				<br />Data[j]=Temp;
				<br />break;
			<br />}
		<br />}
	<br />}
<br />}
<br />struct src{
	<br />int v;        //结点
	<br />int shortest; //权值
<br />};
<br />/*
<br />普利姆算法：
<br />目的：根据图的邻接矩阵表示出图的最小生成树
<br />思想：用局部构造整体
<br />设置两个集合分别放顶点和边，初始为空
<br />选定图中的一个顶点为起始顶点开始构造最小生成树
<br />从顶点集合和剩下顶点中选取权值最先的两个顶点
<br />将非顶点集合中的顶点加入顶点集合中，将这两个顶点的边加入边的集合
<br />重复上述操作直到选取了(顶点-1)条边
<br />参数说明：
<br />LJJZ：图的邻接矩阵
<br />Point_Sum：结点个数
<br />G：辅佐数组
<br />*/
<br />void Prim(int LJJZ[][max],int Point_Sum,struct src G[]){
<br />int i,j,k;          //辅助变量 
<br />int min;            //存放G中最小的权值
<br />for(i=1;i<Point_Sum;i++){ //
<br />min=1000;           //min的值必须大于等于邻接矩阵中两结点不存在的值
<br />for(j=1;j<Point_Sum;j++){
	<br />if(G[j].shortest<min&&G[j].shortest>0){
		<br />min=G[j].shortest;  //获得G中的最先权值
		<br />k=j;
	<br />}
<br />}
<br />printf("%d--%d\n",G[k].v,k);
<br />G[k].shortest=0;
<br />//更新G
<br />for(j=0;j<Point_Sum;j++){ 
	<br />if(LJJZ[k][j]<G[j].shortest){
		<br />G[j].shortest=LJJZ[k][j];
		<br />G[j].v=k;
	<br />}
<br />}
<br />}
<br />}
<br />//测试普利姆
<br />void main(){
<br />int i,j;
<br />int Point_Sum;
<br />int LJJZ[max][max];
<br />struct src G[max];
<br />printf("请输入图的结点数：\n");
<br />scanf("%d",&Point_Sum);
<br />printf("请输入图的邻接矩阵,无穷以1000表示：\n");
<br />for(i=0;i<Point_Sum;i++){
	<br />for(j=0;j<Point_Sum;j++){
	<br />scanf("%d",&LJJZ[i][j]);
	<br />}
<br />}
<br />G[0].shortest=0;
<br />G[0].v=0;
<br />for(i=1;i<Point_Sum;i++){
	<br />G[i].shortest=LJJZ[0][i];
	<br />G[i].v=0;
<br />}
<br />Prim(LJJZ,Point_Sum,G);
<br />}
<br />/*
<br />汉诺塔问题：
<br />已知汉诺塔上有指针若干，从小到大排序在a杆子上
<br />现要求将a上的指针经b移动到c上，每次只能移动一个指针
<br />并且大的不能在小的上面
<br />思想：采用递归，入栈操作
<br />/
<br />void HanNuo(char a,char b,char c,int DishNumber){
	<br />if(DishNumber==1){
		<br />printf("%c-->%c\n",a,c);
	<br />}
	<br />else{
		<br />HanNuo(a,c,b,DishNumber-1);
		<br />printf("%c-->%c\n",a,c);
		<br />HanNuo(b,a,c,DishNumber-1);
	<br />}
<br />}
<br />//迪杰斯特拉
<br />void Dijkstra(int n,int v,int dist[],int prev[],int **cost){
	<br />int i,j,maxint=65535,*s,temp,u;
	<br />s=(int *)malloc(sizeof(int) *n);
	<br />for(i=1;i<n;i++){
		<br />dist[i]=cost[v][i];
		<br />s[i]=0;
		<br />if(dist[i]==maxint)
			<br />prev[i]=0;
		<br />else
			<br />prev[i]=v;
	<br />}
	<br />dist[v]=0;
	<br />s[v]=1;
	<br />for(i=1;i<n;i++)
	<br />{
		<br />temp=maxint;
		<br />u=v;
		<br />for(j=1;j<=n;j++){
			<br />if((!s[j])&&(dist[j]<temp)){
				<br />u=j;
				<br />temp=dist[j];
			<br />}
		<br />}
		<br />s[u]=1;
		<br />for(j=1;j<=n;j++){
			<br />if((!s[j])&&(cost[u][j]<maxint)){
				<br />int newdist=dist[u]+cost[u][j];
				<br />if(newdist<dist[j]){
					<br />dist[j]=newdist;
					<br />prev[j]=u;
				<br />}
			<br />}
		<br />}
	<br />}
<br />}
<br />void ShowPath(int n,int v,int u,int *dist,int *prev){
	<br />int j=0,w=u,count=0,*way;
	<br />way=(int *)malloc(sizeof(int)*(n+1));
	<br />while(w!=v){
		<br />count++;
		<br />way[count]=prev[w];
		<br />w=prev[w];
	<br />}
	<br />printf("路径为：\n");
	<br />for(j=count;j>=1;j--){
		<br />printf("%d->",way[j]);
	<br />}
	<br />printf("%d\n",u);
<br />}
<br />void main(){
	<br />int i,j,t,n,v,**cost,*dist,*prev;
	<br />printf("请输入结点数\n");
	<br />scanf("%d",&n);
	<br />printf("请输入结点\n");
	<br />cost=(int **)malloc(sizeof(int)*(n+1));
	f<br />or(i=1;i<=n;i++)
		<br />cost[i]=(int *)malloc(sizeof(int)*(n+1));
	<br />for(i=1;i<=n;i++)
		<br />for(t=1;t<=n;t++)
			<br />scanf("%d",&cost[i][t]);
		<br />dist=(int *)malloc(sizeof(int)*n);
		<br />prev=(int *)malloc(sizeof(int)*n);
		<br />printf("请输入源结点\n");
		<br />scanf("%d",&v);
		<br />Dijkstra(n,v,dist,prev,cost);
		<br />printf("最短路径为：\n");
		<br />for(i=1;i<=n;i++){
			<br />if(i!=v){
				<br /><br />printf("%d 到 %d 的距离为 %d:",v,i,dist[i]);
				<br />printf("%d %d",i,prev[i]);
				<br />ShowPath(n,v,i,dist,prev);
			<br />}
		<br />}
<br />}
