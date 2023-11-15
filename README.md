#include <stdio.h> 
#include <locale.h> 
#include <stdlib.h> 
#include <stdbool.h>
#include <conio.h>

#define vazio '.' 
#define paredeV '|' 
#define paredeH '-' 
#define heroi '@' 
#define fantasma 'f' 
#define pilula 'p' 
#define explosao 'e'

char** mapa;
int linhas;
int colunas;
int posX, posY; // Posição do personagem '@'
int fantasmaX,fantasmaY; // Posição do fantasma 'f'
int pilulasColetadas = 0; // Número de pílulas coletadas
int podeAndar;
void fantasma;
void movimentarfantasma;

void imprimirMapa() 
{ system("cls"); // Limpa a tela 
for (int i = 0; i < linhas; i++) 
{ printf("%s\n", mapa[i]); 
} 
}

int main() 
{ 
setlocale(LC_ALL, "portuguese");

FILE* arq;
arq = fopen("pac.txt", "r");

if (arq == 0) 
{
    printf("Erro na leitura do arquivo\n");
    exit(1);
}

fscanf(arq, " %d %d", &linhas, &colunas);

mapa = (char**)malloc(sizeof(char*) * linhas);

for (int i = 0; i < linhas; i++) 
{
    mapa[i] = (char*)malloc(sizeof(char) * (colunas + 1));
    fscanf(arq, "%s", mapa[i]);
}

fclose(arq);

for (int i = 0; i < linhas; i++) 
{
    for (int j = 0; j < colunas; j++) 
	{
        if (mapa[i][j] == '@') 
		{
            posX = i;
            posY = j;
            break;
        }
    }
}

// Início do jogo
char movimento,explodiuMapa;
while (1) 
{
	imprimirMapa();
    
    printf("Use w para cima, a para a esquerda, s para baixo, d para a direita, e para explodir o mapa ou f para sair:\n ");
    scanf(" %c", &movimento);

    if (movimento == 'e') 
	{
        // Se o jogador pressionou 'e', explodir o mapa
        for (int i = 0; i < linhas; i++) 
		{
            for (int j = 0; j < colunas; j++) 
			{
                mapa[i][j] = explosao;
            }
        }
        explodiuMapa = true;
    }

    if (!explodiuMapa) {
        if (movimento == 'w') {
            if (mapa[posX - 1][posY] != '#') 
			{
                mapa[posX][posY] = ' ';
                posX--;
                mapa[posX][posY] = '@';
            }
        } else if (movimento == 'a') {
            if (mapa[posX][posY - 1] != '#') 
			{
                mapa[posX][posY] = ' ';
                posY--;
                mapa[posX][posY] = '@';
            }
        } else if (movimento == 's') {
            if (mapa[posX + 1][posY] != '#') 
			{
                mapa[posX][posY] = ' ';
                posX++;
                mapa[posX][posY] = '@';
            }
        } else if (movimento == 'd') {
            if (mapa[posX][posY + 1] != '#') 
			{
                mapa[posX][posY] = ' ';
                posY++;
                mapa[posX][posY] = '@';
            }
        }
    }
    if (explodiuMapa) 
	{
        printf("|--------|\n");
        printf("|    ....|\n");
        printf("|   @**|.|\n");
        printf("|..|.**..|\n");
        printf("|--------|\n");
        break;
    } else if (movimento == 'f') 
	{
        break;
    }
}

// Libera a memória
for (int i = 0; i < linhas; i++) 
{
    free(mapa[i]);
}
free(mapa);

return 0;
}

void fantasmas()
{
	for (int i=0;i<linhas;i++)
	{
		for(int j=0;j<colunas;j++)
		{
			if(mapa[i][j] == fantasmas)
			{
				fantasmaX = i;
                fantasmaY = j;
		}
		movimentarfantasma();
	}
}
}
void movimentarfantasma()
{
	srand(time(0));
	int posicao = rand()%4; // 0: cima, 1: esquerda, 2: baixo, 3: direita
	int opcoes[4][2] = {
		{xAtual,yAtual+1};	//baixo
		{xAtual+1,yAtual};	//dir
		{xAtual,yAtual-1};	//esq		
		{xAtual-1,yAtual};	//cima
	}
	if podeAndar(opcoes[posicao][0];opcoes[posicao][1])
	{
		mapa[fantasmaX][fantasmaY] = vazio;
		mapa[x][y] = fantasma;
		fantasmaX = x;
		fantasmaY = y;
		
	}
	
}
int podeAndar(int x,int y)
{
	if(mapa[x][y] == paredeV){
		return 0;
	}
	if(mapa[x][y] == paredeH){
		return 0;
	}
	if(mapa[x][y] == fantasma){
		return 0;
	}
	if(mapa[x][y] == pilula){
		return 0;
	}
	return 1;
}
	
