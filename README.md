stdio.h>
#include <string.h>
#include <ctype.h>

// Simula o arquivo conta_palavras.h
#ifndef CONTA_PALAVRAS_H
#define CONTA_PALAVRAS_H

ypedef struct {
    char palavra[50];
    int frequencia;
} Palavra;
