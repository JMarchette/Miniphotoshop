
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
void aumentarBrilho(int** original, int linhas, int colunas, int maxValor)
{	int l, c;
	for(l=0; l<linhas; l++)
	{	for(c=0; c<colunas; c++)
		{	original[l][c] = (int)(original[l][c] * 1.2);
			if(original[l][c] > maxValor)
				original[l][c] = maxValor;
		}
	}
}

void diminuirBrilho(int** original, int linhas, int colunas)
{	int l, c;
	for(l=0; l<linhas; l++)
	{	for(c=0; c<colunas; c++)
		{	
      original[l][c] = (int)(original[l][c] / 1.2);
		}
	}
}

void diminuirContraste(int** original, int linhas, int colunas, int maxValor)
{   int l, c;
    for(l=0; l<linhas; l++)
    {    for(c=0; c<colunas; c++)
        if(original[l][c] <= 128)
        {
            original[l][c] = (int)(original[l][c] * 1.2);
            if(original[l][c] > maxValor)
            original[l][c] = maxValor;
        }
        else 
        original[l][c] = (int)(original[l][c] / 1.2);
    }
}

/* void diminuirContraste (int ** original, int linhas, int colunas)
{
  int l, c;
  for(l=0; l<linhas; l++)
  {
    for(c=0; c<colunas; c++)
    {
      if (l <= 128 || c >= 128)
      {
        original[l][c] = (int)(original[l][c] * 1.2);
      }
      else
      {
        original[l][c] = (int)(original[l][c] / 1.2);
      }
    }
  }
} */

void aumentarContraste(int** original, int linhas, int colunas, int maxValor)
{   int l, c;
    for(l=0; l<linhas; l++)
    {    for(c=0; c<colunas; c++)
        if(original[l][c] <= 128)
        {
            original[l][c] = (int)(original[l][c] / 1.2);
        }
        else
        {
            original[l][c] = (int)(original[l][c] * 1.2);
            if(original[l][c] > maxValor)
            original[l][c] = maxValor;
        }
    }
}

void borrar(int** original, int linhas, int colunas, int tamanhoBorrao)
{	int l, c;

  int **nova, i;
	nova = (int **) malloc(linhas * sizeof(int *));
	for(i=0; i<linhas; i++)
  {
		nova[i] = (int *) malloc(colunas * sizeof(int));
  }
 
	for(l=tamanhoBorrao; l<linhas-tamanhoBorrao; l++)
  {
		for(c=tamanhoBorrao; c<colunas-tamanhoBorrao; c++)
    {
			nova[l][c] = (original[l][c] + original[l+tamanhoBorrao][c]
				+ original[l-tamanhoBorrao][c] + original[l][c+tamanhoBorrao]
				+ original[l][c-tamanhoBorrao])/5;
    }
  }
	return nova;
}

void espelharV(int** original, int linhas, int colunas)
{	
  int l,c,aux;
	for(l=0; l<linhas/2; l++) //inverte os elementos da matriz verticalmente
  {
		for(c=0; c<colunas; c++)
		{	
      aux = original[l][c];
			original[l][c] = original[linhas - 1 - l][c];
			original[linhas - 1 - l][c] = aux;
		}
  }
}

void espelharH(int** original, int linhas, int colunas)
{	
  int l,c,aux, inicio = 0;
	for(l=0; l<linhas; l++) // inverte os elementros de matriz horizontalmente
  {
		for(c=0; c<colunas/2; c++)
		{	
      aux = original[l][c];
			original[l][c] = original[l][colunas - 1 - c];
			original[l][colunas - 1 - c] = aux;
		}
  }
}

void fazerMoldura(int ** original, int linhas, int colunas)
{
  int l, c;

  for(c=0; c<colunas; c++)
  {
    for(l=0; l<linhas; l++)
    {
      if (l<10 || l>linhas-10)
      {
        original[l][c] = (int)(original[l][c] / 2);
      }
      if (c<10 || c>colunas-10)
      {
        original[l][c] = (int)(original[l][c] / 2);
      }
    }
  }
}

