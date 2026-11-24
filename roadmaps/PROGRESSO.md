# Acompanhamento de progresso | SOC / Blue Team / Security Engineering

> **Última atualização:** 24/11/2026. Os checkboxes abaixo só mudam com evidência real. Esta página acompanha **projetos e competências**, não concede níveis profissionais.

[Roadmap completo e estimativas de horas](ROADMAP_SOC_BLUE_TEAM_PLENO_SENIOR.md)

## Situação atual

| Marco | Situação | Evidência |
| --- | --- | --- |
| Laboratório Wazuh com agentes e detecções | **Validado** | [Detection Engineering Blue Team](https://github.com/raphaelguterres/detection-engineering-blue-team) |
| Cinco regras customizadas e regressões versionadas | **Validado** | [README técnico](https://github.com/raphaelguterres/detection-engineering-blue-team#estado-da-fase-3) |
| Manager → Indexer, mesma identidade original | **6/6 concluído** | [Relatório sanitizado](https://github.com/raphaelguterres/detection-engineering-blue-team/blob/main/docs/phase3-manager-indexer-exact-correlation-20261102.md) |
| Manager → Indexer → Discover, mesma identidade original | **6/6 concluído — 5/5 regras** | [Aceite operacional](https://github.com/raphaelguterres/detection-engineering-blue-team/blob/main/docs/phase3-final-three-stage-six-event-acceptance-20261102.md) |
| Threat Hunting Lab | **Projeto existente; aprofundamento planejado** | [Repositório](https://github.com/raphaelguterres/threat-hunting-detection-lab) |
| Assessment AppSec | **Projeto existente; integração DevSecOps planejada** | [Repositório](https://github.com/raphaelguterres/appsec-automatizado) |
| Incident Response & SOAR Lab | **Validado em laboratório** | [Relatório final](https://github.com/raphaelguterres/incident-response-soar-lab/blob/ff11f9bb0704c67d3c6a365323f0145364e59f15/docs/M3-REVISAO-TECNICA.md) |
| Cloud Security Detection Lab | **Em andamento** | AWS Free Plan em Ohio, escopo aceito e [repositório publicado](https://github.com/raphaelguterres/cloud-security-detection-lab) |

**Escritório VELAR · 3 de 5 marcos concluídos.** M0, M1 e M3 concluídos. Rodada VELAR do M2 aceita, com checklist técnico aberto. M4 em foco na área de Infraestrutura.

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

### M1 — Threat Hunting e investigação · 35–60 h estimadas

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

**M1 permanece em andamento:** [Issue #9](https://github.com/raphaelguterres/threat-hunting-detection-lab/issues/9). As 35–60 horas são previsão para o restante dessa etapa, não horas já registradas.

### M2 — AppSec e DevSecOps · 65–110 h estimadas

- [ ] Modelagem de ameaças de aplicação própria e ambiente autorizado.
- [ ] SAST, secret scanning, análise de dependências e SBOM no CI.
- [ ] DAST com escopo restrito, orçamento de requisições e parada segura.
- [ ] Dois ciclos evidenciados de achado → correção → teste de regressão.
- [ ] Runbook de escopo, triagem, priorização e comunicação técnica.

<!-- office:accepted-round M2 -->

**Rodada VELAR concluída e aceita em 24/11/2026.** O proprietário aceitou os nove passos executados no escritório VELAR. A próxima prioridade operacional é M3.

| Evidência aceita | Resultado registrado |
| --- | --- |
| Modelagem de ameaças do formulário de avaliação | Mapa da entrada, fronteira visitante–API, verificação de consentimento em homologação e revisão do risco de envios repetidos. |
| Controle de CI e rastreabilidade de dependência | Etapa de verificação de segredos e arquivos sensíveis concluída com sucesso no CI do site. Next.js 16.4.6 do portal rastreado do manifesto e lockfile à entrada SPDX do SBOM. |
| Limites de validação | Homologação em loopback, dados fictícios, SQLite descartável, teto de 12 chamadas por sessão e parada para revisão definida. |
| Ciclo de correção e regressão | Worker temporário de homologação corrigido e retestado. O envio limitado retornou 429 sem gravação e um novo envio após a janela retornou 201. |
| Triagem | Etapa com entrada, critérios de decisão e evidência para revisão, aplicada ao caso de homologação. |

Os documentos de evidência e seus aceites estão no workspace do projeto VELAR. O checklist técnico acima continua sendo o registro dos critérios integrais da trilha. A rodada aceita cobriu um ciclo de correção e uma etapa do runbook. A cobertura de CI auditável, o DAST da trilha, o segundo ciclo independente e o runbook completo seguem no checklist.

### M3 — Incident Response & SOAR · 90–150 h estimadas

- [x] Criar repositório [incident-response-soar-lab](https://github.com/raphaelguterres/incident-response-soar-lab).
- [x] Modelo de caso, normalização de alertas e enriquecimento rastreável.
- [x] Triagem determinística com contexto e justificativa.
- [x] Playbooks em dry-run e aprovação humana para ações de resposta.
- [x] Testar falhas, repetição de eventos, rollback e trilha de auditoria.
- [x] Relatório final com métricas do **ambiente de laboratório**, sem confundir com produção.

**Registro de 24/11/2026.** Os seis passos da rodada M3 no escritório receberam aceite, incluindo a métrica de duplicação. O repositório privado reúne o README, as seis evidências e um protótipo local com dados sintéticos, triagem determinística, revisão humana, resposta em dry-run e auditoria. Sete testes locais passaram, incluindo duplicação, recusa, rollback de falha de auditoria e reabertura do SQLite. A revisão técnica do marco segue pelo checklist acima. [README e evidências](https://github.com/raphaelguterres/incident-response-soar-lab/blob/c43b8b8b358e6416ddee09fbc8cb67bcf51970a1/README.md).

**Revisão inicial de 24/11/2026.** Os sete testes do commit c43b8b8 passaram em uma cópia local com fixtures sintéticas. A triagem determinística e o dry-run com decisão humana foram verificados. Naquele momento, o M3 ficou em revisão técnica. [Evidência da revisão](https://github.com/raphaelguterres/incident-response-soar-lab/blob/fd1a4fc612b972a141b2c03a5b29c8b5e462adff/docs/M3-REVISAO-TECNICA.md).

Pendências encontradas na revisão inicial, encerradas na revalidação abaixo:

1. Demonstrar a normalização de uma fixture bruta para os campos canônicos e testar a preservação do identificador e da fonte.
2. Sinalizar revisão pendente no caso ao receber uma entrega divergente depois do encaminhamento. A auditoria já registra a divergência. Falta refletir a pendência no caso e testar a preservação do encaminhamento original sem repeti-lo.
3. Reexecutar a suíte e atualizar o relatório final do laboratório com os resultados e os limites da amostra.

**M3 concluído em 24/11/2026.** Os 10 testes do commit 9a52ba9 passaram. A entrada bruta preserva identidade e origem e é convertida para o modelo canônico. Uma nova entrega divergente marca o caso como pendente de revisão e preserva o único encaminhamento anterior. O relatório apresenta os resultados, a métrica de duplicação e os limites do ensaio sintético. A próxima prioridade é M4. [Relatório final do laboratório](https://github.com/raphaelguterres/incident-response-soar-lab/blob/ff11f9bb0704c67d3c6a365323f0145364e59f15/docs/M3-REVISAO-TECNICA.md).

### M4 — Cloud Security e IaC · 110–180 h estimadas

- [x] Escolher AWS **ou** Azure e limitar orçamento/escopo. AWS Free Plan em Ohio (`us-east-2`), com limite de US$ 0 em cobranças.
- [x] Criar repositório [cloud-security-detection-lab](https://github.com/raphaelguterres/cloud-security-detection-lab) no GitHub. [README, template e evidências no commit publicado](https://github.com/raphaelguterres/cloud-security-detection-lab/commit/288a42b64fb2404f0ba23424847120a418b6b6ba).
- [ ] Infraestrutura mínima reproduzível e removível por IaC. Ciclo em Ohio verificado, aguardando aceite.
- [ ] IAM de privilégio mínimo com verificação negativa.
- [ ] Coletar logs e construir três detecções com teste seguro.
- [ ] Documentar custos, arquitetura, operação e teardown.

**Revisão de 24/11/2026.** Os seis passos documentais do escritório têm aceite, incluindo o procedimento de encerramento do bucket. O checklist técnico tem dois de seis critérios concluídos. O README, o template do bucket privado e as [evidências sanitizadas](https://github.com/raphaelguterres/cloud-security-detection-lab/blob/288a42b64fb2404f0ba23424847120a418b6b6ba/docs/EVIDENCIAS-M4.md) estão publicados.

1. **Próxima prioridade no escritório · Infraestrutura.** Revisar e aceitar a evidência de criação e remoção do mesmo bucket em Ohio. [Registro sanitizado](https://github.com/raphaelguterres/cloud-security-detection-lab/blob/e9140cd63498b63211bca0a712510debccc1f13c/docs/VALIDACAO-IAC-OHIO.md#aceite)
2. Demonstrar leitura permitida e escrita negada para a mesma identidade IAM.
3. Complementar o sinal `PutBucketPolicy`, já testado com entradas fictícias, com duas detecções adicionais. Validar as três com eventos reais de gerenciamento e testes seguros, mantendo o bloqueio de acesso público.
4. Consolidar arquitetura, operação e remoção no relatório final. Vincular o inventário final ao recurso provisionado e conferir custos após a atualização do faturamento.

A revisão e a publicação foram feitas fora da AWS. O ensaio em nuvem depende de confirmar o Free Plan ativo, os recursos autorizados e o limite de US$ 0 em cobranças.

### Etapa avançada — somente após a base

- [ ] B1: detecção multissource, tuning e métricas — **110–170 h**.
- [ ] B2: engenharia de plataforma SOC e resiliência — **140–240 h**.
- [ ] B3: engenharia de infraestrutura segura — **140–230 h**.
- [ ] B4: ADRs, revisões técnicas, incident reviews e colaboração — **50–100 h**.

## Próximos 90 dias — sugestão adaptável

| Período | Prioridade | Evidência de saída |
| --- | --- | --- |
| Semanas 1–2 | **M0 concluído:** conferência Discover, aceite da Fase 3 | Seis identidades verificadas nas três fontes, estudo de caso e Issue #4 atualizados |
| Semanas 3–6 | M1: três investigações e tuning | Estudos de caso, testes e cobertura atualizada |
| Semanas 7–11 | M2: AppSec/DevSecOps | Pipeline auditável, achados corrigidos, regressões reproduzíveis |
| Semanas 12–13 | Consolidar, revisar, documentar e planejar M3 | README, decisões, portfólio e backlog de resposta a incidentes |

**Nota:** as semanas são um plano inicial, não prazos assumidos. A carga total da Etapa A é maior que 90 dias a 15 h/semana; o cronograma acima **não promete concluí-la nesse intervalo**.

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
