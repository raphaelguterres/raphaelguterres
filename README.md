# Raphael Guterres

**Analista de cibersegurança · SOC e Blue Team**

Investigo eventos de Windows e Linux e escrevo regras de detecção para o Wazuh. Nos meus laboratórios, comparo os registros do endpoint com o que chega ao SIEM para explicar por que um alerta disparou e o que vale investigar.

## Projetos selecionados

**[AppSec na borda com Cloudflare](https://github.com/raphaelguterres/cloudflare-429-edge-lab)**<br>
Validei em homologação que o HTTP `429` do Worker bloqueou o envio antes da API e manteve o SQLite com duas linhas. Depois da janela, um novo envio gravou a terceira. [Evidências e diagnóstico do reteste](https://github.com/raphaelguterres/cloudflare-429-edge-lab/blob/main/docs/evidencias.md)

**[Threat Hunting & Detection Lab](https://github.com/raphaelguterres/threat-hunting-detection-lab)**<br>
Correlacionei eventos por usuário, sessão e arquivo em três investigações controladas. Usei controles negativos para verificar se eventos sem relação também apareceriam como um par. [Revisão das três hipóteses](https://github.com/raphaelguterres/threat-hunting-detection-lab/blob/59eeef6/docs/m1-final-review-20261110.md)

**[Cloud Security Detection Lab](https://github.com/raphaelguterres/cloud-security-detection-lab)**<br>
Testei privilégio mínimo na AWS com a mesma sessão IAM e o mesmo objeto S3. A leitura retornou HTTP `200` e a tentativa de sobrescrita retornou `403`. [Ensaio e estado do aceite](https://github.com/raphaelguterres/cloud-security-detection-lab/blob/main/docs/VALIDACAO-IAM-S3-OHIO.md)

**[Detection Engineering Blue Team](https://github.com/raphaelguterres/detection-engineering-blue-team)**<br>
Escrevi cinco regras Wazuh para Windows e rastreei seis alertas do Manager ao Discover, conferindo a identidade de cada evento nas três etapas do SIEM. [Relatório de validação](https://github.com/raphaelguterres/detection-engineering-blue-team/blob/main/docs/phase3-final-three-stage-six-event-acceptance-20261102.md)

**[Cybersecurity Roadmap BR](https://github.com/raphaelguterres/cybersecurity-roadmap-br)**<br>
Mantenho trilhas de cibersegurança e laboratórios em português para a comunidade brasileira. [Painel de estudos](https://raphaelguterres.github.io/cybersecurity-roadmap-br/)

## Quando o SIEM parou de indexar

Pausei o Indexer em um laboratório Wazuh. Uma sonda HTTPS fora da VM detectou a queda enquanto duas fontes Linux continuavam emitindo eventos. Após a retomada, encontrei **os dois marcadores gerados durante a pausa**.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/raphaelguterres/raphaelguterres/main/docs/img/tempos-indexer-escuro.png">
  <img src="https://raw.githubusercontent.com/raphaelguterres/raphaelguterres/main/docs/img/tempos-indexer-claro.png" width="540" alt="O Indexer ficou pausado por 75,593 s. Após a retomada, a confirmação de que as duas fontes estavam em estado normal levou 5,736 s.">
</picture>

[Ver a investigação e as medições](docs/caso-disponibilidade-siem.md)

## Formação

**Pós-graduação em Cibersegurança e Forense** · Em andamento<br>
**Defesa Cibernética** · Formação concluída

## Ferramentas na prática

- **Telemetria e investigação** — Sysmon e logs nativos de Windows Server e Linux para reconstruir sequências de eventos.
- **Detecção e busca** — Wazuh para escrever regras e OpenSearch para localizar os alertas indexados.
- **Automação de laboratório** — Python e PowerShell para coleta e testes, Docker para isolar serviços e GitHub Actions para executar regressões.
- **Segurança em nuvem** — AWS IAM e S3 para testar permissões e CloudFormation para criar e remover a infraestrutura.

## Trilha profissional

[Minha trilha profissional](roadmaps/ROADMAP_SOC_BLUE_TEAM_PLENO_SENIOR.md) · [Andamento dos laboratórios](roadmaps/PROGRESSO.md)
