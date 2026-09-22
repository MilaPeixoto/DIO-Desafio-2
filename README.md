# Desafio Criativo — Feedbacks Bancários e Fraudes via Pix

Por: Camila Maia

## Introdução

Este projeto foi desenvolvido como parte do Desafio Criativo da DIO, com foco em análise de feedbacks públicos de clientes bancários relacionados a fraudes em transações Pix.

O objetivo é estruturar os dados em um banco MariaDB, aplicar consultas SQL e extrair insights relevantes para apoiar equipes de prevenção a fraudes e gestão de riscos em instituições financeiras.

A entrega final inclui:

- Um prompt refinado para orientar a IA na análise.
- A modelagem do banco de dados em MariaDB.
- Scripts de inserção de dados e consultas SQL.
- Views para facilitar análises recorrentes.

---

## Passo 1 — Definição da intenção

Quero que a IA analise uma base de dados públicos sobre fraudes relacionadas a transações Pix para identificar padrões, tendências e indicadores relevantes sobre a ocorrência de fraudes no sistema de pagamentos, para montar um banco de dados utilizando Maria DB.

O resultado será usado por equipes de análise de dados, prevenção a fraudes e gestão de riscos de instituições financeiras para apoiar a identificação de situações de maior ocorrência de fraude e orientar ações de monitoramento e prevenção.

A entrega deve conter um resumo dos principais insights encontrados, uma organização dos dados por critérios relevantes, evidências numéricas extraídas da base e sugestões de ações que possam ser consideradas pelas áreas responsáveis.

O resultado será considerado bom se for claro, organizado, baseado exclusivamente nos dados fornecidos, apresentar evidências que sustentem os insights identificados e gerar informações úteis para apoiar decisões de análise, monitoramento e prevenção de fraudes.

---

## Fontes

Utilizei como fonte o reclame aqui de alguns bancos como: Bradesco, Itaú e Santander. Destes, selecionei 19 feedbacks, que estão organizados na tabela a seguir:

