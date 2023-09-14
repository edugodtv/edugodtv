import random

# Cria o tabuleiro do jogo como uma lista de listas 5x5
tabuleiro = [['~' for _ in range(5)] for _ in range(5)]

# Função para exibir o tabuleiro
def exibir_tabuleiro(tabuleiro):
    for linha in tabuleiro:
        print(" ".join(linha))
    print()

# Função para posicionar os navios aleatoriamente
def posicionar_navios(tabuleiro):
    for _ in range(3):  # Vamos colocar 3 navios
        navio_linha = random.randint(0, 4)
        navio_coluna = random.randint(0, 4)
        # Verifica se já existe um navio na posição gerada
        while tabuleiro[navio_linha][navio_coluna] == 'X':
            navio_linha = random.randint(0, 4)
            navio_coluna = random.randint(0, 4)
        tabuleiro[navio_linha][navio_coluna] = 'X'

# Função principal do jogo
def jogo_batalha_naval():
    print("Bem-vindo ao Jogo de Batalha Naval!")
    exibir_tabuleiro(tabuleiro)
    posicionar_navios(tabuleiro)

    tentativas = 0
    max_tentativas = 10

    while tentativas < max_tentativas:
        try:
            palpite_linha = int(input("Digite a linha (0-4): "))
            palpite_coluna = int(input("Digite a coluna (0-4): "))

            if 0 <= palpite_linha <= 4 and 0 <= palpite_coluna <= 4:
                if tabuleiro[palpite_linha][palpite_coluna] == 'X':
                    print("Parabéns! Você acertou um navio!")
                    tabuleiro[palpite_linha][palpite_coluna] = '!'
                else:
                    print("Você errou. Tente novamente.")
                tentativas += 1
                exibir_tabuleiro(tabuleiro)
            else:
                print("Por favor, insira valores entre 0 e 4.")

            if tentativas == max_tentativas:
                print("Fim de jogo! Você atingiu o limite de tentativas.")
                break
        except ValueError:
            print("Por favor, digite números válidos.")

# Inicia o jogo
jogo_batalha_naval()
