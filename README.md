# O Crivo de Eratóstenes: Encontrando Primos com Eficiência

O **Crivo de Eratóstenes** é um algoritmo elegante e antigo para encontrar todos os números primos até um determinado limite. Ele se destaca pela sua simplicidade e eficiência, evitando cálculos desnecessários. Vamos mergulhar em uma explicação detalhada de seu funcionamento:

## Conceito Central
A ideia fundamental do algoritmo é eliminar iterativamente os múltiplos de números primos, começando com 2. Isso se baseia no fato de que qualquer múltiplo de um número primo não pode ser primo.

## Passo a Passo
### Inicialização:
- Crie um vetor booleano chamado `eh_primo` com tamanho `n + 1`, onde `n` é o limite superior para a busca de primos.
- Inicialize todos os elementos de `eh_primo` como `true`, assumindo inicialmente que todos os números são primos.
- Defina `eh_primo[0]` e `eh_primo[1]` como `false`, pois 0 e 1 não são primos.

### Iteração pelos Possíveis Primos:
- Percorra o vetor `eh_primo` do índice 2 até a raiz quadrada de `n`.
- Para cada índice `i`, verifique se `eh_primo[i]` é `true`:
  - Se for `true`, significa que `i` é primo.
  - Inicie um loop interno para marcar os múltiplos de `i`.

### Marcação dos Múltiplos:
- O loop interno começa no índice `i * i` e incrementa em `i` a cada iteração.
- Para cada índice `j` no loop interno, defina `eh_primo[j]` como `false`, pois `j` é um múltiplo de `i` e, portanto, não é primo.
- O loop interno evita marcar os múltiplos menores que `i * i`, pois eles já foram marcados por primos anteriores.

### Extração dos Primos:
- Após a conclusão dos loops, os índices restantes com `eh_primo[i]` como `true` representam os números primos até `n`.
- Você pode criar um novo vetor para armazenar esses primos ou simplesmente iterar pelo `eh_primo` e imprimir/utilizar os primos identificados.

## Exemplo
Vamos encontrar todos os primos até 10:
### Inicialização:
```
Índice:   0  1  2  3  4  5  6  7  8  9  10
eh_primo: F  F  T  T  T  T  T  T  T  T  T
```
Use code with caution.
### Iteração e Marcação:
- `i = 2` (primo): Marcamos 4, 6, 8, 10 como `false`.
- `i = 3` (primo): Marcamos 9 como `false`.
- `i = 4`: Ignorado, pois `eh_primo[4]` é `false`.
- `i = 5` (primo): 10 já está marcado.
- Loop externo termina.

### Resultado:
```
Índice:   0  1  2  3  4  5  6  7  8  9  10
eh_primo: F  F  T  T  F  T  F  T  F  F  F
```
Use code with caution.

Os primos até 10 são: 2, 3, 5, 7.

## Código em C++
```cpp
#include <iostream>
#include <vector>

using namespace std;

vector<int> crivo_de_eratostenes(int n) {
    vector<bool> eh_primo(n + 1, true);
    eh_primo[0] = eh_primo[1] = false;

    for (int i = 2; i * i <= n; ++i) {
        if (eh_primo[i]) {
            for (int j = i * i; j <= n; j += i) {
                eh_primo[j] = false;
            }
        }
    }

    vector<int> primos;
    for (int i = 2; i <= n; ++i) {
        if (eh_primo[i]) {
            primos.push_back(i);
        }
    }

    return primos;
}

int main() {
    int n;
    cout << "Digite o limite superior: ";
    cin >> n;

    vector<int> primos = crivo_de_eratostenes(n);

    cout << "Números primos até " << n << ":" << endl;
    for (int primo : primos) {
        cout << primo << " ";
    }
    cout << endl;

    return 0;
}
```

## Eficiência e Limitações
- **Eficiência:** O Crivo de Eratóstenes é mais eficiente que a verificação de primalidade individual para cada número. Ele evita cálculos desnecessários, especialmente para intervalos maiores.
- **Limitações:** Para números extremamente grandes, o Crivo de Eratóstenes pode exigir muita memória devido ao vetor `eh_primo`. Existem algoritmos mais avançados para esses casos, como o Crivo de Atkin.

## Conclusão
O Crivo de Eratóstenes é uma ferramenta poderosa e intuitiva para encontrar números primos. Sua simplicidade e eficiência o tornam uma escolha popular em várias aplicações, desde a matemática básica até a criptografia.
