# 📊 Documentação Pública do Modelo Semântico - CecateNordeste

> **Guia Completo para Usuários, Analistas e Desenvolvedores**

**Data de Atualização:** 10 de dezembro de 2025  
**Status:** Modelo em Produção  
**Versão:** 1.0  
**Classificação:** Documento Público

---

## 📑 Índice

1. [Visão Geral](#visão-geral)
2. [Estrutura do Modelo](#estrutura-do-modelo)
3. [Tabelas e Dimensões](#tabelas-e-dimensões)
4. [Tabelas de Fatos](#tabelas-de-fatos)
5. [Medidas e Cálculos](#medidas-e-cálculos)
6. [Guia do Usuário](#guia-do-usuário)
7. [FAQ - Perguntas Frequentes](#faq---perguntas-frequentes)

---

## Visão Geral

### O que é este Modelo Semântico?

O **Modelo Semântico CecateNordeste** é uma base de dados multidimensional que organiza e integra informações sobre:

- 📍 **Municípios** da região Nordeste
- 👥 **Pessoas** inscritas em eventos de treinamento
- 📅 **Eventos** e atividades de capacitação
- ✅ **Inscrições** e presença em eventos
- ⭐ **Avaliações** de satisfação
- 💼 **Dados laborais** e histórico de trabalho
- 💰 **Informações financeiras** (PNATE e saldos)

### Objetivo Principal

Fornecer uma base consolidada de dados para análise, relatórios e tomada de decisão sobre o treinamento e capacitação profissional na região Nordeste.

### Estrutura Geral

```
MODELO SEMÂNTICO
│
├── 📊 TABELAS DE DIMENSÃO (Dim)
│   ├── dimMunicipio      → Informações geográficas
│   ├── dimEvento         → Detalhes dos eventos
│   ├── dimPessoa         → Dados dos participantes
│   ├── dimFuncao         → Categorias de funções
│   ├── dimContatos       → Informações de contato
│   └── dRegional         → Organização regional
│
├── 📈 TABELAS DE FATOS (Fact)
│   ├── fAvaliacao        → Avaliações dos participantes
│   ├── fInscricao        → Registros de inscrição
│   ├── fHistoricoTrabalho → Histórico profissional
│   └── fSaldosPnate      → Dados financeiros
│
├── ⏰ TABELAS DE TEMPO
│   ├── Calendario        → Tabela de datas completa
│   ├── Tempo             → Dimensão de tempo
│   ├── Periodo           → Períodos específicos
│   └── TempoAno          → Agrupamento por ano
│
└── 🛠️ TABELAS DE SUPORTE
    ├── _Medidas          → Cálculos e fórmulas DAX
    ├── _Cores            → Paleta de cores padronizada
    ├── _ExpTítulos       → Metadados e títulos
    └── Outras...         → Dados auxiliares
```

---

## Estrutura do Modelo

### Arquitetura em Estrela (Star Schema)

O modelo utiliza a arquitetura clássica **Star Schema**, onde:

- **TABELAS DE FATOS** (centro): Armazenam eventos/transações
- **TABELAS DE DIMENSÃO** (ao redor): Fornecem contexto e detalhes

**Benefícios:**
- ✅ Consultas rápidas
- ✅ Facilita análises multidimensionais
- ✅ Estrutura compreensível
- ✅ Manutenção simplificada

---

## Tabelas e Dimensões

### 1. **dimMunicipio** - Dimensão de Municípios

**Descrição:** Contém informações geográficas, administrativas e demográficas de todos os municípios.

**Campos Principais:**

| Campo | Tipo | Descrição |
|-------|------|-----------|
| `IDMunicipio` | Número | Identificador único |
| `codigo_ibge` | Número | Código IBGE oficial |
| `Município` | Texto | Nome do município |
| `Estado` | Texto | Estado (UF) |
| `código_uf` | Número | Código da unidade federativa |
| `População` | Número | População estimada |
| `latitude` | Decimal | Coordenada geográfica (latitude) |
| `longitude` | Decimal | Coordenada geográfica (longitude) |
| `capital` | Sim/Não | Indicador de capital |
| `Região` | Texto | Região geográfica |
| `Região Imediata` | Texto | Classificação regional imediata |
| `Região Intermediária` | Texto | Classificação regional intermediária |
| `Prioridade` | Sim/Não | Município prioritário |
| `Organização Regional` | Texto | Agrupamento administrativo |
| `Nome da Organização Regional` | Texto | Nome do agrupamento |

**Medidas Disponíveis:**
- **Municípios** → Contagem total de municípios
- **População Residente** → Soma da população
- **Regiões Intermediárias** → Contagem de regiões
- **Regiões Imediatas** → Contagem de sub-regiões
- **Municípios com Inscritos** → Contagem com registros
- **Municípios sem Inscritos** → Contagem sem registros
- **Número de Estados** → Contagem de UFs

**Exemplo de Uso:**
*"Quantos municípios existem no Ceará?" → Use a medida "Municípios" filtrada pelo Estado "CE"*

---

### 2. **dimEvento** - Dimensão de Eventos

**Descrição:** Cadastro completo de todos os eventos de treinamento e capacitação realizados.

**Campos Principais:**

| Campo | Tipo | Descrição |
|-------|------|-----------|
| `idEvento` | Número | Identificador único do evento |
| `NomeEvento` | Texto | Título/Nome do evento |
| `descricao` | Texto | Descrição detalhada |
| `data_evento_inicio` | Data | Data de início |
| `data_evento_fim` | Data | Data de término |
| `carga_horaria` | Número | Horas de duração do evento |
| `modalidade` | Texto | Tipo (Presencial/Online/Híbrido) |
| `localidade` | Texto | Local do evento |
| `vagas_maximas` | Número | Capacidade máxima |
| `nome_certificado` | Texto | Nome do certificado emitido |
| `site` | URL | Website do evento |
| `whatsapp` | Texto | Contato por WhatsApp |
| `contato_responsavel` | Texto | Pessoa responsável |
| `data_criacao` | Data | Data de cadastro |
| `data_finalizacao` | Data | Data de conclusão |

**Medidas Disponíveis:**
- **Número de Eventos** → Total de eventos
- **Participantes** → Pessoas que participaram
- **Participação das Pessoas** → Taxa de retorno
- **Participação dos Municípios** → Municipios atingidos

**Exemplo de Uso:**
*"Quantas pessoas participaram do treinamento XYZ?" → Selecione o evento em "dimEvento" e veja "Participantes"*

---

### 3. **dimPessoa** - Dimensão de Pessoas

**Descrição:** Registro de todas as pessoas inscritas ou participantes nos programas.

**Campos Principais:**

| Campo | Tipo | Descrição |
|-------|------|-----------|
| `idPessoa` | Número | Identificador único |
| `nome` | Texto | Nome completo |
| `email` | Texto | Endereço de email |
| `telefone` | Texto | Número de telefone |
| `cpf` | Texto | CPF (quando disponível) |
| `genero` | Texto | Gênero (M/F) |
| `data_nascimento` | Data | Data de nascimento |
| `endereco` | Texto | Endereço residencial |
| `municipio` | Texto | Município de residência |
| `estado` | Texto | Estado (UF) |
| `data_inscricao` | Data | Data do primeiro registro |
| `status` | Texto | Status atual (Ativo/Inativo) |
| `profissao` | Texto | Profissão declarada |
| `setor` | Texto | Setor de atuação |

---

### 4. **dimFuncao** - Dimensão de Funções

**Descrição:** Categorização das funções e cargos dos participantes.

| Campo | Tipo | Descrição |
|-------|------|-----------|
| `idFuncao` | Número | Identificador |
| `nomeFuncao` | Texto | Nome da função |

---

### 5. **dimContatos** - Dimensão de Contatos

**Descrição:** Informações detalhadas de contato e comunicação.

| Campo | Tipo | Descrição |
|-------|------|-----------|
| `idContato` | Número | Identificador único |
| `nome` | Texto | Nome do contato |
| `email` | Texto | Email principal |
| `telefone` | Texto | Telefone principal |
| `celular` | Texto | Celular |
| `endereco` | Texto | Endereço |
| `municipio` | Texto | Município |
| `estado` | Texto | Estado |
| `tipo` | Texto | Tipo de contato |
| `data_ultima_atualizacao` | Data | Última atualização |

---

### 6. **dRegional** - Dimensão Regional

**Descrição:** Agrupamento administrativo de municípios por regiões organizacionais.

| Campo | Tipo | Descrição |
|-------|------|-----------|
| `Código IBGE` | Número | Código do município |
| `Sigla Organização` | Texto | Sigla da região |
| `Nome Organização` | Texto | Nome completo |
| `Região Organização` | Texto | Macro-região |

---

## Tabelas de Fatos

### 1. **fAvaliacao** - Fato de Avaliações

**Descrição:** Registra as avaliações de satisfação e feedback dos participantes sobre os eventos.

**Campos Principais:**

| Campo | Tipo | Descrição |
|-------|------|-----------|
| `idAvaliacao` | Número | Identificador único |
| `idEvento` | Número | Evento avaliado |
| `idPessoa` | Número | Pessoa que avaliou |
| `data_cadastro` | Data | Data da avaliação |
| `nota_inscricao` | 1-5 | Avaliação: facilidade de inscrição |
| `nota_divulgacao` | 1-5 | Avaliação: divulgação do evento |
| `nota_data_evento` | 1-5 | Avaliação: agendamento adequado |
| `nota_horario` | 1-5 | Avaliação: horário conveniente |
| `nota_duracao` | 1-5 | Avaliação: duração apropriada |
| `nota_local` | 1-5 | Avaliação: local/infraestrutura |
| `nota_recepcao` | 1-5 | Avaliação: acolhimento |
| `nota_geral` | 1-5 | Avaliação geral do evento |
| `motivacao_experiencia` | Sim/Não | Motivo: ganhar experiência |
| `motivacao_discussoes` | Sim/Não | Motivo: trocar ideias |
| `motivacao_recursos` | Sim/Não | Motivo: obter recursos |
| `motivacao_conhecimentos` | Sim/Não | Motivo: adquirir conhecimentos |
| `motivacao_parcerias` | Sim/Não | Motivo: fazer parcerias |
| `aspectos_positivos` | Texto | O que foi bom |
| `aspectos_negativos` | Texto | Pontos de melhoria |
| `comentarios` | Texto | Comentários adicionais |

**Interpretação de Dados:**

- **Notas de 1-5:** Escala de satisfação
  - 1 = Muito insatisfeito
  - 3 = Neutro/Regular
  - 5 = Muito satisfeito

**Exemplo de Uso:**
*"Qual foi a satisfação média com a infraestrutura?" → Analise a média de "nota_local"*

---

### 2. **fInscricao** - Fato de Inscrições

**Descrição:** Registro de todas as inscrições em eventos.

**Campos Principais:**

| Campo | Tipo | Descrição |
|-------|------|-----------|
| `idInscricao` | Número | Identificador único |
| `idEvento` | Número | Evento |
| `idPessoa` | Número | Pessoa inscrita |
| `data_inscricao` | Data | Data da inscrição |
| `status` | Texto | Status (Confirmada/Cancelada/Pendente) |
| `presenca` | Sim/Não | Presença confirmada |
| `motivo_ausencia` | Texto | Motivo se ausente |
| `data_cancelamento` | Data | Se foi cancelada |

---

### 3. **fHistoricoTrabalho** - Fato de Histórico Laboral

**Descrição:** Histórico profissional e experiência de trabalho das pessoas.

| Campo | Tipo | Descrição |
|-------|------|-----------|
| `idHistorico` | Número | Identificador |
| `idPessoa` | Número | Pessoa |
| `empresa` | Texto | Nome da empresa |
| `cargo` | Texto | Cargo exercido |
| `data_inicio` | Data | Início |
| `data_fim` | Data | Término |
| `descricao` | Texto | Descrição da função |

---

### 4. **fSaldosPnate** - Fato de Saldos Financeiros

**Descrição:** Informações financeiras e saldos de recursos (PNATE e outros).

| Campo | Tipo | Descrição |
|-------|------|-----------|
| `idSaldo` | Número | Identificador |
| `idMunicipio` | Número | Município |
| `data_referencia` | Data | Data do saldo |
| `saldo_conta` | Dinheiro | Saldo em conta corrente |
| `saldo_fundos` | Dinheiro | Saldo em fundos |
| `saldo_rdb_cdb` | Dinheiro | Saldo em RDB/CDB |
| `saldo_poupanca` | Dinheiro | Saldo em poupança |
| `saldo_pnate` | Dinheiro | Saldo PNATE específico |

**Medidas Disponíveis:**
- **SaldoConta** → Saldo em conta
- **SaldoFundos** → Saldo em fundos
- **SaldoRDB/CDB** → Saldo em investimentos
- **SaldoPoupança** → Saldo poupador
- **SaldoPNATE** → Saldo PNATE total

---

## Medidas e Cálculos

### O que são Medidas?

**Medidas** são cálculos agregados (somas, contagens, médias) criadas com a linguagem **DAX** (Data Analysis Expression) que fornecem informações consolidadas.

### Medidas Organizadas por Categoria

#### 📍 **Medidas de Municípios e Geografia**

| Medida | Definição | Exemplo |
|--------|-----------|---------|
| **Municípios** | Contagem de municípios únicos | Total: 181 |
| **Municípios com Inscritos** | Municípios que têm pelo menos 1 inscrição | 142 |
| **Municípios sem Inscritos** | Municípios sem nenhuma inscrição | 39 |
| **Número de Estados** | Contagem de UFs | 9 (Nordeste) |
| **Regiões Imediatas** | Classificação regional menor | 15 |
| **Regiões Intermediárias** | Classificação regional maior | 3 |
| **Atendimento de Municípios** | % de municípios atendidos | 78% |

**Onde usar:**
- Dashboard "Cobertura Geográfica"
- Análise de expansão territorial
- Relatórios regionais

---

#### 👥 **Medidas de Participação e Pessoas**

| Medida | Definição | Exemplo |
|--------|-----------|---------|
| **Participantes** | Total de pessoas em evento específico | 450 |
| **Participação das Pessoas** | % de retorno/reengajamento | 65% |
| **Participação dos Municípios** | % de municípios em evento | 82% |
| **Número de Pessoas Inscritas** | Total de inscrições | 520 |
| **Lat** | Latitude média (para mapas) | -5.24 |
| **Long** | Longitude média (para mapas) | -38.76 |

**Onde usar:**
- Análise de alcance
- Mapeamento de participação
- Visualizações geográficas

---

#### 📅 **Medidas de Eventos e Atividades**

| Medida | Definição | Exemplo |
|--------|-----------|---------|
| **Número de Eventos** | Total de eventos realizados | 24 |
| **Número de Inscrições** | Total de inscrições em todos eventos | 1.250 |
| **Número de Presenças** | Pessoas que compareceram | 980 |
| **Número de Avaliações** | Avaliações respondidas | 856 |
| **Taxa de Presença** | % presença vs inscrição | 78% |

**Onde usar:**
- Dashboard executivo
- Relatórios de desempenho
- Análise de taxa de conversão

---

#### ⭐ **Medidas de Avaliação e Qualidade**

| Medida | Definição | Exemplo |
|--------|-----------|---------|
| **Nota Geral Média** | Média das avaliações gerais | 4.2/5 |
| **Satisfação Infraestrutura** | Média de nota_local | 4.0/5 |
| **Satisfação Facilitador** | Média de nota_recepcao | 4.5/5 |
| **Taxa Resposta Avaliação** | % que respondeu avaliação | 82% |

---

#### 🎓 **Medidas do Sistema SETE**

| Medida | Definição | Aplicação |
|--------|-----------|-----------|
| **Número de Estudantes SETE** | Alunos do sistema SETE | Educação |
| **Estudantes Sete/Censo** | Taxa SETE vs Censo | Cobertura |
| **Municípios com SETE Instalado** | Onde sistema está operacional | Implementação |
| **% Municípios sem Estudante SETE** | Gaps de cobertura | Análise de lacunas |
| **MunicipioUsaSete** | Indicador de uso ativo | Status operacional |

---

#### 💰 **Medidas Financeiras**

| Medida | Definição | Aplicação |
|--------|-----------|-----------|
| **SaldoConta** | Total em contas correntes | Fluxo de caixa |
| **SaldoFundos** | Total em fundos | Investimentos |
| **SaldoRDB/CDB** | Total em RDB/CDB | Poupança |
| **SaldoPoupança** | Total em poupança | Reservas |
| **SaldoPNATE** | Recursos PNATE disponíveis | Orçamento específico |

---

#### 🎨 **Medidas de Cores (Visualização)**

Estas medidas retornam códigos hexadecimais para padronizar cores nos relatórios:

| Medida | Cor | Código |
|--------|-----|--------|
| **corPrincipal_60** | Azul Vivido 60% | #155BCB |
| **corPrincipal_80** | Azul Vivido 80% | #0C326F |
| **corPrincipal_5** | Azul Vivido 5% | #EDF5FF |
| **corNeutra_90** | Cinza 90% | #1B1B1B |
| **corNeutra_70** | Cinza 70% | #555555 |
| **corNeutra_20** | Cinza 20% | #CCCCCC |
| **corNeutra_10** | Cinza 10% | #E6E6E6 |
| **corNeutra_4** | Cinza 4% | #F3F3F3 |
| **corPura_branco** | Branco | #FFFFFF |

**Uso:** Consultor Visual em relatórios para consistência de cores

---

## Guia do Usuário

### Como Interpretar os Dados

#### Cenário 1: "Avaliar Performance de um Evento"

1. Selecione o **evento** em `dimEvento`
2. Observe:
   - **Número de Inscrições** → Interesse
   - **Número de Presenças** → Taxa de comparecimento
   - **Número de Avaliações** → Engajamento pós-evento
   - **Notas de avaliação** → Satisfação
   - **Participantes por Município** → Alcance geográfico

**Exemplo:** 
- Evento "Treinamento de Gestão"
- 250 inscritos, 210 presentes (84%), 180 avaliações
- Média: 4.3/5 ⭐ (Bom desempenho!)

---

#### Cenário 2: "Identificar Municípios com Baixa Cobertura"

1. Filtre por **Estado** ou **Região**
2. Use **Atendimento de Municípios**
3. Identifique: Municípios sem inscritos
4. Próximas ações: Focar em expansão

**Exemplo:**
- Estado: Piauí
- Cobertura: 65%
- 8 municípios sem inscritos → Alvo de ação

---

#### Cenário 3: "Analisar Dados Financeiros"

1. Selecione **período** no calendário
2. Visualize **saldos por tipo**:
   - Conta corrente
   - Fundos
   - PNATE
3. Compare **tendências** ao longo do tempo

---

### Boas Práticas

✅ **Faça:**
- Use filtros para focar análises
- Combine múltiplas medidas para contexto
- Valide dados extremos (valores muito altos/baixos)
- Documente conclusões importantes

❌ **Evite:**
- Tirar conclusões com amostra pequena (<5 registros)
- Comparar períodos muito diferentes sem contextualização
- Ignorar datas de atualização dos dados

---

## FAQ - Perguntas Frequentes

### Q1: Qual a diferença entre "Inscrição" e "Presença"?

**R:** 
- **Inscrição** = Pessoa se registrou no evento
- **Presença** = Pessoa realmente compareceu

Uma pessoa pode estar inscrita mas não comparecer.

---

### Q2: Por que existem múltiplas tabelas de data local?

**R:** Foram criadas automaticamente pelo Power BI para relacionamentos de data. Plano futuro: consolidar em uma única tabela.

---

### Q3: Como interpretar as notas de avaliação?

**R:**
```
1 = Muito Insatisfeito  😞
2 = Insatisfeito        😐
3 = Neutro/Regular      😐
4 = Satisfeito          😊
5 = Muito Satisfeito    😍
```

Média **≥ 4.0** = Desempenho excelente ✅

---

### Q4: O que significa "Taxa de Presença"?

**R:** 
$$\text{Taxa Presença} = \frac{\text{Presenças}}{\text{Inscrições}} \times 100\%$$

**Exemplo:** 800 presentes / 1000 inscritos = **80%**

---

### Q5: Como o SETE se relaciona com os dados do Censo?

**R:** 
- **SETE** = Sistema integrado no Nordeste (dados operacionais)
- **Censo** = Dados oficiais de educação

A comparação mostra cobertura (SETE/Censo × 100%)

---

### Q6: Posso usar estes dados comercialmente?

**R:** Consulte o documento de **Política de Dados** e **Termos de Uso** da instituição.

---

### Q7: Como reportar dados inconsistentes?

**R:** Envie um ticket técnico para: `suporte@cecatene.org`

Inclua:
- Data da descoberta
- Medida/Campo afetado
- Valor esperado vs real
- Capturas de tela

---

### Q8: Com que frequência os dados são atualizados?

**R:** 
- **Eventos e Inscrições:** Diário
- **Avaliações:** Diário
- **Dados Financeiros:** Mensalmente
- **Dados Geográficos:** Anualmente (ou quando há mudanças)

---

### Q9: Existe API para acessar estes dados programaticamente?

**R:** Verifique disponibilidade com a equipe técnica. Opções possíveis:
- Power BI Embedded API
- REST API customizada
- Exportação em lote (CSV/Excel)

---

### Q10: Como criar um novo relatório usando este modelo?

**R:** Pasos:
1. Conecte ao modelo semântico
2. Selecione tabelas e colunas
3. Adicione filtros relevantes
4. Escolha visualizações apropriadas
5. Crie medidas personalizadas se necessário

**Consulte:** Guia de Criação de Relatórios (documento separado)

---

## Estatísticas do Modelo

### Volume de Dados

| Elemento | Quantidade |
|----------|-----------|
| **Tabelas** | 41 |
| **Dimensões** | 6 |
| **Tabelas de Fato** | 4 |
| **Medidas Calculadas** | 69 |
| **Colunas Totais** | ~500+ |
| **Relacionamentos** | 20+ |

### Cobertura Geográfica

- **Estados:** 9 (Nordeste)
- **Municípios:** 181
- **Regiões Imediatas:** 15
- **Regiões Intermediárias:** 3

### Histórico de Dados

- **Dados Disponíveis Desde:** 2020
- **Atualização Mais Recente:** 10/12/2025
- **Período Coberto:** ~5 anos

---

## Próximos Passos

- [ ] Ler este guia completamente
- [ ] Explorar um relatório específico
- [ ] Fazer uma primeira análise
- [ ] Documentar insights
- [ ] Compartilhar aprendizados com a equipe

---

## Suporte e Contato

**Dúvidas sobre dados?**
- 📧 Email: `dados@cecatene.org`
- 📱 WhatsApp: +55 (xx) 9xxxx-xxxx
- 🌐 Website: www.cecatene.org

**Problemas técnicos?**
- 🐛 Abra uma issue em: `github.com/Rede-DSBR/CecateNE`
- 📋 Descreva o problema com detalhes

---

## Histórico de Versões

| Versão | Data | Alterações |
|--------|------|-----------|
| 1.0 | 10/12/2025 | Documentação inicial |
| | | Descrição completa de tabelas e medidas |
| | | Guia do usuário |
| | | FAQ |

---

## Anexos

### A. Glossário de Termos

- **DAX:** Data Analysis Expression (linguagem de fórmulas)
- **PNATE:** Programa Nacional de Apoio ao Transporte Escolar
- **IBGE:** Instituto Brasileiro de Geografia e Estatística
- **Dataflow:** Pipeline de dados do Power BI
- **Star Schema:** Arquitetura de dados em forma de estrela

### B. Referências

- [Power BI Documentation](https://docs.microsoft.com/power-bi/)
- [DAX Function Reference](https://dax.guide/)
- [SETE Sistema](https://www.google.com)

### C. Checklist de Validação de Dados

- [ ] Data está no período esperado?
- [ ] Valores estão dentro de intervalos lógicos?
- [ ] Há valores NULL ou vazios inesperados?
- [ ] Contagens fazem sentido com filtros aplicados?
- [ ] Comparações de período são consistentes?

---

## Licença e Termos de Uso

Este documento e os dados que descreve são fornecidos conforme os termos da instituição.

**Classificação:** Documento Público  
**Última Atualização:** 10 de dezembro de 2025  
**Próxima Revisão:** 10 de junho de 2026

---

**Desenvolvido com ❤️ pela Equipe de Dados da Rede-DSBR**

Para sugestões de melhoria, favor abrir uma issue no repositório GitHub.
