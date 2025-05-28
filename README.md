// Autores: Arthur Machado e Thiago de Nardi

#include <iostream>     
#include <cstdlib>      // funções rand e srand
#include <ctime>        // para obter o tempo atual (usado na semente do rand)
using namespace std;    

int main() {
    int tamanhoSenha = 4;    // tamanho padrão da senha
    int maxTentativas = 10;  // numero máximo de tentativas
    int opcao = 0;           // variavel pra armazenar a opção do menu escolhida pelo usuário

    srand(time(0)); // inicializa o gerador de números aleatórios com base no tempo atual

    // loop principal do menu - continua até que o usuário escolha a opção 4
    while (opcao != 4) {
        // exibe o menu principal
        cout << "\n=== MENU ===\n";
        cout << "1 - Jogar\n";
        cout << "2 - Dificuldade\n";
        cout << "3 - Sobre\n";
        cout << "4 - Fim\n";
        cout << "Escolha uma opção: ";
        cin >> opcao; // le a opção escolhida pelo usuário

        // se o usuário escolheu jogar
        if (opcao == 1) {
            int senha[5]; // array para armazenar a senha gerada (até 5 dígitos)
            
            // gera números aleatórios para compor a senha
            for (int i = 0; i < tamanhoSenha; i++) {
                senha[i] = rand() % 10; // Números de 0 a 9
            }

            int acertou = 0; // flag para verificar se o jogador acertou a senha

            // loop de tentativas do jogador
            for (int t = 1; t <= maxTentativas; t++) {
                int tentativa[5]; // array para armazenar a tentativa do jogador
                int corretos = 0; // conta quantos dígitos estão corretos e na posição certa

                cout << "\nTentativa " << t << " de " << maxTentativas << endl;

                // recebe os números da tentativa do jogador
                for (int i = 0; i < tamanhoSenha; i++) {
                    cout << "Digite o numero " << i + 1 << ": ";
                    cin >> tentativa[i];

                    // validação da entrada - deve ser entre 0 e 9
                    while (tentativa[i] < 0 || tentativa[i] > 9) {
                        cout << "Número inválido. Digite entre 0 e 9: ";
                        cin >> tentativa[i];
                    }
                }

                // verifica quantos dígitos estão corretos e na posição certa
                for (int i = 0; i < tamanhoSenha; i++) {
                    if (tentativa[i] == senha[i]) {
                        corretos++; // incrementa o contador de acertos exatos
                    }
                }

                // mostra ao jogador quantos dígitos acertou
                cout << "Dígitos certos na posição correta: " << corretos << endl;

                // se todos os dígitos foram acertados
                if (corretos == tamanhoSenha) {
                    cout << "Parabéns! Você acertou a senha!\n";
                    acertou = 1; // marca que o jogador venceu
                    break;       // sai do laço de tentativas
                }
            }

            // se o jogador não acertou após todas as tentativas
            if (acertou == 0) {
                cout << "Você perdeu! A senha era: ";
                for (int i = 0; i < tamanhoSenha; i++) {
                    cout << senha[i]; // mostra a senha correta
                }
                cout << endl;
            }
        }

        // se o jogador escolheu mudar a dificuldade
        else if (opcao == 2) {
            int nivel; // armazena a dificuldade escolhida
            cout << "\nEscolha a dificuldade:\n";
            cout << "1 - Facil (3 dígitos)\n";
            cout << "2 - Médio (4 dígitos)\n";
            cout << "3 - Difícil (5 dígitos)\n";
            cin >> nivel;

            // altera o tamanho da senha e número de tentativas com base na dificuldade
            if (nivel == 1) {
                tamanhoSenha = 3;
                maxTentativas = 8;
            } else if (nivel == 2) {
                tamanhoSenha = 4;
                maxTentativas = 10;
            } else if (nivel == 3) {
                tamanhoSenha = 5;
                maxTentativas = 12;
            } else {
                cout << "Nível inválido. Mantida a dificuldade atual.\n";
            }
        }

        // se o jogador escolheu a opção "sobre"
        else if (opcao == 3) {
            cout << "\n=== SOBRE ===\n";
            cout << "Jogo simples de adivinhação de senha.\n";
            cout << "Desenvolvido dia 25/05/2025.\n";
            cout << "Desenvolvedores:\n";
            cout << "Arthur De Jesus Machado & Thiago De Nardi.\n";
            cout << "Tenha um bom jogo, e se divirta.\n";
        }

        // se o jogador escolheu sair do jogo
        else if (opcao == 4) {
            cout << "Encerrando o jogo...\n";
        }

        // caso a opção digitada não seja válida
        else {
            cout << "Opção inválida. Tente novamente.\n";
        }
    }

    return 0;
}
