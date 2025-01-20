stdio.h>
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

void ordenar_palavras(Palavra* palavras, int total_palavras) {
    for (int i = 0; i < total_palavras - 1; i++) {
        for (int j = i + 1; j < total_palavras; j++) {
            if (strcmp(palavras[i].palavra, palavras[j].palavra) > 0) {
                Palavra temp = palavras[i];
                palavras[i] = palavras[j];
                palavras[j] = temp;
            }
        }
    }
}

// Simula o arquivo testa_conta_palavras.c
void teste_abrir_arquivo() {
    Palavra palavras[100];
    int total_palavras;

    contar_palavras("arquivo_inexistente.txt", palavras, &total_palavras);

    if (total_palavras != 0) {
        printf("Falha no teste_abrir_arquivo: total_palavras deveria ser 0.\n");
    } else {
        printf("Passou no teste_abrir_arquivo.\n");
    }
}

void teste_contar_palavras() {
    Palavra palavras[100];
    int total_palavras;

    FILE* arquivo = fopen("teste.txt", "w");
    fprintf(arquivo, "teste teste palavra");
    fclose(arquivo);

    contar_palavras("teste.txt", palavras, &total_palavras);

    if (total_palavras == 2 && palavras[0].frequencia == 2 && palavras[1].frequencia == 1) {
        printf("Passou no teste_contar_palavras.\n");
    } else {
        printf("Falha no teste_contar_palavras.\n");
    }
}

void teste_ordenar_palavras() {
    Palavra palavras[3] = {
        {"zebra", 1},
        {"banana", 2},
        {"abacaxi", 1}
    };
    int total_palavras = 3;

    ordenar_palavras(palavras, total_palavras);

    if (strcmp(palavras[0].palavra, "abacaxi") == 0 &&
        strcmp(palavras[1].palavra, "banana") == 0 &&
        strcmp(palavras[2].palavra, "zebra") == 0) {
        printf("Passou no teste_ordenar_palavras.\n");
    } else {
        printf("Falha no teste_ordenar_palavras.\n");
    }
}

int main() {
    printf("Iniciando os testes...\n");

    teste_abrir_arquivo();
    teste_contar_palavras();
    teste_ordenar_palavras();

    printf("Testes concluídos.\n");
    return 0;
}
