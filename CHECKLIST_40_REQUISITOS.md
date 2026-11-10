# Checklist dos 40 requisitos — LOUD VALORANT (site estático de fã)

Legenda: ✅ aplicado no site · 🔧 faz você na hospedagem/antes de publicar · ➖ não se aplica (site sem backend, login, banco de dados ou pagamento)

| # | Requisito | Status | Como ficou |
|---|---|---|---|
| 1 | Autenticação segura | ➖ | Não há login. |
| 2 | Controle de acesso | ➖ | Não há áreas restritas. 🔧 Ative 2FA na conta da hospedagem. |
| 3 | Criptografia de dados | ➖ | Nenhum dado é guardado. Em trânsito: item 4. |
| 4 | HTTPS / TLS | ✅🔧 | CSP com `upgrade-insecure-requests`; `_headers` com HSTS. Publique só em host com HTTPS. |
| 5 | Hashing de senhas | ➖ | Não há senhas. |
| 6 | SQL injection | ➖ | Não há banco de dados. |
| 7 | XSS / CSRF | ✅ | CSP sem `unsafe-inline` em scripts (script e estilo liberados por hash), sem `eval`, links de matérias só aceitos se `https://`. CSRF: sem formulários nem sessões (`form-action 'none'`). |
| 8 | Rate limiting | 🔧 | Sem API. Cloudflare/Netlify já limitam abuso na borda. |
| 9 | Proteção de APIs | ➖ | Sem API (`connect-src 'none'`). |
| 10 | Auditoria de dependências | ✅ | Zero bibliotecas JS. Só fontes do Google Fonts (liberadas por domínio na CSP). |
| 11 | Política de privacidade | ✅ | Página #privacidade. |
| 12 | Bases legais | ✅ | Seção 3 da política (LGPD art. 7º). |
| 13 | Minimização de dados | ✅ | Site não coleta nada. |
| 14 | Finalidades documentadas | ✅ | Seção 3 da política. |
| 15 | Gestão de consentimento | ✅ | Sem cookies/rastreadores, logo sem banner necessário. Política diz que pedirá consentimento se isso mudar. |
| 16 | Política de cookies | ✅ | Seção 4 da política + aviso no rodapé. |
| 17 | Direitos dos titulares | ✅ | Seção 5 (art. 18 LGPD), canal por e-mail, resposta em 15 dias. |
| 18 | Exclusão de dados | ✅ | Seções 5 e 6, inclusive pedido de remoção de quem aparece no site. |
| 19 | Retenção de dados | ✅ | Seção 6 (e-mails apagados em até 6 meses). |
| 20 | Contratos com operadores | ✅🔧 | Seção 7 cita hospedagem e Google. Aceite o DPA/termos do seu provedor. |
| 21 | Termos de uso | ✅ | Página #termos. |
| 22 | Transparência de preços | ✅ | Termos, seção 5: preços (ex.: 2175 VP) são informativos e podem mudar. |
| 23 | Cobranças transparentes | ✅ | O site não cobra nada. Dito nos Termos. |
| 24 | Cancelamento de assinaturas | ✅ | Não há assinaturas. Dito nos Termos. |
| 25 | Política de reembolso | ✅ | Termos, seção 5: reembolso e arrependimento seguem as lojas oficiais. |
| 26 | Identificação do fornecedor | ✅🔧 | Nome e e-mail nas duas páginas legais. **Você precisa preencher** (ver abaixo). |
| 27 | Publicidade transparente | ✅ | Sem anúncios/afiliados. Removi `gclid`, `gbraid`, `gad_*`, `cplk` e `si` dos links (eram rastreadores de anúncio). |
| 28 | Depoimentos autênticos | ✅ | Não há depoimentos; Termos, seção 6. |
| 29 | Licenças de uso | ✅🔧 | Aviso de marcas da Riot/LOUD, licença das fontes (OFL) e canal de remoção. Veja o alerta sobre imagens abaixo. |
| 30 | Transparência sobre IA | ✅ | Termos, seção 4. |
| 31 | Backups automatizados | 🔧 | Guarde o projeto num repositório Git (GitHub); a hospedagem mantém o histórico de deploys. |
| 32 | Logs seguros | ✅🔧 | O site não registra nada. Logs da hospedagem: configure retenção curta. |
| 33 | Monitoramento de ameaças | 🔧 | Ative alertas/uptime e proteção da borda (ex.: Cloudflare). |
| 34 | Resposta a incidentes | ✅ | Política, seção 10. |
| 35 | Notificação de incidentes | ✅ | Política, seção 10 (ANPD e titulares, art. 48). |
| 36 | Testes de segurança | ✅ | Testei em navegador: 8 páginas, matéria aberta, links, CSP sem violações. 🔧 Rode também securityheaders.com após publicar. |
| 37 | Revisão de código | ✅ | Revisei o uso de `innerHTML` (só dados fixos do próprio código) e todos os links externos. |
| 38 | Privilégios administrativos | 🔧 | 2FA e senha forte no GitHub e na hospedagem; nenhuma chave no código. |
| 39 | Gestão de vulnerabilidades | ✅ | Canal em `.well-known/security.txt` (preencher e-mail) e política, seção 10. |
| 40 | Auditoria de conformidade | ✅ | Este checklist. Reveja a cada mudança no site. |

## Antes de publicar
1. **Preencha seus dados** no início do bloco `LEGAL` do `index.html` (`nome` e `email`). Enquanto vazio, as páginas legais mostram `[SEU NOME]` e `[SEU E-MAIL DE CONTATO]` em laranja. Use um e-mail dedicado ao site.
2. Preencha o e-mail em `.well-known/security.txt`.
3. Se usar Netlify ou Cloudflare Pages, suba a pasta inteira (o arquivo `_headers` ativa HSTS, `frame-ancestors`, etc.). Em GitHub Pages esse arquivo não vale, e o site fica protegido apenas pela CSP embutida.
4. Se editar o script ou o CSS do `index.html`, a CSP precisa dos novos hashes: o navegador bloqueia e o console diz o hash correto para colocar na tag `<meta http-equiv="Content-Security-Policy">` e no `_headers`.

## Pontos de atenção (juízo seu)
- **Imagens**: logos, fotos do elenco e imagens dos cosméticos são da LOUD/Riot ou de fotógrafos. Fan site sem fins lucrativos costuma ser tolerado, mas não é licença. Mantenha o site sem monetização (sem anúncios, doações ou venda) e atenda qualquer pedido de remoção.
- **Google Fonts**: carregar fontes do Google envia o IP do visitante ao Google (já informado na política). Para zerar isso, baixe as fontes e hospede junto do site.
- **Radar**: cita nomes e rumores sobre pessoas reais. Está rotulado como Oficial/Não oficial/Torcida, com fontes, e há canal de correção. Mantenha atenção a pedidos de remoção.
- Os textos legais são um modelo sólido, mas não substituem um advogado. Se um dia houver venda, doação ou anúncios, revise tudo.
