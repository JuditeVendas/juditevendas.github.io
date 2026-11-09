<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/juditevendas-logo-dark.svg">
    <img src="assets/juditevendas-logo.svg" alt="JuditeVendas" width="420">
  </picture>
</p>

<p align="center">
  Anúncios, site e relatório semanal para negócios locais.<br>
  <a href="https://juditevendas.github.io">juditevendas.github.io</a>
</p>

## O que é

Site institucional da JuditeVendas. É uma página estática em HTML, CSS e JavaScript, sem etapa de build, publicada pelo GitHub Pages a partir da branch `main`.

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

- [ ] Preencher WhatsApp, e-mail e Instagram no `CONFIG`
- [ ] Revisar os compromissos da faixa de números: diagnóstico em 48h, site em 7 dias, 1 relatório por semana, sem fidelidade
- [ ] Trocar a seção "Para quem é" ou somar depoimentos reais quando houver clientes
- [ ] Opcional: domínio próprio, com arquivo `CNAME` e ajuste de DNS
