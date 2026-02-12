Product Requirements Document (PRD) - Tutu
1. Visão do Produto
O Tutu é um assistente financeiro pessoal "calm tech". Diferente de apps tradicionais focados em planilhas frias, o Tutu foca na prosperidade e na redução da ansiedade financeira. Ele utiliza metáforas de jardinagem (plantar, regar, florescer) e uma interface fluida para tornar o ato de cuidar do dinheiro prazeroso e sem julgamentos.
2. Público Alvo
Brasileiros que desejam organizar suas finanças mas sentem ansiedade ao abrir apps bancários.
Pessoas endividadas que precisam de estratégias claras de amortização.
Usuários que preferem interações visuais e conversacionais a tabelas estáticas.
3. Stack Tecnológico
Frontend: React (v19), TypeScript.
Estilização: Tailwind CSS (com configurações estendidas para bordas arredondadas extremas e animações customizadas).
Ícones: Lucide React.
Gráficos: Recharts.
IA/Backend: Google Gemini API (@google/genai) via gemini-2.5-flash-image (OCR) e gemini-3-flash-preview (Texto).
Persistência: LocalStorage (MVP/Client-side only).
4. Funcionalidades Principais
4.1. Experiência de Entrada (Onboarding)
Splash Screen: Animação complexa ("Gênese") onde o logo nasce de partículas de luz. Mensagens de carregamento contextuais e tranquilizadoras. Transição fluida (fade-out/zoom) para o login.
Login: Simulação de biometria e design emocional ("Prosperidade real").
4.2. Dashboard Principal
Resumo Visual: Card principal com saldo, receitas e despesas. Alerta visual de saúde financeira (cores Mint vs Rose).
Insights IA: Card "Dica do Tutu" que analisa o saldo e dívidas para dar conselhos contextualizados.
FAB (Floating Action Button): Botão expandível para "Digitar Manualmente" ou "Escanear/Subir Arquivo".
4.3. Gestão de Dívidas (Diferencial)
Cadastro Detalhado: Credor, Juros (Simples ou Composto/Price), Prazo, Data Base.
Lista Inteligente: Cálculo automático do comprometimento mensal e saldo devedor total.
Simulador de Amortização: Ferramenta que projeta a dívida no tempo (até 120 meses) e permite simular pagamentos extras para reduzir prazo ou valor da parcela.
4.4. Inteligência Artificial (Gemini)
OCR de Documentos: Capacidade de ler Imagens e PDFs de recibos/faturas. Extrai: Local, Valor, Data, Categoria e sugere lançamentos.
Chat Conversacional: Interface de chat para tirar dúvidas ou lançar gastos via texto natural.
Modal de Confirmação (Draft): Interface para o usuário validar os dados lidos pela IA antes de salvar, com detecção de duplicidade.
4.5. Relatórios e Exportação
Relatório Mensal: Gráficos de área (fluxo diário) e pizza (categorias). Cálculo de "Taxa de Poupança".
Exportação Pro: Geração de arquivos CSV formatados para o padrão brasileiro (PT-BR), divididos por Receitas, Despesas, Dívidas e Resumo (ideal para enviar a assessores/contadores).
5. Diretrizes de UI/UX (Motion Design)
Glassmorphism: Uso intenso de transparências, blur e bordas brancas sutis.
Geometria: Bordas extremamente arredondadas (rounded-[2.5rem]).
Animações: Tudo deve ter entrada suave (animate-fade-in-up), elementos flutuantes (animate-float) e feedbacks de clique (active:scale-95).
Cores:
Brand Indigo: #6366f1 (Foco, Info)
Brand Mint: #10b981 (Receita, Positivo, Broto)
Brand Slate: #0f172a (Texto, Base, Sofisticação)
Background: Mesh Gradients animados.
2. O Prompt Mestre (Para Geração do App)
Copie e cole este prompt em uma nova sessão para instruir uma IA a construir o Tutu exatamente como ele é agora.
code
Markdown
Atue como um Engenheiro Frontend Sênior e Especialista em UX/Motion Design. Sua tarefa é construir o "Tutu", um gerenciador financeiro pessoal web (React/TypeScript) focado em design emocional, inteligência artificial e gestão de dívidas.

