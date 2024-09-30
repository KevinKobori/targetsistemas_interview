# Pergunta 1:

```dart
void main() {
  int INDICE = 12, SOMA = 0, K = 1;

  while (K < INDICE) {
    K = K + 1;
    SOMA = SOMA + K;
  }

  print(SOMA); // Resposta: 77
}
```

Durante a execução desse trecho, a variável SOMA será incrementada continuamente enquanto K 
for menor que o valor de INDICE, que é 12. Ao final, SOMA terá o valor de 77, pois é a soma 
dos números de 2 até 11. Basicamente, estamos somando 2 + 3 + 4 ... + 12.