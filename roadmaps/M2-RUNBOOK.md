# Runbook de AppSec · Formulário de avaliação da VELAR

**Revisado em 25/11/2026** · Escopo de homologação

Use este runbook para decidir se um relato sobre o formulário é um controle esperado, um desvio confirmado ou um caso que ainda precisa de evidência.

## 1. Escopo e parada segura

- Confirme o responsável, a revisão da aplicação, o ambiente e o objetivo antes de testar. O ambiente autorizado para novos ensaios é a cópia em loopback, com endereços fictícios de `example.test` e SQLite descartável.
- Limite o ensaio aos recursos locais do formulário, à saúde da API e a `POST /api/lead`. Conte todas as chamadas, inclusive as que falham. Use até **12 por sessão**, no máximo uma por segundo e uma em andamento. Desative o seguimento de redirecionamentos e as retentativas automáticas.
- Pare ao concluir os casos ou atingir o teto. Pare imediatamente se houver HTTP 429, 5xx, timeout, resposta ou gravação inesperada, redirecionamento, destino fora do loopback ou sinais de dados reais na base. Registre a última tentativa e preserve a evidência sanitizada disponível.
- Se houver dúvida sobre autorização, impacto fora de homologação ou dados reais, encaminhe ao responsável pelo ambiente. Uma nova sessão após um desvio requer revisão da causa e confirmação do escopo pelo responsável. Evidências históricas de homologação podem ser revisadas sem reexecutar o ensaio.

## 2. Triagem

Registre a revisão, data e fuso, rota, camada que respondeu, resultado esperado e observado, impacto, contagem de requisições e referência da evidência. Use o mesmo identificador sanitizado para correlacionar as fontes quando disponível.

| Decisão | Evidência mínima | Ação |
| --- | --- | --- |
| Fora do escopo ou ambiente incerto | Endereço ou revisão diverge da autorização, ou surgem dados reais | Pare e encaminhe ao responsável pelo ambiente. Preserve somente os metadados necessários. |
| Controle esperado | A camada correta aplicou a proteção e as contagens confirmam seu efeito. A recuperação é avaliada com evidência já disponível quando fizer parte do critério | Registre a decisão e encerre o relato com o motivo e as referências. |
| Desvio confirmado | Divergência reproduzida em ambiente autorizado, com impacto observado e evidência suficiente | Registre severidade, confiança e prioridade. Atribua a correção à área de Aplicações ou de Infraestrutura, conforme a camada. |
| Evidência insuficiente | A origem da resposta ou o efeito no SQLite continua indeterminado | Registre o dado faltante, quem o pode obter e o próximo ponto de revisão. Mantenha o caso pendente. |

Para limite de envio, cruze a resposta HTTP, o registro da camada que respondeu e as contagens da API e do SQLite. Para confirmação no navegador, compare a mensagem exibida, a preservação dos campos e a gravação observada. Mantenha a distinção entre resposta simulada e resposta real da API local.

## 3. Priorização

Descreva o impacto observado e a confiança na evidência separadamente da urgência de tratar o caso. Reavalie a prioridade quando o alcance ou a evidência mudar.

| Prioridade | Quando usar | Encaminhamento |
| --- | --- | --- |
| P0 · imediata | Indício plausível de exposição de dados reais ou impacto grave em serviço de produção | Interrompa o ensaio e alerte o responsável pelo ambiente e Segurança/IR pelo canal interno. |
| P1 · alta | Desvio grave confirmado com alcance relevante, como aceitação indevida de dados ou falha ampla de um controle | Encaminhe ao responsável técnico na triagem e combine a próxima atualização. |
| P2 · normal | Falha confirmada e limitada à homologação, com impacto concreto no fluxo avaliado | Abra tarefa para a área responsável, vincule a correção e faça o reteste antes de encerrar. |
| P3 · acompanhamento | Desvio de baixo impacto ou evidência insuficiente, sem indício de impacto relevante | Atribua responsável e um ponto de revisão para completar a análise. |

Um controle esperado recebe o estado **encerrado como comportamento esperado**. A falta de evidência por si só não reduz a prioridade quando houver sinal de impacto grave.

## 4. Comunicação técnica e encerramento

Use o canal interno para registrar o caso e o PR ou ticket para vincular a correção. Use um resumo sanitizado em documentos públicos. Remova dados pessoais, credenciais, endereços internos e identificadores brutos.

~~~text
Caso e estado
Ambiente, revisão, data e fuso
Resultado esperado e observado
Impacto, severidade, confiança e prioridade
Evidências, incluindo status HTTP e contagens quando aplicáveis
Parada aplicada ou decisão de continuar
Responsável, próxima ação e próximo ponto de revisão
Teste de regressão e resultado
~~~

Feche um controle esperado quando a evidência sustentar a decisão. Para um desvio, registre a correção, o resultado antes e depois e pelo menos um caso válido que continuou funcionando. Se faltar evidência, mantenha o caso pendente com o responsável indicado. Registre o encerramento técnico de homologação separadamente da aprovação para implantação.

## Validação do runbook

Revisão de mesa em 25/11/2026 com evidências já coletadas. As mensagens abaixo são exemplos internos de registro.

| Caso | Evidência cruzada | Decisão e comunicação registrada na revisão |
| --- | --- | --- |
| Limite aplicado pelo Worker de homologação | HTTP 429 do Worker. API e SQLite mantiveram duas ocorrências. O envio bloqueado ficou ausente das duas fontes. A evidência histórica de recuperação mostrou HTTP 201 e três ocorrências | **Controle esperado, encerrado.** “O Worker bloqueou o envio sem encaminhar nem gravar. A recuperação consta do ensaio histórico. A triagem pode ser encerrada.” |
| Confirmação indevida no navegador | No ensaio anterior à correção, HTTP 200 simulado mostrou sucesso com zero registros. Após a correção, a interface preservou os campos. Um HTTP 201 da API local gravou uma linha. Cinco testes de regressão passaram | **Desvio confirmado, severidade média, confiança alta, P2.** “Aplicações, a interface confirmava um envio sem gravação em homologação. A correção do PR #15 passou no reteste local. Encerramento técnico em homologação registrado.” |
| Fixture de mesa com HTTP 429 sem registros da API e do banco | O status, isoladamente, não comprova onde ocorreu o bloqueio nem se houve gravação | **Evidência insuficiente, P3 no cenário simulado.** “Aplicações, mantenha o caso pendente até obter a camada que respondeu e as contagens da API e do SQLite.” |
| Fixture de mesa com ambiente não confirmado | O destino da validação não foi confirmado como loopback | **Fora do escopo, parada imediata.** “Responsável pelo ambiente, confirme o escopo autorizado antes de qualquer nova requisição.” |

Evidências revisadas. [Reteste do Worker em homologação](https://github.com/raphaelguterres/cloudflare-429-edge-lab/blob/0dc62ad9144971a9da30d4b246514fb74dfcbf0e/docs/evidencias.md#registro-sanitizado-da-rodada-final) · [Correção e regressão do formulário](https://github.com/raphaelguterres/velarcyber-website/pull/15)