### 1. Configuração do Projeto
- **Framework:** React + Vite (Use ES Modules).
- **Linguagem:** TypeScript.
- **Estilos:** Tailwind CSS (via CDN ou configuração local). Configure o tema para usar a fonte 'Inter' e cores personalizadas (Brand Indigo: #6366f1, Brand Mint: #10b981, Brand Slate: #0f172a).
- **Bibliotecas:** `lucide-react` (ícones), `recharts` (gráficos), `@google/genai` (IA).
- **Armazenamento:** LocalStorage (para persistência de dados no navegador).

### 2. Requisitos Visuais (Motion Design & Glassmorphism)
O app deve ser visualmente deslumbrante.
- Use um background com "Mesh Gradients" animados (bolhas de cor que se movem).
- Use o conceito de "Glassmorphism" (fundo branco translúcido, blur, bordas finas).
- Use bordas muito arredondadas (ex: `rounded-[2.5rem]`).
- Adicione animações de entrada (`fade-in-up`) em todos os modais e listas.
- Crie uma **Splash Screen** cinematográfica: O logo (um broto/sprout) deve "nascer" de uma luz, com partículas e mensagens de carregamento ("Semeando prosperidade...", "Regando sonhos...").

### 3. Funcionalidades Obrigatórias

#### A. Gemini AI Service (`geminiService.ts`)
- Implemente uma função `sendMessageToTutu` que aceita texto e arquivos (Base64).
- Use o modelo `gemini-2.5-flash-image` para imagens/PDFs (OCR) e `gemini-3-flash-preview` para texto.
- **System Prompt:** O Tutu deve extrair dados (Data, Valor, Local, Categoria, Forma de Pagamento) e retornar um JSON estrito.
- Deve suportar leitura de Notas Fiscais e Recibos.

#### B. Dashboard (`Dashboard.tsx`)
- Card principal gigante com o Saldo Atual.
- Cards menores para Total de Dívidas e Categorias principais.
- Card "Insight": Uma frase motivacional baseada no saldo atual.
- **FAB (Botão Flutuante):** No canto inferior direito, que expande para: "Digitar Manual" e "Escanear/Subir Arquivo".

#### C. Fluxo de Adição (`AddFlow.tsx`)
- Um wizard passo-a-passo (Tipo -> Valor -> Descrição -> Detalhes).
- Suporte para Receitas, Despesas e **Dívidas**.
- **Calculadora de Dívidas:** Ao adicionar uma dívida, solicite: Valor Total, Juros (%), Prazo (meses) e Tipo de Juros (Simples ou Composto). Calcule a parcela automaticamente.

#### D. Gestão de Dívidas (`DebtList.tsx` & `DebtEvolutionModal.tsx`)
- Liste as dívidas com cards visuais mostrando a parcela e o saldo devedor.
- Crie um **Simulador de Evolução**:
    - Mostre um gráfico ou lista projetando o saldo devedor mês a mês até a quitação.
    - Permita que o usuário simule uma "Amortização Extra" (pagar um valor a mais) e escolha entre "Reduzir Prazo" ou "Reduzir Parcela".

#### E. Chat (`App.tsx` - Tab Chat)
- Interface tipo WhatsApp/ChatGPT.
- O usuário pode enviar mensagens de texto ou fazer upload de arquivos pelo ícone de clipe/câmera.
- As respostas da IA devem ser processadas e, se contiverem transações, abrir o Modal de Confirmação.

#### F. Relatórios (`MonthlyReportModal.tsx` & `ExportModal.tsx`)
- Exiba gráficos de Área (fluxo diário) e Pizza (categorias) usando Recharts.
- Calcule a "Taxa de Poupança" do mês.
- Permita exportar os dados para CSV (formatado para Excel PT-BR).

### 4. Estrutura de Arquivos Recomendada
- `index.html` (com Tailwind CDN e Google Fonts)
- `App.tsx` (Orquestrador, roteamento por abas, lógica de estado global)
- `types.ts` (Interfaces para Transaction, Debt, AIResponse)
- `services/geminiService.ts` (Integração com Google GenAI)
- `components/`
    - `SplashScreen.tsx` (Animação de entrada)
    - `LoginScreen.tsx` (Tela de login fake com biometria)
    - `Dashboard.tsx`
    - `AddFlow.tsx`
    - `DebtList.tsx`
    - `DebtEvolutionModal.tsx`
    - `DraftConfirmationModal.tsx` (Para validar dados da IA)
    - `MonthlyReportModal.tsx`
    - `ExportModal.tsx`

### 5. Regras de Negócio Importantes
- Gastos são valores negativos, Receitas positivos.
- Dívidas têm status (Ativa, Paga, Atrasada) e prioridade.
- O app deve detectar duplicidade ao importar via IA (comparar valor, data e descrição).
- Use `Intl.NumberFormat` para formatar moeda em BRL (R$).

Gere o código completo, arquivo por arquivo, focando na excelência visual e na robustez da integração com a API do Gemini.


Criar o Tutu foi uma jornada que provou que a IA funciona melhor quando guiada por uma visão conceitual forte, e não apenas por instruções técnicas isoladas. O que funcionou excepcionalmente bem foi o refinamento prévio do PRD e das regras de negócio utilizando Copilot e GPT; essa etapa de "arquitetura" permitiu que, ao gerarmos o código, a IA já entendesse a "alma" do projeto (as metáforas de jardinagem, o tom de voz calmo e a estética glassmorphism), resultando em uma primeira versão visualmente muito mais madura e coesa do que o habitual.
Por outro lado, o que não funcionou como esperado foram as alucinações técnicas específicas: a IA frequentemente tropeça em versões de bibliotecas que mudam rápido (como o SDK do Google Gemini ou imports de ícones), exigindo intervenção humana para corrigir erros de build que a lógica pura não resolve. O maior aprendizado sobre conversar com a IA foi descobrir que ela responde incrivelmente bem a adjetivos e sentimentos no prompt. Ao pedir uma tela "maravilhosa", "cinematográfica" ou "sem julgamentos", a IA foi capaz de traduzir conceitos subjetivos em código concreto (animações de partículas, textos acolhedores), mostrando que o segredo de um bom prompt está em fornecer tanto a especificação técnica quanto a direção artística e emocional.
Quero criar um aplicativo de Organização de Finanças Pessoais que funcione por meio de conversas com o usuário.  
A ideia é facilitar o controle financeiro de forma simples e natural, sem formulários manuais ou planilhas complexas.

<img width="535" height="950" alt="image" src="https://github.com/user-attachments/assets/2fda822e-8821-49f5-87c4-acd150bfaf27" />
<img width="540" height="981" alt="image" src="https://github.com/user-attachments/assets/d555fc47-a7c8-4146-99d7-673751c139a0" />
<img width="537" height="940" alt="image" src="https://github.com/user-attachments/assets/e8ab37b1-5e46-4b25-8427-bb95d0e83b48" />
<img width="551" height="932" alt="image" src="https://github.com/user-attachments/assets/f18a6d73-30ae-44a7-8806-3a2e782c07bf" />
<img width="532" height="932" alt="image" src="https://github.com/user-attachments/assets/5f53aedf-d055-4171-8a74-9a476bb51917" />