| #  | Banco     | Data       | Tipo de ocorrência                  | Resumo do relato + Link |
|----|-----------|------------|-------------------------------------|--------------------------|
| 1  | Itaú      | 10/09/2026 | Golpe via Pix                       | Cliente relata ter caído em golpe, feito um Pix para uma conta Itaú e contestado imediatamente. Segundo o relato, a contestação não foi reconhecida e houve prejuízo de R$ 200. [Fonte](https://www.reclameaqui.com.br/itau/editado-pelo-reclame-aqui-via-pix-banco-itau-nao-reconhece-contestacao-e-cliente-fica-no-prejuizo_SYswuONB9zQOILNc/) |
| 2  | Itaú      | 16/03/2026 | Pix não reconhecido                 | Cliente afirma que cinco Pix sequenciais foram realizados de uma conta poupança sem sua autorização. Relata ter feito BO e contestado as operações. [Fonte](https://www.reclameaqui.com.br/itau/itau-se-rea-a-contestar-5-transacoes-pix-em-conta-poupanca-mesmo-com-bolet_HTgz-H2V6g2rtE-F/) |
| 3  | Itaú      | 23/04/2026 | Pix para pessoa desconhecida         | Cliente relata uma transferência Pix de R$ 1.100 para pessoa desconhecida e tentativa de recuperação pelo MED. Afirma que o pedido foi negado porque o saldo já havia sido retirado da conta destinatária. [Fonte](https://www.reclameaqui.com.br/itau/falha-na-seguranca-do-banco-itau-na-contestacao-de-pix-e-de-indebita-de-r-110000_CVR0QmHo-h1MERoF/) |
| 4  | Itaú      | 28/04/2026 | Contestação de Pix                  | Cliente relata dois pagamentos via QR Code, de R$ 899 e R$ 901, e informa que a contestação das devoluções foi negada. [Fonte](https://www.reclameaqui.com.br/itau/contestacao-de-pagamento-via-pix-negada-pelo-itau_543GUwlcUissCFXx/) |
| 5  | Itaú      | 01/02/2026 | Golpe em compra de celular          | Cliente relata ter enviado R$ 100 via Pix para reservar um celular, descobriu posteriormente que se tratava de golpe, registrou BO e solicitou contestação/MED. [Fonte](https://www.reclameaqui.com.br/itau/cliente-vitima-de-editado-pelo-reclame-aqui-via-pix-busca-contestacao-e-acionamento-do-med-junto-ao-itau_vXzTKJoPjmN3N54O/) |
| 6  | Itaú      | 31/03/2026 | Publicidade enganosa / Pix          | Cliente relata ter realizado múltiplas transferências após ser induzido por publicidade no TikTok, posteriormente identificada por ele como golpe. Afirma ter contestado todas as transações menos de dez minutos depois. [Fonte](https://www.reclameaqui.com.br/itau/falha-na-seguranca-e-negativa-indevida-de-contestacao-de-pix-possivel-editado-pelo-reclame-aqui-solicitacao-de-reanalise-e-med_QBNy-7ofRvb7Nzrp/) |
| 7  | Itaú      | 11/08/2026 | Pix não autorizado                  | Cliente afirma ter identificado um Pix de R$ 200 que não reconhecia, abriu contestação e enviou BO. Relata que a contestação foi encerrada sem recuperação do valor. [Fonte](https://www.reclameaqui.com.br/itau/pix-nao-autorizado-e-contestacao-negada-pelo-banco_X4geh_d-f2864UiY/) |
| 8  | Itaú      | 22/04/2026 | Contestação indevida                | Cliente afirma ter sido afetado por uma contestação de Pix iniciada por outra pessoa, gerando estornos e bloqueios que atingiram valores relacionados a ele. [Fonte](https://www.reclameaqui.com.br/itau/contestacao-de-pix-indevida-originada-no-itau-causa-prejuizos-financeiros-e-bancarios-ao-cliente_ZJ-axBWhzSaIRqTz/) |
| 9  | Santander | 26/08/2026 | Golpe / Pix                         | Cliente relata duas transações Pix de R$ 400 e R$ 500 realizadas após ser induzido por uma situação fraudulenta. Solicita contestação e acionamento do MED. [Fonte](https://www.reclameaqui.com.br/santander/contestacao-de-pix-e-solicitacao-de-devolucao-de-valores-apos-editado-pelo-reclame-aqui_bptGinUjvTBW2a1x/) |
| 10 | Santander | 29/06/2026 | Boleto falso / Pix                  | Cliente afirma ter pago via Pix um boleto para um CNPJ diferente do esperado. Contestou a operação, mas relata que o banco não identificou indícios de fraude. [Fonte](https://www.reclameaqui.com.br/santander/contestacao-de-pix-por-golpe-pagamento-de-boleto-para-cnpj-incorreto-banco_yBtHTdY0RkMPXsZ3/) |
| 11 | Santander | 09/03/2026 | Contestação indevida                | Cliente relata que recebeu um Pix por um serviço, mas posteriormente a remetente contestou a transação. Segundo o relato, isso provocou restrições em sua conta. [Fonte](https://www.reclameaqui.com.br/santander/contestacao-indevida-de-pix-e-restricao-na-conta-bancaria-no-banco-santander_OrSxdk6iwTT9fCtF/) |
| 12 | Santander | 17/07/2026 | Conta invadida                      | Cliente afirma que sua conta foi invadida e que ocorreu um Pix indevido. Diz ter realizado contestação e não ter recebido resposta inicialmente. A resposta posterior do banco contesta a ocorrência. [Fonte](https://www.reclameaqui.com.br/santander/conta-invadida-e-pix-realizado-indevidamente-sem-resposta-a-contestacao_7MHzx1oVnEcKjIBR/) |
| 13 | Santander | 02/09/2026 | Celular furtado / Pix não reconhecido | Cliente relata furto do celular, acesso posterior às contas e realização de Pix de R$ 1.999,99 usando o cheque especial. Afirma não reconhecer a operação e relata contestação negada. [Fonte](https://www.reclameaqui.com.br/santander/celular-furtado-acesso-indevido-a-conta-e-pix-nao-reconhecido-de-r-199999-contestacao-negada_-wLMHAIUQ6IfpcXF/) |
| 14 | Santander | 30/04/2026 | Golpe relacionado a contratação     | Cliente afirma ter recebido uma proposta falsa de contratação e realizado Pix de R$ 99,90. Contestou pelo Santander e relata falta de retorno dentro do prazo informado. [Fonte](https://www.reclameaqui.com.br/santander/contestacao-de-pix_bnMA9cp5VsyGjis4/) |
| 15 | Santander | 13/03/2026 | Golpe / MED                         | Cliente relata ter realizado um Pix e posteriormente identificado que se tratava de golpe. Afirma ter contestado no dia seguinte e não ter recebido retorno dentro do prazo informado. [Fonte](https://www.reclameaqui.com.br/santander/de-pix-e-falta-de-retorno-do-santander-apos-contestacao_dq_uLsGlgOULpP7j/) |
| 16 | Santander | 01/03/2026 | Pix não processado corretamente     | Cliente relata tentativa de pagamento em loja física, com erro no aplicativo, mas débito do valor de R$ 119,97. Afirma que recebeu orientação de que seria reembolsado, mas o valor não teria sido devolvido no prazo. [Fonte](https://www.reclameaqui.com.br/santander/dificuldade-em-obter-informacoes-sobre-contestacao-de-pix-e-falta-de-retorno-sobre_oQraj4vgLlnoytau/) |
| 17 | Bradesco  | 14/04/2025 | Loja falsa / Pix                    | Cliente relata ter comprado de uma loja falsa, realizado Pix por QR Code e percebido o golpe após não receber o produto. Afirma ter aberto contestação e não ter obtido recuperação inicialmente. [Fonte](https://www.reclameaqui.com.br/bradesco/bradesco-conivente-com-a-primepag_ZmVtuwfPG4hvmZ7Y/) |
| 18 | Bradesco  | 2025       | MED / contestação                   | Cliente relata que valores recebidos em sua conta foram posteriormente devolvidos por meio de contestações Pix, causando restrições sobre os valores recebidos. [Fonte](https://www.reclameaqui.com.br/bradesco/banco-bradesco-permite-uso-indevido-do-medpix-e-causa-prejuizo-financeiro_8_qxqsyXN0KgsEN5/) |
| 19 | Bradesco  | 2025       | Pix / MED                           | Há uma reclamação individual do Bradesco sobre golpe via Pix e falha no processo de MED, com relato do consumidor e resposta institucional. A página permanece acessível, mas o resultado de busca que consegui recuperar não expõe toda a data e descrição inicial com a mesma qualidade dos demais registros. [Fonte](https://www.reclameaqui.com.br/bradesco/via-pix-e-falha-no-med-pelo-bradesco_bmXQ38oLXSZRg7CI/) |

---

## Passo 2 — Contexto e restrições

**Contexto:**

Feedbacks de clientes bancários relacionados a fraudes em Pix, incluindo golpes, contestações indevidas, falhas no MED e operações não reconhecidas.

**Dados disponíveis:**
- Banco (Itaú, Santander, Bradesco)
- Data da ocorrência
- Tipo de ocorrência
- Resumo do relato
- Links de referência (Reclame Aqui)

**Critérios de análise:**
- Tipo de fraude
- Banco envolvido
- Data/ano
- Valor citado (quando disponível)
- Impacto percebido

**Cuidados e restrições:**
- Usar apenas os dados fornecidos.
- Não inventar números, causas ou conclusões.
- Não expor dados pessoais ou sensíveis.
- Informar limitações quando os dados não forem suficientes.
- Usar linguagem clara, executiva e voltada para tomada de decisão.

---

## Passo 3 — Prompt Final

Atue como analista de dados especializado em prevenção a fraudes bancárias.

Sua tarefa é analisar feedbacks públicos de clientes bancários sobre fraudes em transações Pix para identificar padrões, tendências e indicadores relevantes.

**Instruções de análise:**
- Classifique os relatos por tipo de ocorrência, modalidade de golpe ou fraude, situação da transação, existência de contestação, menção ao MED, recuperação ou não recuperação do valor, problemas relacionados ao atendimento e sentimento predominante no relato.
- Identifique os principais padrões, problemas recorrentes e oportunidades de melhoria observados na amostra.
- Identifique, quando houver evidências suficientes, características recorrentes das ocorrências, como engenharia social, transações não reconhecidas, contas invadidas, falsas ofertas, lojas falsas ou outros mecanismos descritos nos relatos.
- Aponte evidências presentes nos dados fornecidos para sustentar cada insight identificado.
- Diferencie claramente informações relatadas pelo consumidor de informações confirmadas pela instituição financeira ou pela fonte.
- Quando houver valores financeiros disponíveis, organize-os e apresente os cálculos somente quando puderem ser realizados exclusivamente com os dados fornecidos.
- Analise possíveis problemas relacionados ao processo de contestação, MED, atendimento e recuperação de valores, sem atribuir responsabilidade à instituição quando os dados não forem suficientes para sustentar essa conclusão.
- Sugira ações práticas para equipes de prevenção a fraudes, gestão de riscos e atendimento, deixando claro quando uma sugestão for uma recomendação analítica e não uma conclusão comprovada pelos dados.

**Formato da resposta:**
1. **Resumo executivo:** apresente os principais insights encontrados na amostra de forma objetiva.  
2. **Classificação dos relatos:** Crie um script para criar tabelas no MariaDB.  
   - **Primeira tabela:** `tbl_feedbacks`  
     - id  
     - id_bank  
     - id_occurrence  
     - date  
     - summary  
     - valueInvolved  
     - referenceLink  
   - **Segunda tabela:** `tbl_banks`  
     - id  
     - bankName  
   - **Terceira tabela:** `tbl_occurrences`  
     - id  
     - occurrenceType  
   - Conecte as tabelas utilizando **FOREIGN KEY**.  
3. **Principais padrões:** apresente os padrões recorrentes identificados e explique quais evidências dos relatos sustentam cada padrão.  
4. **Problemas e oportunidades:** organize os principais problemas identificados e as respectivas oportunidades de melhoria.  
5. **Ações sugeridas:** apresente recomendações práticas para prevenção a fraudes, gestão de riscos e atendimento, relacionando cada ação aos problemas identificados.  
6. **Limitações da análise:** informe explicitamente quando os dados forem insuficientes, quando houver informações não disponíveis e quais limitações existem devido ao tamanho e à forma de seleção da amostra.

**Restrições:**
- Usar apenas os dados fornecidos.
- Não inventar números, causas ou conclusões.
- Diferencie relatos dos clientes de fatos comprovados.
- Não exponha dados pessoais ou sensíveis.
- Não generalize os resultados para todos os clientes ou fraudes dos bancos.
- Informe quando os dados forem insuficientes.
- Use linguagem clara, objetiva e técnica.

