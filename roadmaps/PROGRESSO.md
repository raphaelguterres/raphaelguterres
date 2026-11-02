# Acompanhamento de progresso | SOC / Blue Team / Security Engineering

> **Última atualização:** 02/11/2026. Os checkboxes abaixo só mudam com evidência real. Esta página acompanha **projetos e competências**, não concede níveis profissionais.

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
| Incident Response & SOAR Lab | **Não iniciado** | Criar repositório próprio quando esta etapa começar |
| Cloud Security Detection Lab | **Não iniciado** | Criar repositório próprio quando esta etapa começar |

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

**M1 permanece em andamento:** [Issue #9](https://github.com/raphaelguterres/threat-hunting-detection-lab/issues/9). As 35–60 horas são previsão para o restante dessa etapa, não horas já registradas.

### M2 — AppSec e DevSecOps · 65–110 h estimadas

- [ ] Modelagem de ameaças de aplicação própria e ambiente autorizado.
- [ ] SAST, secret scanning, análise de dependências e SBOM no CI.
- [ ] DAST com escopo restrito, orçamento de requisições e parada segura.
- [ ] Dois ciclos evidenciados de achado → correção → teste de regressão.
- [ ] Runbook de escopo, triagem, priorização e comunicação técnica.

### M3 — Incident Response & SOAR · 90–150 h estimadas

- [ ] Criar repositório `incident-response-soar-lab` (ainda inexistente).
- [ ] Modelo de caso, normalização de alertas e enriquecimento rastreável.
- [ ] Triagem determinística com contexto e justificativa.
- [ ] Playbooks em dry-run e aprovação humana para ações de resposta.
- [ ] Testar falhas, repetição de eventos, rollback e trilha de auditoria.
- [ ] Relatório final com métricas do **ambiente de laboratório**, sem confundir com produção.

### M4 — Cloud Security e IaC · 110–180 h estimadas

- [ ] Escolher AWS **ou** Azure e limitar orçamento/escopo.
- [ ] Criar repositório `cloud-security-detection-lab` (ainda inexistente).
- [ ] Infraestrutura mínima reproduzível e removível por IaC.
- [ ] IAM de privilégio mínimo com verificação negativa.
- [ ] Coletar logs e construir três detecções com teste seguro.
- [ ] Documentar custos, arquitetura, operação e teardown.

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
