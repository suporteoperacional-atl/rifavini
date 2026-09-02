# Rifa Solidária — MacBook Air M1

Sistema completo: site público (comprador escolhe pacote, paga PIX, anexa comprovante) + painel seu (você aprova o pagamento e o sistema gera os números e manda por e-mail automaticamente). Sem custo — usa Google Sheets, Apps Script e GitHub Pages.

## Passo 1 — Criar a planilha
1. Crie uma planilha nova no Google Sheets, ex: **"Rifa Macbook"**.
2. Renomeie a primeira aba para **Pedidos**.
3. Na linha 1, cole exatamente estes cabeçalhos (uma coluna cada):
   ```
   ID | DataHora | Nome | Contato | Email | Pacote | Qtd | Valor | ComprovanteURL | Status | Numeros | DataAprovacao
   ```

## Passo 2 — Publicar o backend (Apps Script)
1. Na planilha: **Extensões > Apps Script**.
2. Apague o conteúdo do arquivo `Código.gs` padrão e cole o conteúdo do arquivo **Código.gs** deste pacote.
3. No topo do arquivo, ajuste:
   - `SENHA_ADMIN` → coloque uma senha só sua para o painel.
4. Clique em **Implantar > Nova implantação**.
   - Tipo: **App da Web**
   - Executar como: **Eu** (seu e-mail)
   - Quem pode acessar: **Qualquer pessoa**
5. Autorize as permissões (Gmail e Drive) quando pedir.
6. Copie a **URL do App da Web** gerada (termina em `/exec`) — você vai usá-la nos dois arquivos HTML.

## Passo 3 — Configurar os arquivos do site
Abra `index.html` e `admin.html` e troque:
- `COLE_AQUI_A_URL_DO_APP_DA_WEB` → pela URL copiada no passo anterior (nos dois arquivos).

No `index.html`, troque também:
- `CHAVE_PIX_AQUI` → sua chave PIX
- `NOME_COMPLETO_AQUI` → nome do favorecido do PIX

## Passo 4 — Publicar no GitHub Pages
1. Crie um repositório novo no GitHub (pode ser público).
2. Suba `index.html` e `admin.html` para a raiz do repositório.
3. Em **Settings > Pages**, escolha a branch `main` e pasta `/root`.
4. O GitHub gera um link tipo `https://seuusuario.github.io/rifa-macbook/`.
   - Divulgue **esse link** (abre `index.html`) para quem vai comprar.
   - Você acessa `https://seuusuario.github.io/rifa-macbook/admin.html` para validar os pagamentos.

## Como funciona no dia a dia
1. Comprador escolhe o pacote, faz o PIX manualmente e anexa o comprovante no site.
2. O pedido cai como **"Pendente"** na sua planilha, com o comprovante salvo automaticamente numa pasta do seu Google Drive chamada **"Comprovantes Rifa Macbook"**.
3. Você abre `admin.html`, digita sua senha, vê a lista de pedidos pendentes com o comprovante.
4. Confirmou que o PIX caiu na sua conta → clica **"Aprovar e enviar números"**.
   - O sistema sorteia números de 4 dígitos (0000–9999) que **nunca se repetem** entre os compradores já aprovados.
   - Envia um e-mail automático pro comprador com os números e o "comprovante de participação".
5. Se o comprovante for falso/inválido, clique **"Rejeitar"**.

## Observações importantes
- A validação do PIX continua manual (olhando seu extrato/app do banco) — o sistema só automatiza a geração de números e o envio de e-mail depois que você aprova.
- Os e-mails são enviados a partir da sua conta Google (Gmail grátis tem limite de ~100 e-mails/dia, mais que suficiente para uma rifa).
- Guarde a URL do painel (`admin.html`) só para você — a senha é a única proteção.
- Você pode acompanhar tudo a qualquer momento direto na planilha, incluindo quem já pagou e quais números cada pessoa tem.
