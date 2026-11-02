# Acompanhamento de progresso | SOC / Blue Team / Security Engineering

> **Última atualização:** 02/11/2026. Os checkboxes abaixo só mudam com evidência real. Esta página acompanha **projetos e competências**, não concede níveis profissionais.

[Roadmap completo e estimativas de horas](ROADMAP_SOC_BLUE_TEAM_PLENO_SENIOR.md)

## Situação atual

| Marco | Situação | Evidência |
| --- | --- | --- |
| Laboratório Wazuh com agentes e detecções | **Validado** | [Detection Engineering Blue Team](https://github.com/raphaelguterres/detection-engineering-blue-team) |
| Cinco regras customizadas e regressões versionadas | **Validado** | [README técnico](https://github.com/raphaelguterres/detection-engineering-blue-team#estado-da-fase-3) |
| Manager → Indexer, mesma identidade original | **6/6 concluído** | [Relatório sanitizado](https://github.com/raphaelguterres/detection-engineering-blue-team/blob/main/docs/phase3-manager-indexer-exact-correlation-20261102.md) |
| Indexer → interface Discover, mesmos seis documentos | **Pendente** | [Issue #4](https://github.com/raphaelguterres/detection-engineering-blue-team/issues/4) |
| Threat Hunting Lab | **Projeto existente; aprofundamento planejado** | [Repositório](https://github.com/raphaelguterres/threat-hunting-detection-lab) |
| Assessment AppSec | **Projeto existente; integração DevSecOps planejada** | [Repositório](https://github.com/raphaelguterres/appsec-automatizado) |
| Incident Response & SOAR Lab | **Não iniciado** | Criar repositório próprio quando esta etapa começar |
| Cloud Security Detection Lab | **Não iniciado** | Criar repositório próprio quando esta etapa começar |

## Checklist de milestones

### M0 — Encerrar Fase 3 de Detection Engineering · 8–15 h estimadas

- [x] Criar e testar cinco regras de detecção customizadas.
- [x] Correlacionar seis eventos originais Manager → Indexer por ID, regra, agente e timestamp UTC.
- [x] Preparar verificador offline e testes para três fontes independentes — [PR #28 aprovado](https://github.com/raphaelguterres/detection-engineering-blue-team/pull/28).
- [ ] **Exportar CSV diretamente da interface Discover** (não Dev Tools), salvar em `.lab/phase3-discover.csv` e executar `scripts/phase3-verify-discover.bat` conforme [procedimento de aceite](https://github.com/raphaelguterres/detection-engineering-blue-team/blob/main/docs/phase3-discover-csv-acceptance.md).
- [ ] Conferir os **mesmos seis eventos** em **Dashboard Discover**, independentemente do Console/Dev Tools, com `id`, `rule.id`, `agent.id` e timestamp UTC, e atestar a origem do CSV.
- [ ] Documentar aceite por regra sem IDs brutos e registrar conclusão na Issue #4.
- [ ] Revisar o estudo de caso e deixar explícitos escopo, resultado e limitações.

**Gate:** 6/6 no Discover com a mesma identidade. Até lá, Fase 3 **não** está formalmente concluída.

### M1 — Threat Hunting e investigação · 35–60 h estimadas

- [ ] Planejar três hipóteses novas e definir telemetria mínima.
- [ ] Construir três timelines de casos controlados e registrar hipóteses alternativas.
- [ ] Demonstrar revisão de falsos positivos ou controles negativos.
- [ ] Atualizar cobertura MITRE ATT&CK com lacunas e limitações.
- [ ] Publicar estudos de caso sanitizados e CI verde.

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
| Semanas 1–2 | M0: conferência Discover, aceite da Fase 3 | Issue #4 fechada **somente com evidência**; estudo de caso atualizado |
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
