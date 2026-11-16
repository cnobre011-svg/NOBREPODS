# Indo para produção

O protótipo é uma página única. Para vender de verdade, falta:

1. **Backend e banco de dados** (Node + PostgreSQL/SQLite, por exemplo) para produtos, categorias, opções, pedidos e configurações. Substituir o *shim* de `index.html` por chamadas à API.
2. **Autenticação do administrador no servidor**: usuário e senha com hash (argon2/bcrypt), sessão segura e 2FA validada no servidor. A verificação TOTP atual roda no navegador.
3. **Permissões**: só o administrador autenticado pode criar, editar ou excluir dados. Validar todos os campos no servidor.
4. **Imagens**: armazenamento de arquivos (S3, Cloudinary ou disco) em vez de data URL.
5. **Pedidos**: gravar o pedido no servidor, com numeração sequencial, antes de abrir o WhatsApp.
6. **Pagamento** (opcional): integrar Pix/cartão (Mercado Pago, Stripe etc.).
7. **Conformidade**: avisos e controles exigidos pela lei para venda de bebidas alcoólicas (proibida para menores de 18 anos).
8. **Migração para React + TypeScript + Tailwind** com build (Vite), separando componentes: `ProductModal`, `Checkout`, `Admin`, `GroupsEditor`, `TwoFA`.
