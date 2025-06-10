# Painel de Relatório de Lojas

Este é um painel de controle interativo, totalmente funcional e em tempo real, desenvolvido para monitorar e analisar o desempenho de vendas de múltiplas lojas. A aplicação é construída como uma única página (SPA) utilizando HTML, Tailwind CSS para estilização, e Firebase (Firestore e Authentication) como backend para armazenamento e autenticação de dados.

![Imagem do Painel de Relatório de Lojas](https://placehold.co/800x400/0052CC/FFFFFF?text=Dashboard+de+Lojas)

---

## ✨ Funcionalidades

O painel está dividido em quatro seções principais, cada uma com dashboards e funcionalidades específicas:

### 1. Dashboard Geral
Uma visão consolidada e de alto nível da performance geral:
- **KPIs Principais:** Faturamento total, ticket médio, taxa de conversão e total de vendas do mês atual, com comparação percentual em relação ao mês anterior.
- **Gráfico de Faturamento Mensal:** Análise da evolução da receita nos últimos 6 meses.
- **Faturamento por Loja:** Gráfico de pizza que mostra a contribuição de cada loja para a receita total.
- **Rankings de Desempenho:** Tabelas que classificam as lojas por faturamento e listam os dias de melhor e pior desempenho.

### 2. Desempenho Detalhado
Uma análise aprofundada dos dados operacionais com filtros interativos por loja e período:
- **Resumo de Indicadores Chave:** Comparação de KPIs (Vendas, Atendimentos, etc.) entre o período selecionado e um período anterior equivalente.
- **Gráficos de Evolução Diária:** Visualização da performance diária de atendimentos, vendas e faturamento.
- **Tabela Detalhada:** Dados diários brutos e calculados (ticket médio, taxa de conversão) para o período selecionado.

### 3. Análise Comparativa
Dashboards focados na comparação de desempenho entre o mês atual e o anterior:
- **Tabela Comparativa:** Comparação direta dos principais KPIs mensais.
- **Gráficos Comparativos:** Gráficos de barras que visualizam a diferença de faturamento, taxa de conversão e ticket médio entre os dois meses.

### 4. Cadastro e Configurações
Área de gerenciamento de dados:
- **Cadastro de Lojas:** Formulário para adicionar e editar lojas.
- **Registro de Dados Diários:** Formulário para inserir os dados operacionais de cada loja (atendimentos, vendas, valor).
- **Listas em Tempo Real:** Visualização imediata de lojas e registros cadastrados.
- **Botões de Ação Rápida:** Botões "Nova Loja" e "Novo Registro" para facilitar a entrada de dados.

---

## 🚀 Tecnologias Utilizadas

- **Frontend:** HTML5, CSS3, JavaScript (ES6 Modules)
- **Estilização:** [Tailwind CSS](https://tailwindcss.com/)
- **Gráficos:** [Chart.js](https://www.chartjs.org/)
- **Backend e Banco de Dados:** [Google Firebase](https://firebase.google.com/)
  - **Firestore:** Banco de dados NoSQL em tempo real para armazenar dados de lojas e registros diários.
  - **Firebase Authentication:** Para autenticação segura de usuários (anônima ou via token).

---

## 🔧 Como Executar Localmente

Como este é um projeto frontend puro que se conecta a um serviço de backend (Firebase), você pode executá-lo diretamente em um navegador.

1.  **Clone o repositório:**
    ```bash
    git clone [https://github.com/seu-usuario/seu-repositorio.git](https://github.com/seu-usuario/seu-repositorio.git)
    ```

2.  **Abra o arquivo `index.html`:**
    - Navegue até a pasta do projeto e abra o arquivo `index.html` em seu navegador de preferência (Chrome, Firefox, etc.).

### Configuração do Firebase

Para que a aplicação funcione com seus próprios dados, você precisará configurar um projeto no Firebase:

1.  **Crie um Projeto no Firebase:**
    - Acesse o [console do Firebase](https://console.firebase.google.com/).
    - Crie um novo projeto.
    - Na página do projeto, adicione um novo aplicativo Web (ícone `</>`).

2.  **Obtenha suas Chaves de Configuração:**
    - Após criar o aplicativo Web, o Firebase fornecerá um objeto de configuração `firebaseConfig`. Ele se parecerá com isto:
      ```javascript
      const firebaseConfig = {
        apiKey: "SUA_API_KEY",
        authDomain: "SEU_AUTH_DOMAIN",
        projectId: "SEU_PROJECT_ID",
        storageBucket: "SEU_STORAGE_BUCKET",
        messagingSenderId: "SEU_MESSAGING_SENDER_ID",
        appId: "SEU_APP_ID"
      };
      ```

3.  **Atualize o Código:**
    - No arquivo `index.html`, localize a linha de configuração do Firebase no script e substitua os valores de exemplo pelos do seu projeto:
      ```javascript
      // Linha a ser alterada
      const firebaseConfig = typeof __firebase_config !== 'undefined' ? JSON.parse(__firebase_config) : { apiKey: "SUA_API_KEY", authDomain: "SEU_AUTH_DOMAIN", projectId: "SEU_PROJECT_ID" };
      ```

4.  **Configure as Regras do Firestore:**
    - No console do Firebase, vá para **Firestore Database** > **Regras**.
    - Para permitir que usuários autenticados leiam e escrevam dados, utilize regras como estas (ajuste conforme sua necessidade de segurança):
      ```
      rules_version = '2';
      service cloud.firestore {
        match /databases/{database}/documents {
          // Permite acesso público aos dados na coleção 'public'
          match /artifacts/{appId}/public/data/{document=**} {
            allow read, write: if request.auth != null;
          }
        }
      }
      ```

5.  **Habilite a Autenticação:**
    - No console do Firebase, vá para **Authentication** > **Sign-in method**.
    - Habilite o provedor de login "Anônimo".

Com essas configurações, a aplicação estará conectada à sua própria instância do Firebase.
