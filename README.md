#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <string.h>

#define TOTAL_CARTAS 3

typedef struct {
    char nome[30];
    int forca;
    int velocidade;
    int inteligencia;
} Carta;

void exibirCarta(Carta c) {
    printf("Nome: %s\n", c.nome);
    printf("Força: %d\n", c.forca);
    printf("Velocidade: %d\n", c.velocidade);
    printf("Inteligência: %d\n", c.inteligencia);
}

int main() {
    srand(time(NULL)); // semente aleatória

    // 1. Baralho de cartas
    Carta baralho[TOTAL_CARTAS] = {
        {"Dragão", 90, 60, 70},
        {"Fênix", 70, 80, 85},
        {"Golem", 95, 40, 60}
    };

    // 2. Sorteio de cartas para os jogadores
    int indice1 = rand() % TOTAL_CARTAS;
    int indice2;

    do {
        indice2 = rand() % TOTAL_CARTAS;
    } while (indice2 == indice1);

    Carta jogador1 = baralho[indice1];
    Carta jogador2 = baralho[indice2];

    printf("Sua carta:\n");
    exibirCarta(jogador1);

    // 3. Jogador escolhe atributo
    int escolha;
    printf("\nEscolha um atributo:\n");
    printf("1 - Força\n2 - Velocidade\n3 - Inteligência\n");
    printf("Digite sua escolha: ");
    scanf("%d", &escolha);

    // 4. Comparar os atributos
    int valor1, valor2;

    switch (escolha) {
        case 1:
            valor1 = jogador1.forca;
            valor2 = jogador2.forca;
            break;
        case 2:
            valor1 = jogador1.velocidade;
            valor2 = jogador2.velocidade;
            break;
        case 3:
            valor1 = jogador1.inteligencia;
            valor2 = jogador2.inteligencia;
            break;
        default:
            printf("Escolha inválida.\n");
            return 1;
    }

    printf("\nCarta do oponente:\n");
    exibirCarta(jogador2);

    // 5. Resultado
    printf("\nResultado: ");
    if (valor1 > valor2)
        printf("Você venceu!\n");
    else if (valor1 < valor2)
        printf("Você perdeu!\n");
    else
        printf("Empate!\n");

    return 0;
}
