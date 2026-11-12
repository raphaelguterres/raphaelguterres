# Indisponibilidade do Indexer em um laboratório SOC

**Raphael Guterres · Exercício controlado com Wazuh e OpenSearch**

## Cenário

A visão operacional parou de responder durante uma interrupção planejada do Indexer. Investiguei quais componentes continuavam operando e se os marcadores emitidos durante a pausa ficariam consultáveis após a retomada.

## Investigação

| Camada | Evidência observada |
| --- | --- |
| Sonda externa | Uma checagem HTTPS no Windows, fora da VM do Kali, confirmou a indisponibilidade após dois timeouts consecutivos. |
| Fontes Linux | Duas fontes seguiram emitindo. Cada uma registrou um marcador no intervalo. |
| Manager | O processo do Wazuh Manager permaneceu em execução. |
| Indexer e verificador | Consultas e publicação de estado falharam enquanto o Indexer estava pausado. |

Pausei somente o Indexer. Comparei os registros de emissão com as consultas e retomei o componente. A sequência isolou a falha na camada de indexação neste exercício.

## Recuperação

| Medição | Resultado |
| --- | --- |
| Pausa controlada do Indexer | 75,593 s |
| Do primeiro timeout à confirmação na sonda | 4,017 s |
| Marcadores do intervalo consultáveis após a retomada | 2 de 2 |
| Da retomada à confirmação das duas fontes em estado normal | 5,736 s |

A resposta HTTPS confirmou que o endpoint voltou a responder. A consulta autenticada ao Indexer confirmou a recuperação dos dois eventos. Os relógios do Windows e do Kali estavam desalinhados, então cada duração usa medições de uma só máquina.

## Melhoria aplicada

A sonda passou a rodar como tarefa do Windows, com histórico local e registro de queda e recuperação independente do Indexer. O funcionamento da tarefa depende da sessão do Windows. O exercício mediu dois eventos de teste em uma única interrupção controlada.

[Voltar ao portfólio](../README.md)
