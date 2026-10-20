# Atendente IA Forwes × ERP NewSystem

Proposta técnica para oferecer o Atendente IA de WhatsApp como módulo do ERP NewSystem.

**Documento completo:** abra a página do projeto (link em *About*, à direita) ou o arquivo [`index.html`](index.html).

## Em uma frase

O lojista liga o módulo e passa a vender pelo WhatsApp usando o estoque, os preços e os clientes que já estão no ERP.

## O que tem aqui

| Arquivo | Para quê |
|---|---|
| `index.html` | Documento completo: o módulo, arquitetura, fluxo de um pedido, segurança, implantação e piloto |
| `openapi.yaml` | Contrato de integração proposto, no padrão OpenAPI 3. Abre no [Swagger Editor](https://editor.swagger.io) ou importa no Postman |

## Como funciona

```
Cliente (WhatsApp)  <-->  Atendente IA (Forwes)  <-- API HTTPS -->  ERP NewSystem
                          conversa e regras                         produtos, estoque,
                          recompra e avisos                         clientes, pedidos
```

O ERP continua sendo a fonte da verdade. O agente lê o que precisa e grava o pedido de volta.

## O que o agente precisa do ERP

| Método | Caminho | Uso |
|---|---|---|
| `GET` | `/v1/produtos?busca=` | Preço e estoque atuais |
| `GET` | `/v1/clientes?telefone=` | Reconhecer o cliente pelo WhatsApp |
| `GET` | `/v1/clientes/{id}/compras` | Histórico em todos os canais, para a recompra |
| `POST` | `/v1/pedidos` | Criar o pedido confirmado (com `Idempotency-Key`) |
| `PATCH` | `/v1/pedidos/{id}` | Marcar como pago ou cancelado |

Os caminhos são uma proposta. Se o ERP já tiver endpoints equivalentes, o agente é adaptado a eles.

Sem API disponível no início, o piloto pode começar com exportação diária de produtos e estoque (CSV).

## Testar agora

- [Atendente de pet shop](https://wesleywac11-netizen.github.io/demos-forwes/petshop.html)
- [Atendente por voz](https://wesleywac11-netizen.github.io/demos-forwes/clinica-voz.html)
- [Portfólio Forwes](https://wesleywac11-netizen.github.io/demos-forwes/)

Demonstrações com dados fictícios.

## Perguntas para o time NewSystem

1. O ERP já tem API para terceiros? Qual a documentação e a autenticação?
2. Existe ambiente de homologação com dados fictícios?
3. O ERP consegue chamar um endereço externo quando pedido ou estoque muda?
4. Como o pedido de venda é representado hoje (pedido, orçamento, venda de PDV)?
5. Qual segmento da base é o melhor candidato para o piloto?

---

Forwes · Wesley · versão 1.0 preliminar · 20/10/2026