int** lerImagem(char * nomeArquivo, int *pLinhas, int *pColunas, int *pMaxValor)
{	FILE *fp;
	fp = fopen(nomeArquivo,"r");
	/* Arquivo ASCII, para leitura */
	if(!fp)
	{	printf( "\nErro na abertura do arquivo\n\n");
		exit(-1);
	}
	//leia tipo do arquivo
	char buffer[1001];
	fgets (buffer, 1000, fp); //Primeira linha
	if(strstr(buffer, "P2") == NULL) // o tipo de arquivo eh diferente de P2?
	{	printf( "\nErro no tipo do arquivo\n\n");
		exit(-2);
	}
	//leia comentario
	fgets (buffer, 1000, fp);
	
	//leia dados da imagem
	fscanf(fp, "%d%d%d", pColunas, pLinhas, pMaxValor);
	
	//criando a matriz
	int **mat, i;
	mat = (int **) malloc(*pLinhas * sizeof(int *));
	for(i=0; i< *pLinhas; i++)
		mat[i] = (int *) malloc(*pColunas * sizeof(int));
	int l, c;
	for(l=0; l<*pLinhas; l++)
	{	for(c=0; c<*pColunas; c++)
			fscanf(fp, "%d", &mat[l][c]);
	}
	fclose(fp);
	return mat;
}
void escreverImagem(char * nomeArquivo, int ** mat, int linhas, int colunas, int maxValor)
{	FILE *fp;
	fp = fopen(nomeArquivo,"w");
	// Arquivo ASCII, para leitura
	if(!fp)
	{	printf( "\nErro na abertura do arquivo\n\n");
		exit(-1);
	}
	//escreva tipo do arquivo
	fprintf (fp, "P2\n");
	//escreva comentario
	fprintf (fp, "#Figura modificada...\n");
	//colunas, linhas
	fprintf(fp, "%d %d\n", colunas, linhas);
	//maxValor
	fprintf(fp, "%d\n", maxValor);
	int l, c;
	for(l=0; l<linhas; l++)
	{	for(c=0; c<colunas; c++)
		{	fprintf(fp, "%d ", mat[l][c]);
		}
		fprintf(fp, "\n");
	}
	fclose(fp);
}
int main(int argc, char * argv[])
{	char opcao[12]="0";
	int linhas=0, colunas=0, maxValor=0, **mat=NULL;
	int tamanhoBorrao = 8;
	char nomeArquivo[100]="";
	char nomeArquivoLeitura[100]="";
	char nomeArquivoEscrita[100]="";
	
 while(opcao[0] != 'S')
	{	printf("\n\nMini-photoshop\n\n");
		printf("A) Ler imagem\n");	
		printf("B) Gravar imagem\n");	
		printf("C) Aumentar o brilho\n");	
		printf("D) Diminuir o brilho\n");	
		printf("E) Aumentar contraste\n");
		printf("F) Diminuir contraste\n");
		printf("G) Desfocar\n");
		printf("H) Fazer moldura\n");
    printf("I) Espelhar horizontalmente\n");
    printf("J) Espelhar verticalmente\n");
    printf("K) Girar para a esquerda\n");
    printf("L) Girar para a direita\n");
		printf("S) Sair\n");
		printf("\nEntre a opcao desejada: ");	
		fgets(opcao, 10, stdin);
		switch(opcao[0])
		{	case 'A':
      case 'a':
				printf("\n\nEntre com o nome da imagem (sem extensao): ");
				fgets(nomeArquivo, 100, stdin);
				nomeArquivo[strlen(nomeArquivo)-1]='\0';
				strcpy (nomeArquivoLeitura, nomeArquivo);
				strcat (nomeArquivoLeitura, ".pgm");
				mat = lerImagem(nomeArquivoLeitura, &linhas, &colunas, &maxValor);
				break;
			case 'B':
     case 'b':
				strcpy (nomeArquivoEscrita, nomeArquivo);	
				strcat (nomeArquivoEscrita, "_editada.pgm");
				printf("\n\nA imagem sera salva como %s\n", nomeArquivoEscrita);
				escreverImagem(nomeArquivoEscrita, mat, linhas, colunas, maxValor);
				break;
			case 'C':
      case 'c':
				aumentarBrilho(mat, linhas, colunas, maxValor);
				break;
			case 'D':
      case 'd':
				//diminuirBrilho(mat, linhas, colunas, maxValor);
				diminuirBrilho(mat, linhas, colunas);
				break;
			case 'E':
      case 'e':
				aumentarContraste(mat, linhas, colunas, maxValor);
				break;
			case 'F':
      case 'f':
				diminuirContraste(mat, linhas, colunas, maxValor);
				break;
			case 'G':
      case 'g':
				//borrar(mat, linhas, colunas, tamanhoBorrao);		
				break;
			case 'H':
      case 'h':
				fazerMoldura(mat, linhas, colunas);
				break;
     case 'I':
     case 'i':
      espelharH(mat, linhas, colunas);
      break;
     case 'J':
     case 'j':
      espelharV(mat, linhas, colunas);
      break;
     case 'K':
     case 'k':
      break;

     case 'L':
     case 'l':
      break;
     case 'S':
     case 's':
      break;
		}
	}
	return 0;
}
