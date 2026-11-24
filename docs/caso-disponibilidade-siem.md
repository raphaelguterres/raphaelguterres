# Quando o SIEM parou de indexar

**Estudo de caso · SOC Telemetry Health Lab · Wazuh e OpenSearch**

Pausei o Indexer para responder a duas perguntas. Uma sonda fora da VM perceberia a interrupção? Depois da retomada, eu conseguiria localizar os eventos emitidos durante a pausa?

## Como isolei a falha

Pausei apenas o Indexer. No Windows, fora da VM do Kali, uma sonda HTTPS registrou dois timeouts consecutivos. Na VM, o processo do Wazuh Manager continuou em execução. As duas fontes Linux seguiram emitindo eventos e cada uma registrou um marcador durante a pausa.

Enquanto o Indexer esteve pausado, as consultas e a publicação de estado falharam. Comparei os registros das fontes com o resultado de uma consulta autenticada ao Indexer após a retomada. **Encontrei os dois marcadores.**

## O que medi

| Medição | Resultado |
| --- | ---: |
| Duração da pausa controlada do Indexer | 75,593 s |
| Do primeiro timeout à confirmação da queda pela sonda | 4,017 s |
| Da retomada à confirmação de estado normal nas duas fontes | 5,736 s |
| Marcadores da pausa encontrados na consulta | 2 de 2 |

Os relógios do Windows e do Kali estavam desalinhados. Calculei cada intervalo com registros de uma única máquina. O resultado cobre uma interrupção e dois eventos de teste.

## O que mudou

A sonda passou a rodar como tarefa do Windows. Ela guarda um histórico local de queda e recuperação que continua disponível quando o Indexer para de responder. A execução da tarefa depende da sessão do Windows.

[Voltar ao perfil](../README.md)
