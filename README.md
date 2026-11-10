<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/juditevendas-logo-dark.svg">
    <img src="assets/juditevendas-logo.svg" alt="JuditeVendas" width="420">
  </picture>
</p>

<p align="center">
  Agência digital: sites, landing pages, tráfego pago, conteúdo e rastreamento.<br>
  <a href="https://juditevendas.github.io">juditevendas.github.io</a>
</p>

## O que é

Site institucional da JuditeVendas **como agência digital** (frente 1 do plano de 90 dias). Por decisão dos sócios, ele não mostra produtos de afiliado: as contas COZ e TEC terão páginas de links próprias, com outra identidade.

São duas páginas estáticas em HTML e CSS, sem etapa de build, publicadas pelo GitHub Pages a partir da branch `main`:

- `index.html`: o site, com serviços, como trabalhamos, portfólio, para quem é, como cobramos, dúvidas e contato;
- `privacidade.html`: a Política de Privacidade (LGPD). Não tem JavaScript.

## Como editar

| O que mudar | Onde |
|---|---|
| WhatsApp, e-mail e Instagram | Objeto `CONFIG`, no `<script>` do fim do `index.html` |
| Textos e seções | Direto no `index.html`. Cada seção começa com um comentário, como `<!-- SOBRE -->` e `<!-- SERVIÇOS -->` |
| Cores | Variáveis no início do `<style>`: `--brand`, `--btn`, `--band-a` e as demais |
| Logos e ícone | Pasta `assets/` |

Depois de editar, faça commit e push na `main`. O GitHub Pages atualiza o site em cerca de um minuto.

Para ver no computador antes de subir, abra o `index.html` no navegador.

## Formulário de contato

O formulário não envia nada para servidor. Ele monta uma mensagem com os dados do visitante e abre o WhatsApp da JuditeVendas com o texto pronto. Enquanto `CONFIG.whatsapp` estiver vazio, a página só mostra a mensagem e o botão de copiar.

## Segurança (CSP)

O `<head>` tem uma Content-Security-Policy que só deixa rodar o script do fim da página, identificado pelo hash `sha256` dele no `script-src`. **Se o script mudar, o hash tem que mudar junto**, senão o JavaScript para de funcionar: o menu, o carrossel e o formulário deixam de responder.

Para gerar o hash novo, rode na pasta do repo:

```
python -c "import re,hashlib,base64;s=re.search(r'<script>(.*?)</script>',open('index.html',encoding='utf-8').read(),re.S).group(1);print(base64.b64encode(hashlib.sha256(s.encode()).digest()).decode())"
```

Outra forma é abrir a página com o hash antigo e ver o console do navegador (F12). O erro de CSP mostra o hash esperado.

Ao adicionar o Pixel da Meta, libere `https://connect.facebook.net` no `script-src` e `https://www.facebook.com` no `img-src` e no `connect-src`. O token da API de Conversões **nunca** entra neste repo, porque ele é público.

## Pendências

- [ ] Preencher WhatsApp, e-mail e Instagram no `CONFIG` e o e-mail e o CNPJ na `privacidade.html`
- [ ] Confirmar os compromissos que estão no ar: diagnóstico em 48h, proposta por escrito, relatório semanal nos serviços de tráfego, sem fidelidade nos mensais. O "site em 7 dias" saiu porque ninguém confirmou o prazo
- [ ] Confirmar na Política de Privacidade o prazo de guarda dos contatos que não viraram cliente (está 12 meses)
- [ ] Portfólio: trocar os 3 cartões "vão aparecer aqui" por projetos reais, com autorização de cada cliente
- [ ] Opcional: página de Termos de Uso (o plano de 90 dias cita)
- [ ] Opcional: domínio próprio, com arquivo `CNAME` e ajuste de DNS
