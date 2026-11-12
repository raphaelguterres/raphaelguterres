# Raphael Guterres

**Analista de Cibersegurança · SOC · Blue Team · Detection Engineering**

Trabalho com engenharia de detecção e investigação em ambientes Windows e Linux. Meus projetos mostram o caminho da telemetria até a decisão de triagem, com regras versionadas, controles negativos e evidências reproduzíveis.

## Projetos

| Projeto | O que você pode revisar |
| --- | --- |
| **Threat Hunting & Detection Lab** | Projeto principal. Hipóteses de investigação, arquitetura Wazuh, linhas do tempo e decisões de triagem. [Repositório](https://github.com/raphaelguterres/threat-hunting-detection-lab) |
| **Detection Engineering Blue Team** | Cinco regras Wazuh para Windows, catálogo MITRE ATT&CK e testes automatizados de detecção. [Repositório](https://github.com/raphaelguterres/detection-engineering-blue-team) |
| **SOC Telemetry Health Lab** | Estudo de caso público sobre detecção externa de indisponibilidade, isolamento da falha e validação da recuperação. [Estudo de caso](docs/caso-disponibilidade-siem.md) |
| **Cybersecurity Roadmap BR** | Projeto open source com trilhas de estudo, laboratórios guiados e recursos para a comunidade brasileira. [Repositório](https://github.com/raphaelguterres/cybersecurity-roadmap-br) · [Dashboard](https://raphaelguterres.github.io/cybersecurity-roadmap-br/) |

## Caso em destaque · Indisponibilidade do Indexer

Em um exercício controlado, pausei o Indexer e confirmei a falha com uma sonda HTTPS fora da VM. O Manager e as fontes Linux continuaram operando. Na retomada, localizei **2 de 2 marcadores** do intervalo e confirmei o retorno das duas fontes a estado normal em **5,736 s**. [Investigação, medições e melhoria aplicada](docs/caso-disponibilidade-siem.md)

## Formação e ferramentas

Formado em Defesa Cibernética. Pós-graduação em Cibersegurança e Forense em andamento.

Wazuh · OpenSearch · Sysmon · Windows Server · Linux · Python · PowerShell · Docker · GitHub Actions
