# 📊 Documentação do Modelo Semântico - CecateNordeste

**Data:** 10 de dezembro de 2025  
**Status:** Modelo em produção  
**Total de Tabelas:** 41  
**Total de Medidas:** 69

---

## 📋 Tabelas do Modelo

### Tabelas de Dimensão (Dim)

| Tabela | Colunas | Medidas | Hierarquias | Descrição |
|--------|---------|---------|-------------|-----------|
| `dimMunicipio` | 28 | 10 | 0 | Dimensão com informações sobre municípios |
| `dimEvento` | 19 | 3 | 0 | Dimensão com eventos |
| `dimPessoa` | 32 | 0 | 0 | Dimensão com dados de pessoas |
| `dimFuncao` | 2 | 0 | 0 | Dimensão com funções |
| `dimContatos` | 16 | 0 | 0 | Dimensão com informações de contatos |
| `dRegional` | 7 | 0 | 0 | Dimensão com dados regionais |

### Tabelas de Fato (Fact)

| Tabela | Colunas | Medidas | Hierarquias | Descrição |
|--------|---------|---------|-------------|-----------|
| `fAvaliacao` | 24 | 0 | 0 | Tabela de fatos com avaliações |
| `fInscricao` | 8 | 0 | 0 | Tabela de fatos com inscrições |
| `fHistoricoTrabalho` | 7 | 0 | 0 | Tabela de fatos com histórico de trabalho |
| `fSaldosPnate` | 18 | 5 | 0 | Tabela de fatos com saldos PNATE |

### Tabelas de Tempo

| Tabela | Colunas | Medidas | Hierarquias | Descrição |
|--------|---------|---------|-------------|-----------|
| `Calendario` | 114 | 0 | 0 | Tabela de calendário principal |
| `Tempo` | 10 | 0 | 0 | Tabela de dimensão temporal |
| `Periodo` | 5 | 0 | 0 | Tabela de períodos |
| `TempoAno` | 2 | 1 | 0 | Tabela de anos |

### Tabelas de Suporte e Sistema

| Tabela | Colunas | Medidas | Hierarquias | Descrição |
|--------|---------|---------|-------------|-----------|
| `_Medidas` | 1 | 30 | 0 | Tabela de medidas DAX (contém 30 medidas) |
| `_Cores` | 3 | 9 | 0 | Tabela de cores para visualizações |
| `_ExpTítulos` | 2 | 1 | 0 | Tabela de títulos para exploração (com descrição de metadados) |
| `sete_instalado` | 9 | 0 | 0 | Tabela de dados do SETE instalado |
| `sete_municipios` | 13 | 4 | 0 | Tabela com dados de SETE por município |
| `SeteUsuarios` | 9 | 4 | 0 | Tabela com dados de usuários do SETE |
| `BuscaAtiva` | 2 | 2 | 0 | Tabela de busca ativa |
| `FiltroMapa` | 4 | 0 | 0 | Tabela de filtros para mapa |
| `Censo_EB` | 426 | 0 | 0 | Tabela com dados do Censo de Educação Básica |

### Tabelas de Data Local (Automáticas)

O modelo contém **14 tabelas de data local** geradas automaticamente:
- `DateTableTemplate_7c54cf19-ef04-4c94-aaa5-5f5a8093b05f`
- `LocalDateTable_40f89283-abcf-49f0-9276-fb230c7c3c1e`
- `LocalDateTable_5ded2b83-11bd-4cc3-b41c-cbc8a205d316`
- `LocalDateTable_a93d66dc-1439-43ce-a254-337be33512de`
- `LocalDateTable_87e99e2c-d28d-4da1-84d3-e287a3ad3c0c`
- `LocalDateTable_a2e6e66b-22b8-4e90-beec-c67af2d87c5f`
- `LocalDateTable_714801ab-058c-4b6b-836a-64b973b7b5bf`
- `LocalDateTable_abed839e-03d2-4eb1-80a5-2ee7eb660cfb`
- `LocalDateTable_f91f19ea-d147-4bbe-ae24-0d9c3a9d927a`
- `LocalDateTable_a7333622-14e4-4313-a81e-3b9d5b072a20`
- `LocalDateTable_03f9d67e-8a4e-481d-879d-0841adfc5289`
- `LocalDateTable_18203fa7-bb24-498b-8e9b-ffbc0c59bf9c`
- `LocalDateTable_2d20d7fa-86c4-45b8-8ebf-d66785e429a4`
- `LocalDateTable_58f4833f-0280-487d-81f3-6f475af88e75`
- `LocalDateTable_34a011be-68ae-4b1a-b24d-11745f859776`
- `LocalDateTable_643f3fab-f141-4299-813f-c3ea5dd4e465`
- `LocalDateTable_61cc53be-0ac3-4d7f-90c3-c074d68ecbe1`
- `LocalDateTable_09ff0678-f625-465c-80c1-5b9475a309da`

---

## 📊 Medidas Produzidas

### Medidas de Municípios e Geografia

