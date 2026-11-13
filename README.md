# Sistema Especialista de Triagem e Priorização de Problemas Urbanos

Projeto avaliativo desenvolvido para a disciplina de **Lógica para Ciência da Computação** (UNIVASF), utilizando programação em lógica com **Prolog**.

## 1. Situação-Problema e Escopo
As administrações municipais recebem diariamente diversas demandas sobre infraestrutura urbana (pavimentação, iluminação pública, trânsito, saneamento). Sem critérios lógicos padronizados, ocorrências graves em locais sensíveis podem competir na mesma fila de espera que reparos estéticos de baixa urgência.

Este projeto consiste em um **protótipo de sistema de apoio à decisão municipal** em Prolog. A partir de uma base de conhecimento estática contendo localidades, categorias de problemas, capacidade operacional das secretarias e chamados registrados, o motor de inferência realiza:
1. **Identificação do chamado** e mapeamento da localidade exata.
2. **Avaliação de risco** (severidade técnica, proximidade a pontos críticos e pressão popular).
3. **Direcionamento setorial** (identificação da secretaria responsável).
4. **Classificação hierárquica de prioridade** (`emergencia`, `alta`, `media`, `baixa`) com exclusão mútua.
5. **Análise de viabilidade operacional** (checagem individual de equipe disponível e orçamento estimado) e diagnóstico de bloqueios.

> **Delimitação de Escopo:** A verificação orçamentária avalia a viabilidade de cada chamado de forma individual e estática frente ao saldo disponível da secretaria responsável, não realizando dedução dinâmica de saldo em tempo de execução.

## 2. Arquitetura da Base de Conhecimento (Fatos)
* `local_urbano(IdLocal, Bairro, TipoVia, PontoCriticoProximo)`
* `tipo_problema(Problema, Categoria, SeveridadeBase, CustoEstimado)`
* `secretaria(IdSecretaria, OrcamentoDisponivel, EquipeDisponivel)`
* `atende_categoria(IdSecretaria, Categoria)`
* `chamado(IdChamado, Problema, IdLocal, TurnoAfetado, RelatosPopulares)`

## 3. Regras Lógicas Planejadas
1. `secretaria_responsavel(IdChamado, Secretaria)`: Relaciona o chamado à secretaria que atende sua categoria.
2. `risco_seguranca_publica(IdChamado)`: Identifica risco iminente (ex: falha de iluminação noturna, semáforo inoperante em qualquer turno ou ocorrência em ponto crítico).
3. `alta_pressao_popular(IdChamado)`: Identifica ocorrências com alto volume de relatos em vias de grande fluxo.
4. `prioridade_chamado(IdChamado, Prioridade)`: Classificação exclusiva em quatro níveis (`emergencia` > `alta` > `media` > `baixa`).
5. `atendimento_viavel(IdChamado)`: Verifica disponibilidade de equipe e suficiência de orçamento para o custo estimado do reparo.
6. `chamado_bloqueado(IdChamado, Motivo)`: Diagnostica impedimentos operacionais (`sem_equipe` e/ou `orcamento_insuficiente`).
7. `ordem_servico_imediata(IdChamado, Secretaria, Prioridade)`: Filtra chamados prioritários (`emergencia` ou `alta`) aptos para despacho imediato.

## 4. Como Executar
*Ainda vou colocar as instruções aqui*