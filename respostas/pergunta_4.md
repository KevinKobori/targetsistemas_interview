# Pergunta 4:

Para essa aplicação de cadastro de clientes, a estrutura de banco de dados proposta seria a seguinte:

Clientes: armazena as informações dos clientes.
id_cliente (PK)
nome_razao_social
estado (referência à tabela de estados)

Telefones: guarda os números de telefone de cada cliente.
id_telefone (PK)
id_cliente (FK, referencia a tabela de Clientes)
numero
tipo_telefone (FK, referencia a tabela de TipoTelefone)

TipoTelefone: armazena os tipos de telefone.
id_tipo_telefone (PK)
descricao

Estados: armazena os estados brasileiros.
id_estado (PK)
uf (abreviação do estado, como "SP", "RJ", etc.)

Utilizando o app https://dbdiagram.io/

Necessitaremos colar o seguinte diagrama:
```shell
Table Clientes {
  id_cliente int [pk]
  nome_razao_social varchar
  estado varchar
}

Table Telefones {
  id_telefone int [pk]
  id_cliente int [ref: > Clientes.id_cliente]
  numero varchar
  tipo_telefone int [ref: > TipoTelefone.id_tipo_telefone]
}

Table TipoTelefone {
  id_tipo_telefone int [pk]
  descricao varchar
}

Table Estados {
  id_estado varchar [pk]
  uf varchar
}

Ref: Clientes.estado > Estados.id_estado
```

## Imagem gerada pelo https://dbdiagram.io/:
![Alt text](./respostas/pergunta_4.png)

Relacionamentos:
Um cliente pode ter muitos telefones (1
).
Um telefone tem um tipo específico (N:1).
Um cliente pertence a um estado (N:1).
Aqui está um exemplo de SQL para buscar os clientes de São Paulo com seus telefones:
```dart
SELECT c.id_cliente, c.nome_razao_social, t.numero 
FROM Clientes c
JOIN Telefones t ON c.id_cliente = t.id_cliente
JOIN Estados e ON c.estado = e.id_estado
WHERE e.uf = 'SP';
```
