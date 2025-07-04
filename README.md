# 🎮 Jogo da Velha em C++

Um simples e divertido **jogo da velha (tic-tac-toe)** feito em **C++**, jogado no terminal por **dois jogadores**.

---

## 🧠 Funcionalidades

- ✅ Dois jogadores locais (X e O)
- ✅ Verificação automática de vitória
- ✅ Detecção de empate
- ✅ Validação de entradas
- ✅ Interface em modo texto

---

## 🖥️ Como rodar:

```
#include <iostream>
using namespace std;

// Tabuleiro 3x3 com posições numeradas de 1 a 9
char board[3][3] = {
    {'1','2','3'},
    {'4','5','6'},
    {'7','8','9'}
};

char current_marker;    
int current_player;    

void drawBoard() {
    cout << "\n";
    cout << " " << board[0][0] << " | " << board[0][1] << " | " << board[0][2] << "\n";
    cout << "---|---|---\n";
    cout << " " << board[1][0] << " | " << board[1][1] << " | " << board[1][2] << "\n";
    cout << "---|---|---\n";
    cout << " " << board[2][0] << " | " << board[2][1] << " | " << board[2][2] << "\n";
    cout << "\n";
}

bool placeMarker(int slot) {
    int row = (slot - 1) / 3; 
    int col = (slot - 1) % 3; 

  
    if (board[row][col] != 'X' && board[row][col] != 'O') {
        board[row][col] = current_marker;
        return true;
    } else {
        return false; 
    }
}


bool checkWinner() {
   
    for (int i = 0; i < 3; i++) {
        // Linha
        if (board[i][0] == board[i][1] && board[i][1] == board[i][2])
            return true;

        // Coluna
        if (board[0][i] == board[1][i] && board[1][i] == board[2][i])
            return true;
    }

  
    if (board[0][0] == board[1][1] && board[1][1] == board[2][2])
        return true;

    if (board[0][2] == board[1][1] && board[1][1] == board[2][0])
        return true;

    return false;
}


void swap_player_and_marker() {
    if (current_marker == 'X') {
        current_marker = 'O';
        current_player = 2;
    } else {
        current_marker = 'X';
        current_player = 1;
    }
}


int main() {
    cout << "=== JOGO DA VELHA ===\n\n";
    cout << "Jogador 1, escolha seu marcador (X ou O): ";
    cin >> current_marker;

   
    current_player = 1;

    drawBoard();

    int slot;

    for (int turn = 1; turn <= 9; turn++) {
        cout << "Jogador " << current_player << " (" << current_marker << "), escolha uma posição (1-9): ";
        cin >> slot;

        if (slot < 1 || slot > 9) {
            cout << "Entrada inválida. Escolha um número de 1 a 9.\n";
            turn--;
            continue;
        }

        if (!placeMarker(slot)) {
            cout << "Espaço já ocupado. Tente novamente.\n";
            turn--;
            continue;
        }

        drawBoard(); 
        if (checkWinner()) {
            cout << "Parabéns! Jogador " << current_player << " venceu o jogo!\n";
            return 0;
        }

        // Alterna o jogador
        swap_player_and_marker();
    }

    cout << "Empate! Ninguém venceu.\n";
    return 0;
}

```
