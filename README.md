# Landing Page - Blinzador

Este projeto é uma landing page de alta conversão, totalmente responsiva, desenvolvida para o produto "Blinzador". A página foi construída com foco em performance e experiência do usuário, utilizando tecnologias modernas de front-end.

## ✨ Visão Geral

A página apresenta um produto para tratamento de fungos nas unhas, com uma estrutura clássica de VSL (Video Sales Letter). Ela é projetada para guiar o usuário através de uma narrativa em vídeo, revelando as ofertas e informações adicionais em um momento estratégico para maximizar a conversão.

## 🚀 Funcionalidades Principais

- **Design Responsivo**: Layout adaptado para uma visualização otimizada em desktops, tablets e dispositivos móveis.
- **Integração com Player de Vídeo**: Utiliza o `vturb-smartplayer` para exibir o vídeo de vendas principal.
- **Exibição de Conteúdo Sincronizada**: As seções de ofertas, garantia e FAQ são reveladas dinamicamente após um tempo determinado (`pitchTime`), que é configurado no player de vídeo.
- **Fallback Timer**: Caso o player de vídeo falhe ou não defina um `pitchTime`, um temporizador de segurança garante que o conteúdo seja exibido após um curto período, evitando que o usuário fique com uma página em branco.
- **Componentes Interativos**:
  - **FAQ Accordion**: Seção de perguntas frequentes interativa, onde as respostas se expandem e se recolhem ao clique.
  - **Contador Regressivo**: Um timer de escassez é exibido na versão mobile para criar urgência.
- **Animações Sutis**: Animações de entrada (`fade-in`) para uma aparição suave do conteúdo.
- **Otimizações de Carregamento**: Uso de `preload` e `dns-prefetch` para acelerar o carregamento de recursos críticos (scripts e imagens do player).

## 🛠️ Tecnologias Utilizadas

- **HTML5**: Estrutura semântica do conteúdo.
- **Tailwind CSS**: Framework CSS utility-first para uma estilização rápida e responsiva, carregado via CDN.
- **CSS3**: Estilos personalizados e animações (`@keyframes`) para componentes como o FAQ e o efeito de brilho.
- **JavaScript (Vanilla)**: Manipulação do DOM e lógica de interatividade, incluindo:
  - Event Listeners (`DOMContentLoaded`, `player:ready`).
  - Funções assíncronas para carregamento de scripts.
  - Lógica para o contador regressivo e o accordion do FAQ.

## 📂 Estrutura de Arquivos

```
front/
├── assets/
│   ├── png/
│   │   ├── bandeiras.png
│   │   ├── botao-carrinho.png
│   │   ├── exemplo-uso.png
│   │   ├── frasco-1.png
│   │   ├── grid.png
│   │   ├── hero.png
│   │   ├── kit-02-garantia.png
│   │   ├── kit-03.png
│   │   ├── kit-06.png
│   │   └── som.png
│   └── svg/
│       ├── angulo-pequeno-direito.svg
│       ├── carrinho-compras.svg
│       ├── check-verde.svg
│       ├── circulos.svg
│       ├── elipse.svg
│       └── estrelas.svg
└── index.html
```

- `index.html`: O único arquivo HTML que contém toda a estrutura, estilos e scripts da página.
- `assets/`: Pasta que armazena todos os recursos visuais (imagens PNG e vetores SVG).

## ⚙️ Como Executar

Como este é um projeto de front-end estático que utiliza CDNs, não há necessidade de um processo de build complexo.

1.  Clone este repositório.
2.  Abra o arquivo `index.html` diretamente em um navegador de sua preferência (Google Chrome, Firefox, etc.).

> **Nota**: Para uma melhor experiência e para evitar possíveis problemas de CORS com o carregamento de assets, é recomendado servir os arquivos através de um servidor local. Uma maneira fácil de fazer isso é usando a extensão **Live Server** no Visual Studio Code.

## 📜 Análise do Código

### CSS

A maior parte da estilização é feita com as classes utilitárias do **Tailwind CSS**. No entanto, uma tag `<style>` no `<head>` é utilizada para:
- **Estilos Globais**: `scroll-behavior: smooth;`.
- **Animações**: A animação `fadeSlideDown` para a exibição do conteúdo com `data-delay`.
- **Componentes Customizados**: Estilos para o funcionamento do FAQ accordion (`.faq-item`, `.faq-answer`).
- **Media Queries**: Lógica específica para exibir/ocultar o vídeo em desktop e o timer em mobile.

### JavaScript

Todo o código JavaScript está contido em blocos `<script>` no final do `<body>`. A lógica principal é encapsulada dentro de um listener de evento `DOMContentLoaded` para garantir que o DOM esteja totalmente carregado antes da execução.

1.  **Lógica `data-delay`**:
    - Um `setTimeout` (`fallbackTimer`) é iniciado para garantir que o conteúdo oculto (`[data-delay]`) apareça após `1800ms`, caso o player de vídeo falhe.
    - O script aguarda o evento `player:ready` do componente `vturb-smartplayer`.
    - Ao receber o evento, ele verifica se `p.data.config.pitchTime` existe.
    - Se existir, o `fallbackTimer` é cancelado e a função `p.displayHiddenElements()` do player é usada para exibir o conteúdo no tempo exato do pitch.
    - Se não existir, o fallback continua ativo.

2.  **Contador Regressivo**:
    - Localiza o elemento `#countdown-timer`.
    - Utiliza `setInterval` para decrementar o tempo a cada segundo e atualizar o texto na tela.

3.  **FAQ Accordion**:
    - Adiciona um listener de clique a cada `.faq-question`.
    - Ao clicar, ele alterna a classe `.active` no elemento pai `.faq-item`, que, por sua vez, aciona as transições de CSS para exibir ou ocultar a resposta.

4.  **Botões**:
    - Um listener de clique genérico é adicionado a todos os botões (exceto os do player de vídeo) para exibir um alerta `alert('Function not yet implemented')`, servindo como um placeholder para a funcionalidade de checkout.