```
1. Municípios
2. Municípios sem inscritos
3. Municípios com inscritos
4. MunicipioSeteInstalado
5. MunicipioTeveInscrito
6. MunicipioTevePresença
7. MunicipioUsaSete
8. MunicipioNaoTevePresença
9. Número de Municípios sem Presença
10. Número de Municípios com Presença
11. Atendimento de Municípios
12. Número de munic. mapa
13. ListaMunic. Cominscrição
14. ListaMunic.
15. ListaMunic.PorRegional
16. ListaMunic.ComInscricaoEventoSelecionado
17. ListaMunic.SemInscricaoEventoSelecionado
18. Número de Munic. sem Estudante SETE
19. Número de Munic. Estudante SETE/Censo
```

### Medidas de População e Regiões

```
20. População Residente
21. Regiões Intermediárias
22. Regiões Imediatas
23. Número de Estados
24. % Região
25. % Instalação
```

### Medidas de Participação

```
26. Participantes
27. Participação das Pessoas
28. Participação dos Municípios
```

### Medidas de Eventos e Inscrições

```
29. Número de Eventos
30. Número de Pessoas Inscritas
31. Número de Avaliações
32. Número de Inscrições
33. Número de Presenças
```

### Medidas de Cores

```
34. corPrincipal_60
35. corNeutra_10
36. corPrincipal_80
37. corPrincipal_5
38. corNeutra_90
39. corNeutra_20
40. corNeutra_70
41. corNeutra_4
42. corPura_branco
43. CorMapa
```

### Medidas do Sistema SETE

```
44. MunicipioSeteInstalado
45. MunicipioTeveInscrito
46. MunicipioTevePresença
47. MunicipioUsaSete
48. Número de Estudantes SETE
49. Estudantes Sete/Censo
50. Número de Munic. sem Estudante SETE
51. Número de Munic. Estudante SETE/Censo
52. % Munic. sem Estudante SETE
53. Munic. com o Sete Instalado
54. SETE - Número de usuários
55. SETE - Número de administradores
56. SETE - Número de Editores
57. SETE - Número de Leitores
58. ValorMapa
59. ExibeMunicipioMapa
```

### Medidas de Educação e Transporte

```
60. Estudantes Transportados Censo
61. Número de Estudantes da Educação Básica Censo
62. Número de Escolas
63. Número de Motoristas
64. Número de veículos em funcionamento
65. Número de Rotas
```

### Medidas Financeiras

```
66. SaldoConta
67. SaldoFundos
68. SaldoRDB/CDB
69. SaldoPoupança
70. SaldoPNATE
71. Filtro de Período
```

### Outras Medidas

```
72. Lat
73. Long
74. ExpSubTitulo
```

---

## 📈 Resumo Estatístico

| Métrica | Valor |
|---------|-------|
| **Total de Tabelas** | 41 |
| **Tabelas de Dimensão** | 6 |
| **Tabelas de Fato** | 4 |
| **Tabelas de Data Local** | 18 |
| **Tabelas de Suporte** | 13 |
| **Total de Medidas** | 69 |
| **Medidas em _Medidas** | 30 |
| **Medidas em dimMunicipio** | 10 |
| **Medidas em _Cores** | 9 |
| **Medidas em SeteUsuarios** | 4 |
| **Medidas em sete_municipios** | 4 |
| **Medidas em fSaldosPnate** | 5 |
| **Medidas em dimEvento** | 3 |
| **Medidas em _ExpTítulos** | 1 |
| **Medidas em TempoAno** | 1 |
| **Medidas em BuscaAtiva** | 2 |

---

## 🔗 Relações Principais

Baseado na estrutura identificada, as principais relações são:

- **dimMunicipio** ↔ **fAvaliacao**, **fInscricao**, **fHistoricoTrabalho**, **fSaldosPnate**
- **dimEvento** ↔ **fAvaliacao**, **fInscricao**
- **dimPessoa** ↔ **fAvaliacao**, **fInscricao**, **fHistoricoTrabalho**
- **Tempo/Calendario** ↔ Múltiplas tabelas de fato

---

## 📝 Notas Importantes

1. **Tabelas de Data Local:** Existem múltiplas tabelas de data local, possivelmente criadas automaticamente pelo Power BI. Considere consolidar em uma única tabela de dimensão de data.

2. **Tabela _Medidas:** Concentra 30 medidas calculadas em DAX - uma boa prática para organização.

3. **Sistema SETE:** O modelo possui extenso suporte a dados do Sistema SETE, incluindo informações de usuários, municípios e estudantes.

4. **Censo de Educação Básica:** Tabela com 426 colunas, sugerindo dados muito granulares do censo educacional.

5. **Metadados:** A tabela `_ExpTítulos` contém metadados sobre as páginas do relatório com informações de autor, versão e data.

---

## 📞 Próximos Passos Recomendados

- [ ] Consolidar tabelas de data local
- [ ] Documentar fórmulas DAX das 69 medidas
- [ ] Criar dicionário de dados para todas as colunas
- [ ] Revisar e otimizar relacionamentos
- [ ] Validar performance do modelo

---

**Gerado automaticamente via MCP Power BI Modeling**
