# Roadmap profissional | Blue Team, Detection Engineering e Security Engineering

> **Trilha independente de evolução técnica** — iniciada em 02/11/2026. O objetivo é reunir evidências verificáveis de autonomia, engenharia, investigação, segurança e comunicação técnica. Este documento **não afirma** que um portfólio ou quantidade de horas concede senioridade, cargo ou experiência corporativa.

**Foco:** SOC / Blue Team → Detection Engineering → Incident Response / SOAR → Cloud Security → Security Engineering.

**Critério de progresso:** uma etapa só passa para **concluída** após implementação, teste, resultados reproduzíveis, análise de limitações e documentação. Itens futuros não devem aparecer como habilidades já comprovadas em currículo ou LinkedIn.

[Ver acompanhamento de entregas e evidências](PROGRESSO.md) · [Portfólio GitHub](https://github.com/raphaelguterres)

## Ponto de partida — projetos reais existentes

| Repositório | Competências demonstradas | Próximo incremento |
| --- | --- | --- |
| [Detection Engineering Blue Team](https://github.com/raphaelguterres/detection-engineering-blue-team) | Regras Wazuh, Sysmon, testes de regressão, CI e correlação de alertas | Confirmar os mesmos seis eventos no Discover e fechar a [Issue #4](https://github.com/raphaelguterres/detection-engineering-blue-team/issues/4) |
| [Threat Hunting & Detection Lab](https://github.com/raphaelguterres/threat-hunting-detection-lab) | Telemetria Windows/Linux, FIM, investigação documentada, MITRE ATT&CK | Evoluir hipóteses, cobertura, tuning e qualidade das investigações |
| [Assessment AppSec](https://github.com/raphaelguterres/appsec-automatizado) | Recon e avaliação de superfície **autorizada**, triagem, evidência e relatórios | Desenvolver pipeline AppSec com modelagem de ameaças, testes e acompanhamento de correções |

**Marco técnico já comprovado no Detection Engineering:** cinco regras customizadas, regressões documentadas e **6/6 correspondências exatas de identidade Manager → Indexer** (mesmo ID, regra, agente e timestamp UTC). **A confirmação independente dos mesmos documentos no Dashboard Discover ainda está pendente.** Não declarar a Fase 3 encerrada antes disso.

## Visão de esforço e prazos

As estimativas abaixo são **horas adicionais de trabalho prático**, não horas passadas rastreadas, nem critérios oficiais de contratação. Incluem planejamento, construção, troubleshooting, testes, evidências, documentação e revisão.

| Meta de portfólio | Horas adicionais acumuladas | Com 15 horas/semana |
| --- | ---: | ---: |
| Evidências competitivas para vagas de pleno | **308–515 h** | **~5–8 meses** |
| Projetos com complexidade e responsabilidades próximas de escopo sênior | **748–1.255 h** | **~12–19 meses** |

**Importante:** cargo de pleno/sênior depende também de experiências reais em equipes, serviços de produção, decisões sob risco, resultados mensuráveis, comunicação e autonomia. Projetos isolados não substituem esse histórico.

## Etapa A — Consolidar competências de pleno (308–515 h)

### A0. Fechamento do Detection Engineering Blue Team — 8–15 h

**Reutilizar:** [repositório operacional existente](https://github.com/raphaelguterres/detection-engineering-blue-team).

**Entregáveis:** prova de identidade dos seis documentos no Discover; aceitação formal por regra; última revisão de riscos, limitações e evidências sanitizadas; encerramento documentado da Issue #4 **somente após** validação.

**Critério de aceite:** mesmos campos \`id\`, \`rule.id\`, \`agent.id\`, timestamp UTC para todos os seis eventos nos três estágios. Sem gerar novas simulações desnecessárias, publicar IDs brutos, modificar credenciais ou enfraquecer TLS.

### A1. Threat Hunting orientado a hipóteses — 35–60 h

**Reutilizar:** [Threat Hunting & Detection Lab](https://github.com/raphaelguterres/threat-hunting-detection-lab).

**Entregáveis:** três novas investigações com hipótese, fonte de telemetria, linha do tempo, interpretação, alternativas benignas e resultado; matriz de cobertura ATT&CK; tuning de detecções e análise de falsos positivos.

**Critério de aceite:** cada caso deve permitir reproduzir a investigação em ambiente autorizado com procedimento, dado de teste seguro e limitações explícitas. Não tratar cenários simulados como incidentes reais.

### A2. AppSec e DevSecOps verificáveis — 65–110 h

**Reutilizar:** [Assessment AppSec](https://github.com/raphaelguterres/appsec-automatizado).

**Entregáveis:** modelagem de ameaças de aplicação controlada; revisão de autenticação, autorização e validação de entradas; análise de dependências/SBOM; pipeline SAST, secret scanning e DAST em ambiente permitido; matriz achado → correção → regressão.

**Critério de aceite:** cada achado possui severidade justificada, reprodução segura, evidência de correção e teste que evita regressão. Nenhum alvo externo sem autorização.

### A3. Incident Response & SOAR Lab — 90–150 h

**Novo projeto proposto**, ainda não criado: \`incident-response-soar-lab\`.

**Entregáveis:** fluxo alerta → enriquecimento → classificação → caso → decisão; playbooks de contenção com aprovação humana; ações em **dry-run** por padrão; trilha de auditoria; validação de rollback, duplicatas, timeout e falhas de integração.

**Critério de aceite:** casos demonstram triagem consistente, decisões explicáveis e nenhuma contenção destrutiva automática. Testes negativos e logs sanitizados fazem parte do repositório.

### A4. Cloud Security Detection Lab — 110–180 h

**Novo projeto proposto**, ainda não criado: \`cloud-security-detection-lab\`.

**Entregáveis:** escolher **uma** nuvem primeiro (AWS ou Azure); infraestrutura reprodutível por IaC; IAM de privilégio mínimo; logs centralizados; três detecções; procedimento de investigação e remoção de recursos; estimativa de custo e limites de segurança.

**Critério de aceite:** ambiente isolado, sem recursos pagos inesperados ou segredos versionados; auditoria de mudanças, testes e teardown documentados.

**Subtotal da Etapa A: 308–515 h adicionais.**

## Etapa B — Demonstrar escopo técnico avançado (mais 440–740 h)

> Iniciar depois de consolidar fundamentos e buscar contato com trabalho real, code review de terceiros e responsabilidade operacional.

| Frente | Horas adicionais | Entregável de arquitetura e operação |
| --- | ---: | --- |
| B1. Detection Engineering avançado | 110–170 h | Múltiplas fontes, tuning mensurável, cobertura, testes contra falsos positivos e avaliação de degradação |
| B2. SOC Platform Engineering | 140–240 h | Ingestão resiliente, filas, auditoria, observabilidade, SLOs de laboratório, recuperação e métricas |
| B3. Security Infrastructure Engineering | 140–230 h | IaC segura, hardening, backup/restore testado, identidade e segredos, threat modeling e rollback |
| B4. Decisões arquiteturais e mentoria | 50–100 h | ADRs, revisão técnica de terceiros, comunicação de trade-offs, incident review e documentação operacional |

**Subtotal da Etapa B: 440–740 h. Acumulado desde agora: 748–1.255 h.**

Essas entregas exercitam atribuições frequentemente associadas a profissionais experientes. **Nenhum número de commits, repositórios ou horas, isoladamente, comprova senioridade.**

## Agenda sustentável de 15 h/semana

| Atividade | Horas/semana |
| --- | ---: |
| Construção / automação | 5 |
| Testes e investigação | 4 |
| Validação de evidências e análise de resultados | 3 |
| Documentação e atualização do GitHub | 2 |
| Revisão de prioridades e aprendizado | 1 |
| **Total** | **15** |

Ritmo sugerido: **uma entrega verificável por semana** e **uma revisão de escopo por mês**, em vez de abrir muitos repositórios simultâneos. Ajustar carga diante de pausas, trabalho e estudo.

## Padrão mínimo de qualidade de cada repositório

- [ ] README com objetivo, arquitetura, premissas e limites.
- [ ] Testes automatizados ou roteiro de validação reproduzível, com resultado documentado.
- [ ] Evidência sanitizada de execução real quando alegada; simulação marcada como simulação.
- [ ] Controles de escopo, credenciais e dados sensíveis.
- [ ] Registro de erros, hipóteses e decisões (incluindo o que **não** foi comprovado).
- [ ] Runbook operacional, plano de rollback e limpeza de recursos.
- [ ] CI e revisão antes de incorporar mudanças relevantes.
- [ ] Estudo de caso curto para recrutadores **e** aprofundamento técnico para especialistas.

## Como avaliar progresso profissional sem superestimar o nível

**Prontidão para vagas pleno:** explicar o raciocínio técnico, operar o laboratório com autonomia, investigar alertas ambíguos, corrigir defeitos, validar resultados e comunicar risco com evidência.

**Escopo sênior:** além do anterior, mostrar decisões arquiteturais, trade-offs de confiabilidade/custo/segurança, liderança técnica, resposta sob pressão, melhoria de processos e resultados em colaboração com equipes reais.

**Métricas úteis:** tempo de detecção **em ensaios controlados**, falsos positivos nos conjuntos de teste, cobertura validada, tempo de recuperação demonstrado, regressões evitadas e decisões registradas. Não atribuir essas métricas à produção quando foram obtidas somente em laboratório.

## Referências

- [NIST NICE Workforce Framework](https://www.nist.gov/itl/applied-cybersecurity/nice/nice-framework-resource-center) — conhecimentos, habilidades e tarefas de cibersegurança.
- [MITRE ATT&CK](https://attack.mitre.org/) — linguagem comum para hipóteses e técnicas.
- [NIST SP 800-61](https://csrc.nist.gov/pubs/sp/800/61/r3/final) — gestão e resposta a incidentes.
- [NIST SSDF SP 800-218](https://csrc.nist.gov/pubs/sp/800/218/final) — desenvolvimento seguro.

---

**Regra principal:** *profundidade, evidência e autonomia antes de quantidade de repositórios*. O roadmap é um instrumento de planejamento, não uma declaração de nível profissional.
