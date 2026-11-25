# M4 · Relatório de encerramento do laboratório AWS em Ohio

**Revisão de 25/11/2026** · **Estado** Encerramento concluído. O Cost Explorer exibiu US$ 0,00 para Ohio no período dos ensaios.

## Escopo, arquitetura e operação

O laboratório operou em `us-east-2` no Free Plan, com limite de **US$ 0 em cobranças**. A stack CloudFormation declara um único bucket privado, com SSE-S3, Bucket Owner Enforced e os quatro bloqueios de acesso público. A saída `BucketName` liga o recurso lógico ao bucket efetivo. No ensaio IAM, o operador criou o objeto fictício e assumiu um papel STS de leitura limitada àquele objeto. O detector processou campos sanitizados de eventos de gerenciamento do CloudTrail Event history. [Template versionado](https://github.com/raphaelguterres/cloud-security-detection-lab/blob/288a42b64fb2404f0ba23424847120a418b6b6ba/infra/bucket-evidencias.json)

## Operação e remoção por ensaio

| Ensaio de 24/11 · horários UTC | Como o recurso foi identificado | Resultado e evidência de remoção |
| --- | --- | --- |
| CloudFormation · 20:53–20:54 | `BucketName` correspondeu ao identificador físico de `BucketEvidencias`. A conferência posterior verificou que os eventos de criação e exclusão traziam o mesmo identificador físico. | Stack e bucket chegaram a `DELETE_COMPLETE` às 20:53:37. A listagem regional não encontrou o mesmo bucket. A checagem das proteções em execução ficou inconclusiva nesse ensaio. [Ciclo de IaC aceito](https://github.com/raphaelguterres/cloud-security-detection-lab/blob/1304d94037e90db1179bc4f40baabc078213973c/docs/VALIDACAO-IAC-OHIO.md) |
| IAM · 21:13–21:14 | Uma nova stack criou o bucket do ensaio. A mesma sessão STS executou as duas operações no mesmo objeto fictício. | `GetObject` retornou `200` e `PutObject` retornou `403 AccessDenied`. Conteúdo e ETag permaneceram iguais. As proteções foram verificadas pela API. Após a limpeza, o papel retornou `NoSuchEntity`, a stack e o bucket chegaram a `DELETE_COMPLETE` e a listagem não encontrou esse bucket. [IAM aceito](https://github.com/raphaelguterres/cloud-security-detection-lab/blob/dd2ced0ebfb59da4a15867ec991c5682e52c2f01/docs/VALIDACAO-IAM-S3-OHIO.md) |
| CloudTrail · 22:13 | Os três eventos de gerenciamento foram correlacionados à mesma conta, região e bucket temporário do ensaio. | `PutBucketPublicAccessBlock`, `PutBucketPolicy` e `DeleteBucket` produziram três sinais. Os bloqueios públicos permaneceram ativos. A consulta ao mesmo bucket após a exclusão retornou HTTP `404`. [Validação e reprodução](https://github.com/raphaelguterres/cloud-security-detection-lab/blob/635e7e40b13012a4159c4ed1f19a1b4d820eed2b/docs/VALIDACAO-CLOUDTRAIL-S3-OHIO.md) |

Em 25/11, a reprodução local com a projeção sanitizada confirmou os três sinais, e os seis testes do detector passaram. A correlação dos recursos ocorreu dentro de cada ensaio. Os identificadores físicos, as credenciais e os registros brutos foram omitidos.

## Faturamento em 25/11

Na primeira consulta de 25/11, o Cost Explorer exibiu US$ 0,00 no total da conta e zero regiões. Na nova consulta, por volta das 19h19 no horário de Brasília (22h19 UTC), o agrupamento por Região passou a exibir Ohio.

| Fonte | Resultado observado | Alcance da evidência |
| --- | --- | --- |
| AWS Settings · Faturamento | Plano gratuito e **US$ 0,00 de valor devido** no registro anterior. | Valor devido da conta na consulta registrada. |
| Cost Explorer · 01–25/11/2026 UTC, agrupado por Região | **Leste dos EUA (Ohio), US$ 0,00**. O total do projeto também exibiu **US$ 0,00**. | Custos não combinados, excluindo `Credit` e `Refund`. O recorte cobre os três ensaios de 24/11, cujos horários UTC constam acima. |

O valor é a estimativa de novembro apresentada pelo console no momento da leitura. A interface consultada não mostrou a hora de processamento. A consulta foi gratuita e somente leitura. [Faturamento por projeto](https://docs.aws.amazon.com/accounts/latest/reference/view-billing-information.html) · [Estimativa mensal e fatura](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/differences-billing-data-cost-explorer-data.html)

O M4 está com **6 de 6 critérios técnicos concluídos**. [Checklist do M4](PROGRESSO.md#m4--cloud-security-e-iac--110180-h-estimadas)
