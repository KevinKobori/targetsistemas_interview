# Pergunta 3:

```dart
import 'dart:math';

void main() {
  // Preparando os dados iniciais
  List<double> faturamento =
      geradorDeFaturamentoRandomicoComBaseEmTodosOsDiasUteisDe2024();

  double menor = double.infinity;
  double maior = double.negativeInfinity;
  double soma = 0;
  int diasComFaturamento = 0;

  for (var valor in faturamento) {
    if (valor < menor) menor = valor;
    if (valor > maior) maior = valor;
    soma += valor;
    diasComFaturamento++;
  }

  double media = soma / diasComFaturamento;
  int diasAcimaDaMedia = 0;

  for (var valor in faturamento) {
    if (valor > media) {
      diasAcimaDaMedia++;
    }
  }

  print("O menor valor de faturamento ocorrido em um dia do ano: $menor");
  print("O maior valor de faturamento ocorrido em um dia do ano: $maior");
  print(
      "Número de dias no ano em que o valor de faturamento diário foi superior à média anual: $diasAcimaDaMedia");
}

bool _isFeriado(DateTime date) {
  // Simulando lista de feriados nacionais do Brasil em 2024
  List<DateTime> feriados = [
    DateTime(2024, 1, 1), // Confraternização Universal
    DateTime(2024, 2, 12), // Carnaval
    DateTime(2024, 2, 13), // Carnaval
    DateTime(2024, 3, 29), // Sexta-feira Santa
    DateTime(2024, 4, 21), // Tiradentes
    DateTime(2024, 5, 1), // Dia do Trabalho
    DateTime(2024, 6, 20), // Corpus Christi
    DateTime(2024, 9, 7), // Independência do Brasil
    DateTime(2024, 10, 12), // Nossa Senhora Aparecida
    DateTime(2024, 11, 2), // Finados
    DateTime(2024, 11, 15), // Proclamação da República
    DateTime(2024, 12, 25), // Natal
  ];

  return feriados.contains(date);
}

bool _isDiaUtil(DateTime date) {
  // Verificar se o dia é útil (não é final de semana e não é feriado)
  return date.weekday != DateTime.saturday &&
      date.weekday != DateTime.sunday &&
      !_isFeriado(date);
}

List<double> geradorDeFaturamentoRandomicoComBaseEmTodosOsDiasUteisDe2024() {
  final double mediaInicial = 10000;
  List<double> faturamentoDiario = [];
  Random random = Random();

  // Percorrer todos os dias de 2024
  for (int mes = 1; mes <= 12; mes++) {
    for (int dia = 1; dia <= DateTime(2024, mes + 1, 0).day; dia++) {
      DateTime date = DateTime(2024, mes, dia);

      // Verificar se o dia é útil
      if (_isDiaUtil(date)) {
        // Gerar faturamento randômico com variação de +-30%
        double variacao = (random.nextDouble() * 0.6) - 0.3;
        double faturamento = mediaInicial * (1 + variacao);

        faturamentoDiario.add(faturamento);
      }
    }
  }

  return faturamentoDiario;
}
```