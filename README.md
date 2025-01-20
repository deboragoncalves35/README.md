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
