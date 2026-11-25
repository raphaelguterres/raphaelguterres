# Progresso em cibersegurança

[Perfil](../README.md) · [Plano de estudos e estimativas](ROADMAP_SOC_BLUE_TEAM_PLENO_SENIOR.md)

**Última atualização:** 24/11/2026. Cada marco reúne entregas, testes e o registro de aceite.

## Situação atual

Três dos cinco marcos foram concluídos. O M4 tem cinco de seis critérios técnicos concluídos. A prioridade atual é consolidar a operação, o encerramento e o faturamento do laboratório AWS.

| Marco | Estado | Evidência |
| --- | --- | --- |
| M0 · Engenharia de detecção | Concluído | Cinco regras Wazuh com regressões e seis alertas conferidos no Manager, no Indexer e no Discover. [Aceite das três fontes](https://github.com/raphaelguterres/detection-engineering-blue-team/blob/main/docs/phase3-final-three-stage-six-event-acceptance-20261102.md) |
| M1 · Threat hunting | Concluído | Três hipóteses validadas em laboratório. O proprietário aceitou os 17 itens em 10/11. [Revisão final](https://github.com/raphaelguterres/threat-hunting-detection-lab/blob/59eeef6/docs/m1-final-review-20261110.md) |
| M2 · AppSec e DevSecOps | Em andamento | Rodada VELAR aceita. O checklist técnico continua aberto. [Caso público do formulário em homologação](https://github.com/raphaelguterres/cloudflare-429-edge-lab/blob/main/docs/evidencias.md) |
| M3 · Resposta a incidentes | Concluído em laboratório | Dez testes com dados sintéticos. O relatório completo tem acesso restrito. [Resumo da revisão](#m3--incident-response--soar--90150-h-estimadas) |
| M4 · Segurança em nuvem | Em andamento | Ciclo de criação e remoção via CloudFormation e teste de privilégio mínimo aceitos. As três detecções do CloudTrail foram validadas em Ohio. [Evidência do CloudTrail](https://github.com/raphaelguterres/cloud-security-detection-lab/blob/635e7e40b13012a4159c4ed1f19a1b4d820eed2b/docs/VALIDACAO-CLOUDTRAIL-S3-OHIO.md) · [Aceite do IAM em Ohio](https://github.com/raphaelguterres/cloud-security-detection-lab/blob/dd2ced0ebfb59da4a15867ec991c5682e52c2f01/docs/VALIDACAO-IAM-S3-OHIO.md#aceite) |

## Checklist de milestones

### M0 — Fase 3 Detection Engineering concluída (02/11/2026) · 8–15 h originalmente estimadas

- [x] Criar e testar cinco regras de detecção customizadas.
- [x] Correlacionar seis eventos originais Manager → Indexer por ID, regra, agente e timestamp UTC.
- [x] Preparar verificador offline e testes para três fontes independentes — [PR #28 aprovado](https://github.com/raphaelguterres/detection-engineering-blue-team/pull/28).
- [x] **Inspecionar independentemente seis JSONs originais na aba Discover** e projetar apenas os campos de identidade para `.lab/phase3-discover.csv`; o CSV original do menu Reporting omitia timestamp e foi preservado **sem uso para o aceite**. [Metodologia](https://github.com/raphaelguterres/detection-engineering-blue-team/blob/main/docs/phase3-final-three-stage-six-event-acceptance-20261102.md).
- [x] Conferir os **mesmos seis eventos** na interface **Dashboard Discover**, independentemente do Console/Dev Tools, com `id`, `rule.id`, `agent.id` e timestamp UTC: **6/6 correspondências exatas** (saída offline, código 0).
- [x] Documentar aceite por regra sem IDs brutos e registrar conclusão na [Issue #4](https://github.com/raphaelguterres/detection-engineering-blue-team/issues/4).
- [x] Revisar o [estudo de caso](https://github.com/raphaelguterres/detection-engineering-blue-team/blob/main/docs/case-study-wazuh-detection-engineering.md) e delimitar escopo, resultado e lacuna de indexação histórica 27–30/10.

**Gate M0:** **PASS 6/6** para os seis alertas de cinco regras na janela UTC de 01–02/11/2026, comprovados nas três fontes. A [Issue #4](https://github.com/raphaelguterres/detection-engineering-blue-team/issues/4) registra o encerramento da Fase 3. A lacuna de indexação de 27–30/10 permanece **investigação separada**.

Documentação do laboratório Wazuh · [Repositório](https://github.com/raphaelguterres/detection-engineering-blue-team) · [Estado da Fase 3](https://github.com/raphaelguterres/detection-engineering-blue-team#estado-da-fase-3) · [Correlação Manager–Indexer](https://github.com/raphaelguterres/detection-engineering-blue-team/blob/main/docs/phase3-manager-indexer-exact-correlation-20261102.md)

### M1 — Threat Hunting e investigação · 35–60 h estimadas

Em 10/11/2026, o proprietário aceitou os 17 itens do marco. As três hipóteses foram validadas em exercícios controlados com eventos reais. A revisão registra a remoção da conta temporária de H02 como pendente de confirmação. [Revisão de encerramento](https://github.com/raphaelguterres/threat-hunting-detection-lab/blob/59eeef6/docs/m1-final-review-20261110.md)

<details>
<summary>Histórico de 2 de novembro e checklist daquela data</summary>

**Incremento de preparação implementado em 02/11/2026:** [PR #10 incorporado](https://github.com/raphaelguterres/threat-hunting-detection-lab/pull/10), com [três hipóteses documentadas](https://github.com/raphaelguterres/threat-hunting-detection-lab/blob/main/docs/m1-three-hunting-hypotheses.md), correlacionador Python offline e **20/20 testes sintéticos aprovados em Linux e Windows**. Os resultados representam somente validação do software de análise, **não novas detecções ou incidentes reais**.

- [x] Planejar três hipóteses novas e definir telemetria mínima, junções e limitações.
- [x] Implementar correlacionador offline com controles negativos **sintéticos**; ainda não caracteriza revisão de falsos positivos em produção.
- [ ] Construir três timelines de **novas investigações reais controladas** e registrar hipóteses alternativas.
- [ ] Demonstrar tuning e revisão de falsos positivos com evidência operacional, não apenas fixtures.
- [ ] Atualizar cobertura MITRE ATT&CK **a partir de evidências reais**, mantendo hipóteses como hipóteses até validação.
- [ ] Publicar estudos de caso sanitizados de M1 e registrar aceite final da fase.

**Revisão real limitada de H01 em 02/11:** o [PR #12](https://github.com/raphaelguterres/threat-hunting-detection-lab/pull/12) adicionou auditor somente leitura e 15 testes. Rodado no arquivo privado existente de seis identidades do Manager, mostrou que a regra **110120 antecedeu 110100 por 3.743,199 segundos**: ordem invertida e intervalo superior a 15 minutos. **Não corrobora H01 nessa pequena amostra**, sem concluir ausência de ameaça; faltam atores, processo-pai e confirmação de criação efetiva da tarefa. A [Issue #9](https://github.com/raphaelguterres/threat-hunting-detection-lab/issues/9) mantém abertas a busca H01 ampliada, H02 e H03 com evidência nativa.

**Auditoria nativa de 02/11 — Windows Remote:** [PR #13](https://github.com/raphaelguterres/threat-hunting-detection-lab/pull/13) documenta consulta somente leitura de Windows Security/Sysmon e Wazuh FIM. Verificou **4698=0** com subcategoria de auditoria desabilitada; **1 criação de conta (4720)** sem logon 4624/4672 do mesmo SID nos 30 minutos seguintes; Sysmon ID 1 **≥2.000** (limite da consulta); **102 FIM históricos** do agente 004 e **nenhum** na janela recente, confirmada por consulta de controle. Isso identifica **lacunas e limites da amostra**, não confirma nem descarta incidentes. [Relatório técnico](https://github.com/raphaelguterres/threat-hunting-detection-lab/blob/main/docs/m1-native-windows-wazuh-visibility-review-20261102.md).

**Change control preparado (02/11):** a [Issue #15](https://github.com/raphaelguterres/threat-hunting-detection-lab/issues/15) e o [runbook técnico](https://github.com/raphaelguterres/threat-hunting-detection-lab/blob/main/docs/m1-change-control-4698-fim-agent004.md) registram auditoria 4698 **desativada**, Security de **20 MB**, WazuhSvc ativo e FIM 004 com **5 diretórios programados, 1 realtime e 23 entradas de registro**. Scripts privados de aprovação/rollback preparados, sem execução da alteração. A aprovação e a inspeção de precedência centralizada FIM continuam pendentes.

**Pré-check adicional em 02/11:** [PR #18](https://github.com/raphaelguterres/threat-hunting-detection-lab/pull/18) confirma log Security **Circular / 20 MB**, com **2 coletores eventchannel Security** locais (um filtrado). Foi identificada uma [diretiva FIM realtime central com caminho de formato Linux inexistente no WindowsServer](https://github.com/raphaelguterres/threat-hunting-detection-lab/issues/17). A origem no grupo do Manager e o efeito efetivo ainda não foram validados porque o Dashboard exigiu nova autenticação; **nenhuma configuração foi alterada**. Habilitação 4698 segue aguardando aprovação na Issue #15.

**Correção preventiva FIM preparada (02/11):** [PR #20](https://github.com/raphaelguterres/threat-hunting-detection-lab/pull/20) entregou [proposta de segregação por OS](https://github.com/raphaelguterres/threat-hunting-detection-lab/blob/main/docs/m1-fim-os-scoped-remediation-plan.md), validador offline e **15 testes novos em Windows/Linux**. O exemplo é sintético e não implantável. **Nenhum arquivo do Manager foi alterado**, e faltam inventário autorizado dos agentes do grupo `default`, aprovação, `verify-agent-conf` oficial e evidência operacional para concluir a [Issue #17](https://github.com/raphaelguterres/threat-hunting-detection-lab/issues/17).

**Controle de mudança reforçado (02/11):** o [PR #21](https://github.com/raphaelguterres/threat-hunting-detection-lab/pull/21) acrescentou comparação offline de **original x proposta** do `agent.conf`, com **21 testes sintéticos aprovados no Windows e Linux**. A ferramenta permite somente o escopo Linux nos blocos elegíveis, rejeitando mudanças de caminhos, fontes, atributos e comentários. **Validação oficial da proposta passou em staging isolado no Wazuh Manager** ([PR #23](https://github.com/raphaelguterres/threat-hunting-detection-lab/pull/23)): `verify-agent-conf` retornou OK, original permaneceu intacto e a cópia temporária foi excluída. **Sem deployment**: ainda faltam inventário autorizado, aprovação de aplicação, backup/rollback e aceite FIM real Windows/Linux.

Em 02/11, o M1 estava em andamento e a previsão para a etapa era de 35–60 horas. [Issue de acompanhamento](https://github.com/raphaelguterres/threat-hunting-detection-lab/issues/9)

</details>

### M2 — AppSec e DevSecOps · 65–110 h estimadas

O [Assessment AppSec](https://github.com/raphaelguterres/appsec-automatizado) tem acesso restrito. O [estudo público do formulário em homologação](https://github.com/raphaelguterres/cloudflare-429-edge-lab/blob/main/docs/evidencias.md) apresenta o ciclo de correção e regressão.

- [x] Modelagem de ameaças de aplicação própria e ambiente autorizado.
- [x] SAST, secret scanning, análise de dependências e SBOM no CI.
- [x] DAST com escopo restrito, orçamento de requisições e parada segura.
- [x] Dois ciclos evidenciados de achado → correção → teste de regressão.
- [ ] Runbook de escopo, triagem, priorização e comunicação técnica.

<!-- office:accepted-round M2 -->

**Rodada VELAR concluída e aceita em 24/11/2026.** O proprietário aceitou os nove passos executados no escritório VELAR. Após essa rodada, o trabalho seguiu para o M3.

| Evidência aceita | Resultado registrado |
| --- | --- |
| Modelagem de ameaças do formulário de avaliação | Mapa da entrada, fronteira visitante–API, verificação de consentimento em homologação e revisão do risco de envios repetidos. |
| Controle de CI e rastreabilidade de dependência | Etapa de verificação de segredos e arquivos sensíveis concluída com sucesso no CI do site. Next.js 16.4.6 do portal rastreado do manifesto e lockfile à entrada SPDX do SBOM. |
| Limites de validação | Homologação em loopback, dados fictícios, SQLite descartável, teto de 12 chamadas por sessão e parada para revisão definida. |
| Ciclo de correção e regressão | Worker temporário de homologação corrigido e retestado. O envio limitado retornou 429 sem gravação e um novo envio após a janela retornou 201. |
| Triagem | Etapa com entrada, critérios de decisão e evidência para revisão, aplicada ao caso de homologação. |

Os documentos de evidência e seus aceites estão no workspace do projeto VELAR. O checklist técnico acima continua sendo o registro dos critérios integrais da trilha. A rodada aceita cobriu um ciclo de correção e uma etapa do runbook. O runbook completo segue no checklist.

**Modelagem de ameaças revisada em 25/11/2026.** O escopo foi o formulário de avaliação da VELAR em homologação autorizada. O modelo aceito em 24/11 mapeia os dados e as fronteiras entre navegador, proxy, API e SQLite e registra as seis categorias do STRIDE. Nos ensaios com dados fictícios, a API recusou envios sem consentimento com HTTP 422 antes de gravar. A resposta HTTP 429 impediu a gravação de um envio repetido e um novo envio foi aceito após a janela. O e-mail autodeclarado e a evidência e retenção do consentimento continuam como pontos de acompanhamento. [Evidência sanitizada do limite e da recuperação em homologação](https://github.com/raphaelguterres/cloudflare-429-edge-lab/blob/0dc62ad9144971a9da30d4b246514fb74dfcbf0e/docs/evidencias.md#registro-sanitizado-da-rodada-final)

**DAST dirigido do formulário em 25/11/2026.** A validação HTTP ficou restrita à cópia da API do formulário em loopback, com dados fictícios, SQLite descartável, teto de 12 tentativas, uma requisição por vez e sem seguir redirecionamentos ou repetir chamadas automaticamente. A primeira conexão foi bloqueada antes de chegar à API. O roteiro seguinte tinha até dez requisições e deixou cinco registros fictícios. O Windows manteve um arquivo aberto durante o encerramento, e o log HTTP dessa rodada ficou indisponível. A integridade do SQLite foi conferida e a base foi removida.

Na checagem complementar, às 00h42 no horário de Brasília, o limitador foi preparado em memória na mesma revisão da API. Uma única chamada a `POST /api/lead` em `127.0.0.1:17891` recebeu `429 rate_limited` e encerrou o teste sem novas chamadas. O SQLite continuou com zero linhas e integridade `ok`. O serviço foi encerrado e a base removida. A revisão da API corresponde ao SHA-256 `0ae7e0d6f14d9a689e7fc23eb3b1d91d6c3be011c148a89ca09ba977ac8c600f`. [Evidência anterior de homologação](https://github.com/raphaelguterres/cloudflare-429-edge-lab/blob/0dc62ad9144971a9da30d4b246514fb74dfcbf0e/docs/evidencias.md#registro-sanitizado-da-rodada-final)

**Segundo ciclo em homologação em 25/11/2026.** O achado de severidade média era a confirmação indevida de envio diante de uma resposta HTTP 200 inesperada. A interface apagava os campos mesmo com zero registros. A correção preserva os dados até receber HTTP 201 com confirmação explícita no JSON. No Edge em loopback, respostas inesperadas simuladas preservaram os dados e a cópia local da API retornou HTTP 201 após gravar uma solicitação fictícia no SQLite descartável. O teste também confirmou o aviso de HTTP 429. Três dos cinco testes de regressão falhavam antes da correção e os cinco passaram depois. Este ciclo trata da confirmação no navegador. O primeiro ciclo tratou da correção no Worker de homologação. [PR da correção](https://github.com/raphaelguterres/velarcyber-website/pull/15) · [Testes de regressão](https://github.com/raphaelguterres/velarcyber-website/blob/44aec19b9f2b4fc2792460154b06cb922879623b/tests/lead-form.test.mjs)

**CI da VELAR em 25/11/2026.** No PR #14, a imagem do Nginx foi atualizada para 1.30.8-alpine-slim e fixada por digest. O Trivy passou sem achados corrigíveis de severidade alta ou crítica nas imagens verificadas. Semgrep, Gitleaks e o gate de DevSecOps também passaram. O PR segue em rascunho, sem merge e sem deploy. [Execução do Trivy](https://github.com/raphaelguterres/velarcyber-website/actions/runs/45535396819/job/138940633355) · [Gate de DevSecOps](https://github.com/raphaelguterres/velarcyber-website/actions/runs/45535396819)

**CI do Assessment em 25/11/2026.** No PR #1, o pip-audit auditou 36 pacotes do ambiente Python de build no runner Windows, sem pacotes ignorados e sem vulnerabilidades conhecidas encontradas. O SBOM CycloneDX 1.6 passou na validação e registrou 36 componentes do mesmo ambiente. A execução e o artefato são de acesso restrito. Os resultados da VELAR e do Assessment cobrem os quatro controles do critério de CI em execuções de pull request. [Execução do Assessment](https://github.com/raphaelguterres/appsec-automatizado/actions/runs/45539703820) · [Artefato de auditoria e SBOM](https://github.com/raphaelguterres/appsec-automatizado/actions/runs/45539703820/artifacts/14988009005)

### M3 — Incident Response & SOAR · 90–150 h estimadas

O resumo abaixo é público. Os links de código e relatórios deste laboratório exigem acesso ao repositório privado.

- [x] Criar repositório [incident-response-soar-lab](https://github.com/raphaelguterres/incident-response-soar-lab).
- [x] Modelo de caso, normalização de alertas e enriquecimento rastreável.
- [x] Triagem determinística com contexto e justificativa.
- [x] Playbooks em dry-run e aprovação humana para ações de resposta.
- [x] Testar falhas, repetição de eventos, rollback e trilha de auditoria.
- [x] Relatório final com métricas do **ambiente de laboratório**, sem confundir com produção.

<details>
<summary>Histórico da revisão inicial</summary>

**Registro de 24/11/2026.** Os seis passos da rodada M3 no escritório receberam aceite, incluindo a métrica de duplicação. O repositório privado reúne o README, as seis evidências e um protótipo local com dados sintéticos, triagem determinística, revisão humana, resposta em dry-run e auditoria. Sete testes locais passaram, incluindo duplicação, recusa, rollback de falha de auditoria e reabertura do SQLite. Nessa primeira rodada, a revisão técnica do marco ainda estava aberta. [README e evidências](https://github.com/raphaelguterres/incident-response-soar-lab/blob/c43b8b8b358e6416ddee09fbc8cb67bcf51970a1/README.md).

**Revisão inicial de 24/11/2026.** Os sete testes do commit c43b8b8 passaram em uma cópia local com fixtures sintéticas. A triagem determinística e o dry-run com decisão humana foram verificados. Naquele momento, o M3 ficou em revisão técnica. [Evidência da revisão](https://github.com/raphaelguterres/incident-response-soar-lab/blob/fd1a4fc612b972a141b2c03a5b29c8b5e462adff/docs/M3-REVISAO-TECNICA.md).

Pendências encontradas na revisão inicial, encerradas na revalidação abaixo:

1. Demonstrar a normalização de uma fixture bruta para os campos canônicos e testar a preservação do identificador e da fonte.
2. Sinalizar revisão pendente no caso ao receber uma entrega divergente depois do encaminhamento. A auditoria já registra a divergência. Falta refletir a pendência no caso e testar a preservação do encaminhamento original sem repeti-lo.
3. Reexecutar a suíte e atualizar o relatório final do laboratório com os resultados e os limites da amostra.

</details>

**M3 concluído em 24/11/2026.** Os 10 testes do commit 9a52ba9 passaram. A entrada bruta preserva identidade e origem e é convertida para o modelo canônico. Uma nova entrega divergente marca o caso como pendente de revisão e preserva o único encaminhamento anterior. O relatório apresenta os resultados, a métrica de duplicação e os limites do ensaio sintético. A próxima prioridade é M4. [Relatório final do laboratório](https://github.com/raphaelguterres/incident-response-soar-lab/blob/ff11f9bb0704c67d3c6a365323f0145364e59f15/docs/M3-REVISAO-TECNICA.md).

### M4 — Cloud Security e IaC · 110–180 h estimadas

- [x] Escolher AWS **ou** Azure e limitar orçamento/escopo. AWS Free Plan em Ohio (`us-east-2`), com limite de US$ 0 em cobranças.
- [x] Criar repositório [cloud-security-detection-lab](https://github.com/raphaelguterres/cloud-security-detection-lab) no GitHub. [README, template e evidências no commit publicado](https://github.com/raphaelguterres/cloud-security-detection-lab/commit/288a42b64fb2404f0ba23424847120a418b6b6ba).
- [x] Infraestrutura mínima reproduzível e removível por IaC. Criação e remoção em Ohio [verificadas e aceitas](https://github.com/raphaelguterres/cloud-security-detection-lab/blob/1304d94037e90db1179bc4f40baabc078213973c/docs/VALIDACAO-IAC-OHIO.md#aceite).
- [x] IAM de privilégio mínimo com verificação negativa. Leitura permitida e escrita negada na mesma sessão em Ohio, [aceitas pelo proprietário](https://github.com/raphaelguterres/cloud-security-detection-lab/blob/dd2ced0ebfb59da4a15867ec991c5682e52c2f01/docs/VALIDACAO-IAM-S3-OHIO.md#aceite).
- [x] Coletar eventos reais de gerenciamento do CloudTrail em Ohio. O detector identificou `PutBucketPublicAccessBlock`, `PutBucketPolicy` e `DeleteBucket` no mesmo bucket de teste. [Resultado e reprodução](https://github.com/raphaelguterres/cloud-security-detection-lab/blob/635e7e40b13012a4159c4ed1f19a1b4d820eed2b/docs/VALIDACAO-CLOUDTRAIL-S3-OHIO.md)
- [ ] Documentar custos, arquitetura, operação e teardown.

**Revisão de 24/11/2026.** Os seis passos documentais do escritório têm aceite, incluindo o procedimento de encerramento do bucket. O checklist técnico tem cinco de seis critérios concluídos. O README, o template do bucket privado e as [evidências sanitizadas](https://github.com/raphaelguterres/cloud-security-detection-lab/blob/288a42b64fb2404f0ba23424847120a418b6b6ba/docs/EVIDENCIAS-M4.md) estão publicados.

O proprietário aceitou o ciclo de criação e remoção em Ohio em 24/11/2026. A checagem das proteções em execução permaneceu inconclusiva. [Registro de aceite](https://github.com/raphaelguterres/cloud-security-detection-lab/blob/1304d94037e90db1179bc4f40baabc078213973c/docs/VALIDACAO-IAC-OHIO.md#aceite)

**Próxima prioridade no escritório · Infraestrutura.** Consolidar arquitetura, operação e remoção no relatório final. Vincular o inventário final ao recurso provisionado e conferir custos após a atualização do faturamento.

Para os próximos testes em nuvem, o escopo exige confirmar o plano gratuito, os recursos autorizados e o limite de US$ 0 em cobranças.

### Etapa avançada — somente após a base

- [ ] B1: detecção multissource, tuning e métricas — **110–170 h**.
- [ ] B2: engenharia de plataforma SOC e resiliência — **140–240 h**.
- [ ] B3: engenharia de infraestrutura segura — **140–230 h**.
- [ ] B4: ADRs, revisões técnicas, incident reviews e colaboração — **50–100 h**.

## Próximos 90 dias — sugestão adaptável

<details>
<summary>Plano original de novembro de 2026</summary>

| Período | Prioridade | Evidência de saída |
| --- | --- | --- |
| Semanas 1–2 | **M0 concluído:** conferência Discover, aceite da Fase 3 | Seis identidades verificadas nas três fontes, estudo de caso e Issue #4 atualizados |
| Semanas 3–6 | M1: três investigações e tuning | Estudos de caso, testes e cobertura atualizada |
| Semanas 7–11 | M2: AppSec/DevSecOps | Pipeline auditável, achados corrigidos, regressões reproduzíveis |
| Semanas 12–13 | Consolidar, revisar, documentar e planejar M3 | README, decisões, portfólio e backlog de resposta a incidentes |

**Nota:** as semanas são um plano inicial, não prazos assumidos. A carga total da Etapa A é maior que 90 dias a 15 h/semana; o cronograma acima **não promete concluí-la nesse intervalo**.

</details>

## Modelo de atualização semanal

Copie e preencha ao final de cada semana, em um PR ou issue do repositório correspondente:

```md
### Semana de AAAA-MM-DD

- Projeto / milestone:
- Horas reais registradas:
- Objetivo:
- Entregue:
- Testes e evidência pública sanitizada:
- Resultado: verified | partial | inconclusive | not_tested
- Limitação ou risco:
- Próxima ação:
```

## Regras de integridade de portfólio

1. Horas **estimadas** e horas **registradas** são medidas diferentes; não inventar controle de ponto retrospectivo.
2. CI verde, alertas em laboratório e incidentes reais são categorias distintas de evidência.
3. Nunca publicar credenciais, IPs internos relevantes, IDs brutos de eventos, artefatos sensíveis ou dados de clientes.
4. Priorizar poucos repositórios aprofundados, com arquitetura, testes, evidências e trade-offs verificáveis.
5. Atualizar o status somente depois de um resultado observável.

**Critério para a carreira:** candidatar-se progressivamente a SOC/Blue Team/AppSec conforme as competências demonstradas. **Senioridade é avaliada no contexto da função e experiência profissional, não pelo preenchimento deste checklist.**
