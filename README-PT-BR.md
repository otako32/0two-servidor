# 0TWO — starter para ligar uma IA real ao GitHub Pages

Este pacote contém um servidor Node.js para a API e um exemplo de integração para o frontend. Ele **não foi publicado nem conectado automaticamente** ao repositório.

## 1. Criar a chave da API
- Acesse https://platform.openai.com/api-keys
- Crie uma chave e guarde-a em segredo.
- A API pode ter cobrança separada do ChatGPT.
- Nunca cole a chave no HTML, no JavaScript do frontend, em mensagens ou no GitHub.

## 2. Publicar o servidor (exemplo: Render ou outro host Node)
1. Envie a pasta `server` para um repositório privado ou para o repositório do projeto.
2. Crie um serviço Web Node no host escolhido, usando a pasta `server` como raiz.
3. Build command: `npm install`
4. Start command: `npm start`
5. Configure variáveis de ambiente no painel do host:
   - `OPENAI_API_KEY` = sua chave secreta
   - `ALLOWED_ORIGIN` = `https://10062011brr.github.io`
   - `PORT` geralmente é fornecida pelo host.
6. Depois de publicar, teste `https://SUA-URL/health`. Deve retornar `{"ok":true,"service":"0TWO AI API"}`.

## 3. Conectar o frontend
- Copie `frontend/otwo-api.js` para a pasta publicada pelo GitHub Pages.
- Troque `https://COLOQUE-A-URL-DO-SEU-SERVIDOR` pela URL HTTPS real do servidor.
- Inclua no HTML: `<script src="./otwo-api.js"></script>`.
- No manipulador do formulário de chat, substitua a resposta simulada por uma chamada a `askOtwo(texto)`, e mostre o texto retornado na interface. Como não tenho o código atual do repositório, essa troca precisa ser ajustada ao nome das funções e elementos do seu HTML.

Exemplo genérico:
```js
try {
  const reply = await askOtwo(textoDigitado);
  addMessage("0TWO", reply);
} catch (err) {
  addMessage("0TWO", err.message);
}
```

## 4. Testar no celular e notebook
Abra o mesmo endereço HTTPS do GitHub Pages nos dois dispositivos. O histórico deste exemplo usa `localStorage`, portanto **não sincroniza entre dispositivos**. Para sincronização real será necessário adicionar login e um banco de dados ao servidor.

## Limitações importantes
- O pacote não integra Firefox embutido, VPN, geração de imagem ou geração de vídeo.
- O código de acesso do HTML é apenas uma trava visual, não autenticação segura.
- Adicione rate limiting e autenticação antes de expor publicamente o endpoint para evitar uso indevido e custos inesperados.
- A origem CORS deve ser ajustada para o domínio exato do site publicado.
