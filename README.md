# Loja Adega

Loja online *mobile-first* para adega (vinhos e destilados): catálogo com destaques, categorias, promoções, tela de produto com opções personalizáveis, carrinho e **pedido enviado por WhatsApp**, sem cadastro de cliente. Inclui painel administrativo com verificação em duas etapas (TOTP).

> **Aviso:** use apenas com produtos de venda legal. A venda de bebidas alcoólicas é proibida para menores de 18 anos, e a de cigarros eletrônicos é proibida no Brasil. Verificar as exigências legais é responsabilidade de quem opera a loja.

## Recursos

- Cabeçalho fixo com menu de categorias, busca e carrinho; menu inferior fixo (Início, Promoções, Pedidos, Perfil).
- Destaques com rolagem horizontal; preço riscado e % de desconto automáticos.
- Tela de produto: foto ampliável, grupos de opções (obrigatório/opcional, mínimo/máximo, adicionais com preço, busca), quantidade e observações.
- Carrinho com itens separados por combinação de opções.
- Checkout sem login: gera a mensagem do pedido e abre o WhatsApp da loja.
- Painel em `#admin`: produtos, categorias, promoções, pedidos, configurações (WhatsApp, taxa e prazo de entrega).
- 2FA por aplicativo autenticador (Google/Microsoft Authenticator).

## Como rodar

```bash
git clone <URL-DO-SEU-REPOSITORIO>
cd loja-adega
python3 -m http.server 8080      # ou: npm start
```

Abra `http://localhost:8080` (loja) e `http://localhost:8080/#admin` (painel).

### Modo local x claude.ai

O código usa `claude.use('db' | 'user' | 'assets')`, que existe quando a página é publicada como Artifact no claude.ai (banco compartilhado, permissões no servidor e upload de imagens). Fora de lá, um *shim* no início do `index.html` simula essas APIs com `localStorage`:

- os dados ficam **só no navegador** de cada pessoa;
- **não há autenticação real**: quem abrir `#admin` entra (a 2FA é apenas uma camada local);
- fotos são salvas como data URL e podem estourar a cota do navegador.

Serve para demonstração e desenvolvimento. Para produção, troque o shim por um backend real.

## Configuração

No `index.html`:

| Constante | Função |
|---|---|
| `WA_DEFAULT` | WhatsApp da loja (55 + DDD + número) |
| `FINAL` | `true` esconde o link "Área do proprietário" no Perfil |

O WhatsApp, a taxa e o prazo de entrega também podem ser editados no painel (aba **Loja**).

## Publicar no GitHub Pages

1. Crie o repositório no GitHub e envie os arquivos:
   ```bash
   git init
   git add .
   git commit -m "Loja Adega: versão inicial"
   git branch -M main
   git remote add origin https://github.com/SEU-USUARIO/loja-adega.git
   git push -u origin main
   ```
2. Em **Settings → Pages**, escolha a branch `main` e a pasta `/ (root)`.
3. Acesse `https://SEU-USUARIO.github.io/loja-adega/`.

## Próximos passos para produção

Ver [docs/PRODUCAO.md](docs/PRODUCAO.md).

## Licença

MIT.
