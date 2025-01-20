#include <stdio.h>
#include <string.h>
#include <ctype.h>

// Simula o arquivo conta_palavras.h
#ifndef CONTA_PALAVRAS_H
#define CONTA_PALAVRAS_H

typedef struct {
    char palavra[50];
    int frequencia;
} Palavra;

void contar_palavras(const char* nome_arquivo, Palavra* palavras, int* total_palavras);
void ordenar_palavras(Palavra* palavras, int total_palavras);

#endif

// Simula o arquivo conta_palavras.c
void contar_palavras(const char* nome_arquivo, Palavra* palavras, int* total_palavras) {
   FILE* arquivo = fopen(nome_arquivo, "r");
    if (!arquivo) {
        printf("Erro ao abrir o arquivo '%s'.\n", nome_arquivo);
        *total_palavras = 0;
        return;
    }
char palavra_atual[50];
*total_palavras = 0;

while (fscanf(arquivo, "%49s", palavra_atual) != EOF) {
        for (int i = 0; palavra_atual[i]; i++) {
            palavra_atual[i] = tolower(palavra_atual[i]);
        }
        int encontrada = 0;
        for (int i = 0; i < *total_palavras; i++) {
            if (strcmp(palavras[i].palavra, palavra_atual) == 0) {
                palavras[i].frequencia++;
                encontrada = 1;
                break;
            }
        }
        if (!encontrada) {
            strcpy(palavras[*total_palavras].palavra, palavra_atual);
            palavras[*total_palavras].frequencia = 1;
            (*total_palavras)++;
        }
    }
    fclose(arquivo);
}
