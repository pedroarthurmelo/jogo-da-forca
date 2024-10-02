# Jogo da Forca

# Trabalho realizado para Raciocínio Algorítmico

Este é um jogo simples de forca desenvolvido em Python. O jogador deve adivinhar uma palavra secreta, com um número limitado de tentativas.

## Como jogar

1. O jogador deve inserir a palavra secreta (apenas letras).
2. O jogador também define quantas tentativas terá para adivinhar a palavra.
3. Outro jogador tenta adivinhar a palavra, letra por letra ou diretamente a palavra inteira.

Se o jogador esgotar o número de tentativas sem acertar a palavra, o jogo termina e a palavra secreta é revelada.

## Código

Aqui está o código em Python do jogo:

```python
print('Bem vindo ao Jogo da Forca')

try:
    # Configuração do jogo
    stringA = input('Digite a Palavra Secreta: ').upper()
    while not stringA.isalpha():  # Verifica se a palavra contém apenas letras
        print("Erro: A palavra deve conter apenas letras.")
        stringA = input('Digite a Palavra Secreta: ').upper()

    while True:
        try:
            n_tentativas = int(input('Digite quantas tentativas: '))
            if n_tentativas > 0:
                break
            else:
                print("Erro: O número de tentativas deve ser positivo.")
        except ValueError:
            print("Erro: Digite um número válido.")

    # Limpa a tela (funciona em terminais que suportam ANSI)
    print("\x1b[2J\x1b[1;1H")

    # Prepara a string oculta com sublinhados
    stringB = ['_'] * len(stringA)

    # Jogo
    print(f'A palavra tem {len(stringA)} caracteres')

    while n_tentativas > 0 and "_" in stringB:
        entrada = input('Digite uma letra ou palavra: ').upper()

        if len(entrada) == 1 and not entrada.isalpha():
            print("Erro: Digite apenas letras.")
            continue

        if entrada == stringA:
            stringB = list(stringA)  # Revela a palavra completa
            break

        if len(entrada) == 1 and entrada in stringA:
            for i, letra in enumerate(stringA):
                if letra == entrada:
                    stringB[i] = entrada
        else:
            print("Letra ou palavra incorreta!")

        n_tentativas -= 1
        print(f'Você tem {n_tentativas} tentativas restantes')
        print(' '.join(stringB))

    if "_" not in stringB:
        print('Parabéns, você acertou!')
    else:
        print(f'Que pena, esgotou as tentativas. A palavra correta era {stringA}.')

    print('########################## Fim de Jogo ##########################')

except KeyboardInterrupt:
    print("\nJogo interrompido pelo usuário. Até a próxima!")
except Exception as e:
    print(f"Ocorreu um erro inesperado: {e}")
