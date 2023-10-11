#include <stdio.h>
#include <locale.h>
#include <stdlib.h>

char** mapa;
int linhas;
int colunas;

int main()
{
	setlocale(LC_ALL,"portuguese");

	FILE* arq;
	arq = fopen("pac.txt","r");

	if(arq == 0)
	{
		printf("erro na  leitura do arq");
		exit(1);
	}

	fscanf(arq," %d %d",&linhas,&colunas);
	mapa = malloc(sizeof(char*)* linhas);
		
	for (int i = 0; i < 10 ; i++)
	{
	mapa[i] = malloc(sizeof(char)* colunas+1);
	}
		
	for (int i = 0; i < 5; i++)
	{
		fscanf(arq, "%s", mapa[i]);
	}
	for (int i = 0; i < 5; i++)
	{
		printf("%s\n",mapa[i]);
	}
	free(mapa);

	fclose(arq);
}
