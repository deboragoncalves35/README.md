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
