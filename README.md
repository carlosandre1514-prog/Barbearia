# Agenda Barba

Site de agendamento para barbearias, salões, manicures, maquiagem e estúdios.
Login com **Firebase Auth**, dados no **Firestore**, fotos pelo **ImageKit**.

## Arquivos
- `index.html`: o site inteiro (cliente, empresa e administrador).
- `firestore.rules`: regras de segurança. **Publique antes de testar** (Firestore → Regras).
- `assets/banner.jpg`: banner da home (1200 x 480 px, opcional).

## Configurar o Firebase (uma vez)
1. Authentication → Método de login → ativar **E-mail/senha**.
2. Firestore Database → criar banco → copiar o conteúdo de `firestore.rules` em **Regras** → Publicar.
3. Authentication → Configurações → Domínios autorizados → adicionar `SEU-USUARIO.github.io`.
4. **Criar o administrador:**
   - Authentication → Usuários → Adicionar usuário (e-mail e senha do admin). Copie o **UID**.
   - Firestore → coleção `users` → documento com ID = o UID → campos:
     `nome` (string), `email` (string), `role` = `admin` (string).

## Como funciona
- Cliente: cria a própria conta em Entrar → Criar conta.
- Empresa: o admin cria o login em ADM → Empresas → Nova empresa. A empresa pode pedir redefinição de senha por e-mail.
- O pedido nasce pendente; só vira horário ocupado quando a empresa confirma.
- A duração do serviço não bloqueia o pedido; a empresa decide ao confirmar.
- Pagamento no local; cada empresa escolhe as formas aceitas.

## Fotos (ImageKit)
O `index.html` já aponta para o assinador (Cloudflare Worker `agenda-assinador`), na linha `const IK={signer:"..."}`.
O assinador deve responder JSON com `publicKey`, `signature`, `expire` e `token`.
Se o campo ficar vazio, o envio de fotos fica desligado.

## Testar
O site usa módulos: não abre com duplo clique (`file://`). Teste no GitHub Pages ou com um servidor local.

## Ainda falta
- Avisos por WhatsApp e notificação de pedido novo.
- Editar nome/endereço da empresa depois de criada.
- Profissionais por empresa e remarcação pelo cliente.
