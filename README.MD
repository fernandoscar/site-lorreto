# ☕ Loretto Café — Refatoração Semântica e Acessível

Projeto acadêmico desenvolvido para a disciplina de **Desenvolvimento Web**, com o objetivo de refatorar o site real da [Loretto Café](https://loretto.com.br) aplicando boas práticas de **HTML Semântico**, **Acessibilidade (WCAG)** e **SEO**.

---

## 📋 Sobre o Projeto

O site original foi construído com WordPress + Elementor, que gera automaticamente centenas de `<div>` genéricas sem valor semântico. Este projeto reescreve toda a estrutura em HTML puro, mantendo o visual e o conteúdo originais, mas com código limpo, semântico e acessível.

---

## ✅ Missões Cumpridas

### 🟢 Missão 1 — Estrutura Base (2 pts)
Uso correto das tags estruturais principais:
- `<header>` — cabeçalho com logo e navegação
- `<main>` — envolve todo o conteúdo principal (único na página)
- `<footer>` — rodapé com endereço, links e copyright
- `<section>` — cada bloco temático da página
- `<aside>` — widget de acessibilidade (conteúdo complementar)

### 🟡 Missão 2 — Semântica (2 pts)
Substituição de todas as `<div>` genéricas por tags com significado:
- `<nav aria-label>` — navegação principal e do rodapé
- `<article>` — cada card de serviço e evento (conteúdo independente)
- `<section aria-labelledby>` — cada seção identificada pelo seu título
- `<blockquote>` — depoimentos/avaliações de clientes
- `<address>` — dados de contato no rodapé
- `<time datetime>` — marcação semântica de datas
- `<aside>` — painel de ferramentas de acessibilidade

### 🟠 Missão 3 — Acessibilidade (2 pts)
Implementação completa seguindo as diretrizes WCAG 2.1:
- Todas as `<img>` com atributo `alt` descritivo (corrigido bug do original: imagem de Confraternizações tinha `alt=""` vazio)
- Todos os campos de formulário com `<label for="id">` associado, incluindo `<select>` e `<input type="range">`
- `aria-required="true"` nos campos obrigatórios
- `aria-describedby` apontando para mensagens de erro de cada campo
- `aria-live="polite"` para anunciar confirmação do formulário
- `aria-live="assertive"` para anúncios do painel de acessibilidade
- `role="list"` nas listas de navegação
- `role="banner"` e `role="contentinfo"` no header e footer
- SVGs decorativos com `aria-hidden="true"`
- Navegação completa por teclado (Tab, Enter, Escape)

### 🔴 Missão 4 — SEO (1 pt)
- `<title>` descritivo e único
- `<meta name="description">` com resumo do conteúdo
- `<link rel="canonical">` para evitar conteúdo duplicado
- Open Graph (`og:title`, `og:description`, `og:image`) para redes sociais
- **Um único `<h1>`** na página (hero), seguido de `<h2>` em cada seção e `<h3>` nos cards — hierarquia correta
- `<time datetime="YYYY-MM-DD">` nas datas dos depoimentos

### 🏆 Missão 5 — Debug (3 pts)
Erros encontrados e corrigidos no código original:
1. `alt=""` vazio na imagem de Confraternizações — corrigido com descrição real
2. Todos os elementos eram `<div>` — substituídos por tags semânticas
3. Hierarquia de títulos quebrada no original — corrigida (H1 → H2 → H3)
4. Formulário sem `<label>` associado — corrigido com `for/id`
5. Nenhuma estrutura `<header>/<main>/<footer>` — adicionada corretamente

### ⭐ Missão Secreta — Bônus (1 pt)
Implementação dupla da missão secreta:
1. **Skip Link** — link "Pular para o conteúdo principal" visível ao pressionar Tab, que leva direto ao `<main>` (essencial para usuários de teclado e leitores de tela)
2. **`aria-live="polite"`** — região que anuncia automaticamente a confirmação de envio do formulário para tecnologias assistivas, sem interromper a leitura

---

## ♿ Painel de Acessibilidade

Widget flutuante no canto inferior direito com o símbolo internacional de acessibilidade (♿). Ao clicar, expande um painel com três ferramentas:

| Ferramenta | O que faz |
|---|---|
| 🌓 Alto Contraste | Alterna para esquema de cores de alto contraste (fundo preto, texto branco, amarelo) |
| A+ / A− | Aumenta ou diminui o tamanho da fonte em toda a página (salvo no `localStorage`) |
| 🌐 PT / EN | Traduz todo o conteúdo da página entre Português e Inglês |

**Detalhes técnicos do painel:**
- Implementado como `<aside>` semântico
- Abre/fecha com animação suave (`transform + opacity`)
- Fecha ao pressionar `Escape`
- Ao abrir, o foco vai automaticamente para o primeiro botão (acessibilidade por teclado)
- `aria-expanded` e `aria-controls` no botão gatilho
- Preferências salvas no `localStorage` (persistem ao recarregar)

---

## 🌐 Troca de Idioma (PT/EN)

Toda a página é traduzível entre Português e Inglês, incluindo:
- Navegação (header e footer)
- Hero (título, descrição, botões)
- Todos os cards de serviços e eventos
- Seção Sobre e Pet Friendly
- Formulário (labels, placeholders, botão)
- Depoimentos (texto e datas)
- Galeria e rodapé

A tradução é feita via JavaScript puro com um objeto de chave-valor mapeando cada `id` para seu texto em PT e EN. O atributo `lang` do `<html>` também é atualizado, o que permite que leitores de tela pronunciem o texto no idioma correto.

---

## 📝 Formulário com Validação Acessível

O formulário de agendamento implementa validação em dois níveis:

1. **HTML5 nativo** — atributos `required`, `type="email"`, `type="tel"`, `minlength` e `pattern` garantem validação mesmo sem JavaScript
2. **JavaScript acessível** — mensagens de erro personalizadas exibidas em `<span aria-live="polite">` abaixo de cada campo, anunciadas por leitores de tela; campos inválidos recebem `aria-invalid="true"` e borda vermelha; campos válidos recebem borda verde

---

## 🏗️ Estrutura do Projeto

```
loretto-cafe/
│
├── index.html       # Página principal (único arquivo)
└── README.md        # Este arquivo
```

Todo o CSS e JavaScript estão embutidos no `index.html` para facilitar a entrega e visualização sem servidor.

---

## 🗂️ Estrutura HTML da Página

```
<html lang="pt-BR">
  <head>
    <!-- SEO, meta tags, Open Graph, fontes -->
  </head>
  <body>
    <a class="skip-link">          <!-- ⭐ Missão Secreta: skip link -->
    <aside class="a11y-widget">    <!-- ♿ Painel de acessibilidade -->

    <header role="banner">
      <nav aria-label="Navegação principal">

    <main id="conteudo-principal">
      <section> <!-- Hero -->
      <section> <!-- Serviços -->
        <article> x4  <!-- Cards de serviço -->
      <section> <!-- Sobre / História -->
      <section> <!-- Pet Friendly -->
      <section> <!-- Espaços para Eventos -->
        <article> x4  <!-- Cards de evento -->
      <section> <!-- Agendamentos / Formulário -->
      <section> <!-- Galeria -->
      <section> <!-- Depoimentos -->
        <blockquote> x6  <!-- Avaliações -->

    <footer role="contentinfo">
      <address>  <!-- Dados de contato -->
      <nav aria-label="Links do rodapé">
```

---

## 🛠️ Tecnologias Utilizadas

- **HTML5** — estrutura semântica
- **CSS3** — variáveis CSS, Grid, Flexbox, animações, `clamp()` para tipografia responsiva
- **JavaScript vanilla** — painel de acessibilidade, troca de idioma, validação de formulário
- **Google Fonts** — [Josefin Sans](https://fonts.google.com/specimen/Josefin+Sans) + [Smooch](https://fonts.google.com/specimen/Smooch)
- **SVG inline** — logo e ícones sem dependências externas
- **[AOS v2.3.4](https://michalsnik.github.io/aos/)** — animações de entrada ao rolar a página (via CDN)
- **[SweetAlert2 v11](https://sweetalert2.github.io/)** — modais acessíveis e estilizados para feedback do formulário (via CDN)

---

## 📚 Referências

- [MDN Web Docs — HTML Semântico](https://developer.mozilla.org/pt-BR/docs/Glossary/Semantics)
- [WCAG 2.1 — Web Content Accessibility Guidelines](https://www.w3.org/TR/WCAG21/)
- [eMAG — Modelo de Acessibilidade em Governo Eletrônico](https://emag.governoeletronico.gov.br/)
- [W3C Validator](https://validator.w3.org/)
- [WAVE — Web Accessibility Evaluation Tool](https://wave.webaim.org/)
- [Google Search Central — Como o Google interpreta HTML](https://developers.google.com/search/docs/fundamentals/seo-starter-guide)
- [AOS — Animate On Scroll Documentation](https://michalsnik.github.io/aos/)
- [SweetAlert2 Documentation](https://sweetalert2.github.io/)

---

## 👨‍💻 Autor

Desenvolvido por **Fernando** — estudante de Engenharia de Software, 3º semestre.

Projeto acadêmico — Disciplina de Desenvolvimento Web.
