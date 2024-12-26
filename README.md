- 👋 Hi, I’m @claudiocls
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
claudiocls/claudiocls is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->[Uploading gerar_numero.py…]()#!/usr/local/bin/python
# coding: utf-8
"""
Script que gera um número para jogar na Mega-Sena
"""

import sys
import random


def generate_number(qty):
    """ Retorna a quantidade de dezenas aleatórias informadas em 'qty' """
    numbers = list(range(1, 61))
    random.shuffle(numbers)

    selected_numbers = []
    even_numbers = 0
    odd_numbers = 0

    for num in numbers:
        # Permite incluir apenas X números
        if len(selected_numbers) == qty:
            break

        # Não inclui os números menos frequêntes
        #if num in [26, 55, 60, 40, 22, 39, 21, 57, 19, 25]:
        #    continue

        # Impede mais de um número na mesma coluna
        if num > 9:
            has_similar = False
            for sel in selected_numbers:
                if str(num)[-1] == str(sel)[-1]:
                    has_similar = True
                    break
            if has_similar:
                continue

        # Impede sequências
        if (num + 1) in selected_numbers or (num - 1) in selected_numbers:
            continue

        # Garante a mesma quantidade de pares e ímpares
        if num % 2 and odd_numbers > even_numbers:
            continue
        if not num % 2 and even_numbers > odd_numbers:
            continue

        # Incluí número
        selected_numbers.append(num)

        # Soma quantidade de pares e ímpares
        if num % 2:
            odd_numbers += 1
        else:
            even_numbers += 1

    # Ordena e formata números selecionados
    selected_numbers.sort()
    selected_numbers = [str(num).rjust(2, '0') for num in selected_numbers]

    print('Seu número é... %s' % ' '.join(selected_numbers))
    print('Boa sorte!')


if __name__ == '__main__':   
    qty = sys.argv[1] if len(sys.argv) > 1 else 6
    try:
        qty = int(qty)
    except:
        print('Informe um número inteiro.')
    else:
        if qty >= 6 and qty <= 15:
            generate_number(int(qty))
        else:
            print('Informe um número de 6 à 15.')


