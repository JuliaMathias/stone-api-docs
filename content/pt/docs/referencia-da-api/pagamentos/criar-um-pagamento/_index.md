---
title: "Criar Um Pagamento"
slug: "criar-um-pagamento"
draft: false
date: "2019-06-04T19:16:40.905Z"
lastmod: "2021-09-23T15:16:04.117Z"
weight: 2
description: >
---

---

<br>

Usado para realizar pagamentos de boleto e concessionárias.


<br>

{{% pageinfo %}}
**Atenção**

O pagamento pode ser agendado através do campo `scheduled_to`. 

A data usada no campo `scheduled_to` deve estar entre a data `next_available_execution_date` e a data limite retornada no campo `execution_limit_date` da API de calendário de agendamento chamada com o parâmetro `operation_type=payment`. 

Caso a data escolhida seja menor do que `next_available_execution_date`, o pagamento será executado imediatamente. 

Caso a data seja maior que `execution_limit_date`, será retornado um erro 422 na criação. 

A criação e o agendamento de pagamentos pode acontecer em qualquer dia (incluindo fins de semana e feriados) e em qualquer horário.

{{% /pageinfo %}}


<br>

---


``` 
POST https://sandbox-api.openbank.stone.com.br/api/v1/payments
```

---

#### **BODY PARAMS**

---

<br>

**barcode***  `string` 

Código de barras do documento.

---

<br>

**account_id***  `string` 

Identificador da conta que irá pagar o documento.


---

<br>

**scheduled_to**  `string` 

Formato: `yyyy-mm-dd`

---

<br>

**amount** `integer`

O valor a ser pago, caso o boleto possa ser pago com um valor divergente ao valor total.
<br>Para consultar o valor a ser pago, sugerimos que realize uma simulação de pagamento [aqui]({{< relref "/docs/referencia-da-api/simulacoes-dry-run/simular-o-pagamento-de-um-documento/">}}) e verifique o valor mínimo e máximo aceito para o pagamento em questão.
<br>Caso não tenha alteração do valor total do pagamento, basta não enviar o campo `amount`.



#### **HEADERS**

---
<br>

**x-stone-idempotency-key***  `string`

Chave de idempotencia.


<br>


##### **Response**

```json
202 Accepted 
```
Body
```json
{
    "account_id": "8cbeb3d2-750f-4b14-81a1-143ad715c273",
    "amount": 100,
    "approval_expired_at": null,
    "approved_at": "2019-08-02T18:22:19Z",
    "approved_by": "user:08807157-f8e1-439e-a2ec-154ecb4bee13",
    "barcode": "89670000000010003137498189637166095077491613",
    "cancelled_at": null,
    "created_at": "2019-08-02T18:22:19Z",
    "created_by": "user:08807157-f8e1-439e-a2ec-154ecb4bee13",
    "details": null,
    "failed_at": null,
    "failure_reason_code": null,
    "failure_reason_description": null,
    "fee": 0,
    "finished_at": null,
    "id": "1879158c-03c6-48ff-b7c3-c34a992cfa9c",
    "refunded_at": null,
    "rejected_at": null,
    "rejected_by": null,
    "scheduled_to": null,
    "status": "APPROVED",
    "writable_line": "896700000004010003137493818963716605950774916130"
}
```
