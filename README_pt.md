<div align="center">
  <img src="https://img.shields.io/badge/Language-中文-red.svg" alt="Chinês">
  <img src="https://img.shields.io/badge/Language-English-blue.svg" alt="Inglês">
  <img src="https://img.shields.io/badge/Language-Español-yellow.svg" alt="Espanhol">
  <img src="https://img.shields.io/badge/Language-Português-green.svg" alt="Português">
  <img src="https://img.shields.io/badge/Model-SDTL-orange" alt="Modelo">
  <img src="https://img.shields.io/badge/Task-SOH_Estimation-blueviolet" alt="Tarefa">
  
  <h1>📚 Notas de Leitura: SDTL - Estimativa de SOH Online Baseada em Deep Transfer Learning e Autoatenção</h1>
  <p>Paper: Deep transfer learning enabled online state-of-health estimation of lithium-ion batteries under small samples across different cathode materials, ambient temperature and charge-discharge protocols</p>
  
  <div style="margin: 10px 0;">
    <a href="./" style="padding: 5px 10px; background: #f0f0f0; border-radius: 4px; text-decoration: none; color: #333;">简体中文</a> | 
    <a href="README_en.html" style="padding: 5px 10px; background: #f0f0f0; border-radius: 4px; text-decoration: none; color: #333;">English</a> | 
    <a href="README_es.html" style="padding: 5px 10px; background: #f0f0f0; border-radius: 4px; text-decoration: none; color: #333;">Español</a> | 
    <a href="#readme" style="padding: 5px 10px; background: #333; border-radius: 4px; text-decoration: none; color: #fff; font-weight: bold;">Português</a>
  </div>
</div>

> **Título do Artigo**: Deep transfer learning enabled online state-of-health estimation of lithium-ion batteries under small samples across different cathode materials, ambient temperature and charge-discharge protocols  
> **Revista**: Journal of Power Sources (2025, Vol. 650, 237503)  
> **Método Principal**: SDTL (Self-attention-based Deep Transfer Learning)  
> **Escopo**: Estimativa de SOH com pequenas amostras através de diferentes materiais catódicos (NCM/NCA), temperaturas e taxas.

## 🔍 Problemas Centrais
A estimativa online do Estado de Saúde (SOH) para baterias de íon-lítio enfrenta desafios significativos:
- **Escassez de Dados**: Dados insuficientes de estágios iniciais para baterias novas ou condições específicas.
- **Condições Variáveis**: Diferenças significativas de degradação devido a materiais catódicos (ex: NCM vs. NCA), temperaturas ambientes (ex: baixa temperatura $4^{\circ}C$) e taxas de descarga.
- **Generalização do Modelo**: Modelos tradicionais de aprendizado profundo lutam para manter a precisão em condições operacionais não vistas sem um retreinamento extenso.

## 💡 Metodologia: O Framework SDTL
O artigo propõe uma abordagem de Aprendizado de Transferência Profundo baseada em Autoatenção (SDTL). Ela utiliza grandes conjuntos de dados de um domínio fonte para pré-treinamento e adapta-se rapidamente a um domínio alvo usando apenas uma pequena quantidade de dados de ciclos iniciais via ajuste fino (fine-tuning).

> 📊 **Diagrama do Framework SDTL**
> ![Framework SDTL](assets/fig1.jpg)
> *Esta figura ilustra o fluxo de trabalho do SDTL: desde a aquisição de dados sob várias condições, extração e seleção de Indicadores de Saúde (HIs), pré-treinamento offline no domínio fonte, até o ajuste fino online e avaliação usando os primeiros 10% dos dados do domínio alvo.*

### Detalhes Técnicos Chave
1.  **Engenharia de Características**:
    -   Extraídos 18 Indicadores de Saúde (HIs) de curvas de tensão, corrente e capacidade incremental (IC).
    -   Selecionados 3 HIs principais usando o Coeficiente de Correlação de Pearson (PCC): Tempo de descarga em corrente constante (HI5), Entropia de corrente (HI17) e Inclinação de corrente (HI18).
2.  **Arquitetura do Modelo**:
    -   Emprega **Autoatenção Multi-Head (Multi-Head Self-Attention)** para capturar dependências de longo prazo em séries temporais.
    -   Incorpora Codificação Posicional para preservar a informação da sequência.
3.  **Estratégia de Transferência**:
    -   **Pré-treinamento**: Treinamento dos parâmetros do modelo em dados do domínio fonte.
    -   **Ajuste Fino**: Congelamento das camadas da rede, exceto a camada totalmente conectada, que é atualizada usando os primeiros 10% dos dados da bateria alvo.

> 📊 **Estrutura do Modelo de Autoatenção**
> ![Estrutura do Modelo](assets/fig5.jpg)
> *Diagrama da rede baseada em autoatenção, incluindo Codificação Posicional, blocos de Atenção Multi-Head, Normalização de Camada e Redes Feed-Forward (FFN).*

## 📈 Resultados Experimentais
O modelo foi validado em dois conjuntos de dados (Série A: baterias NCM, Série B: baterias NCA da NASA) cobrindo diferentes temperaturas ($24^{\circ}C, 4^{\circ}C$) e taxas (1C, 2C).

- **Precisão**: O SDTL alcançou RMSE e MAE mais baixos em comparação com os modelos base Transformer e LSTM.
- **Adaptação com Pequenas Amostras**: Capaz de previsão precisa do ciclo de vida completo usando apenas 10% dos dados de ciclos iniciais da bateria alvo.
- **Vantagem Comparativa**: Superou outros métodos de aprendizado de transferência (como DAAP, DAAD) em termos de precisão e estabilidade.

> 📊 **Visualização dos Resultados de Estimativa de SOH**
> ![Resultados de Estimativa](assets/fig8.jpg)
> *A Figura (a) mostra os resultados de estimativa em três séries de baterias; A Figura (b) destaca o desempenho de ajuste em condições de baixa temperatura ($4^{\circ}C$); A Figura (c) apresenta a comparação de distribuição de erros.*

## 📚 Referências
- **Citação**: Li, X., Zhao, M., et al. "Deep transfer learning enabled online state-of-health estimation..." Journal of Power Sources 650 (2025): 237503.
- **Fontes de Dados**: Conjunto de dados próprio de baterias NCM e Repositório de Prognósticos da NASA (NCA).

<br>

<div align="center">
  <p>© 2026 Tech Blog Notes | Fonte: <a href="https://doi.org/10.1016/j.jpowsour.2025.237503">Journal of Power Sources</a></p>
  <br>
  <a href="./">简体中文</a> | 
  <a href="README_en.html">English</a> | 
  <a href="README_es.html">Español</a> | 
  <a href="README_pt.html">Português</a>
</div>
