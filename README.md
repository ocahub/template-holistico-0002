# template-holistico-0002

Template de site holístico da plataforma (atividade 00047), feito a partir do site
`andrezaastrologia`: o visual da Andreza Astrologia: marfim, vinho e coral, fotos em arco, roda do zodíaco e fases da lua (Cormorant Garamond e Jost).

Para lojas que **vendem** (módulos E-commerce e Holístico): o `template.json` pede
`sales:CreateProduct`, então ele não aparece para a imobiliária. A tenant escolhe o
template em **Loja › Site** e monta as páginas em **Editar páginas**: textos, imagens,
ordem das seções, páginas novas, cores e fontes. O build lê a versão **publicada** no
cloud-management.

## Como funciona

- **`template.json`**: o contrato com o painel e o cloud-management: as seções (campos,
  grupo, globais), as aparências (paletas e fontes), o conteúdo padrão de cada seção e
  as páginas prontas (Início, Sobre, Contato). Os textos padrão são genéricos.
- **`app/components/sections/`**: um componente por tipo de seção (`hero` →
  `SectionHero`). O mesmo catálogo de seções nos templates holísticos 0001 e 0002;
  muda o visual.
- **O que é dinâmico vem do `@ocahub/kit`**: a vitrine de produtos
  (`RhProductShowcase`, por tipo: sessões, mapas, produtos físicos, assinaturas), a
  conta e a sacola, o WhatsApp da loja, a faixa do mapa astral grátis (só quando a loja
  oferece a amostra) e todas as páginas da loja: `/loja`, produto, carrinho, checkout,
  conta, compras e `/mapa-astral`.
- **Variáveis da empresa** nos textos: `{empresa}`, `{whatsapp}`, `{telefone}`,
  `{email}`, `{endereco}`, `{registro}` e `{instagram}` (Loja › Dados da loja ›
  Contatos do site).
- **Botões**: o link é uma página do site (`/loja`, `/sobre`), outro site
  (`https://...`) ou, vazio, o WhatsApp da loja.

## Versão nova

Mude o `template.json` (e a `version`), faça o push e, no painel, **Plataforma ›
Templates de site › Ler template.json**. Seção nova: o componente em
`app/components/sections/` e a entrada em `sections` e `sectionDefaults`.

## Desenvolvimento

No dev, o cloud-management usa este clone (`dev/template-holistico-0002`, montado em
`/templates`) no lugar do GitHub. O robô `release-check/tests-dev/templates-holisticos.spec.ts`
publica a Bruxa (0001) e a Andreza (0002) com as páginas de hoje.
