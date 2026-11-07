<p align="center">
  <img src="assets/logo.png" width="96" alt="Logo do Oikos">
</p>

<h1 align="center">Oikos</h1>

<p align="center">
  <strong>Resíduo tem valor. Nós mostramos onde.</strong><br>
  Plataforma de economia circular de resíduos sólidos, feita no Brasil.
</p>

<p align="center">
  <a href="https://oikos.company">oikos.company</a> ·
  <a href="https://apps.apple.com/br/app/oikos-economia-circular/id6786017565">App Store</a> ·
  <a href="https://play.google.com/store/apps/details?id=com.oikos">Google Play</a>
</p>

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/mobile-screens-dark.jpg">
    <img src="assets/mobile-screens-light.jpg" alt="Telas do aplicativo Oikos" width="100%">
  </picture>
</p>

## O que é o Oikos

O Oikos conecta quem gera resíduo (moradores, empresas e órgãos públicos) a quem transforma esse resíduo em recurso: cooperativas, recicladoras, ecopontos e coletores. A ideia é tornar visível um mercado que já existe, mas que é difícil de encontrar, e dar à comunidade um jeito de cobrar o descarte correto.

- **Pontos de coleta e mercado.** Mapa de empresas e ecopontos com os resíduos que cada um aceita, horários de funcionamento e preço pago por quilo.
- **Denúncias ambientais.** Registro de descarte irregular com foto, vídeo e localização. A comunidade vota se a denúncia foi resolvida e a moderação acompanha o andamento.
- **Modo pesquisa.** Teste de usabilidade aplicado dentro do próprio aplicativo, usado na avaliação da dissertação de mestrado que originou o projeto.

## Repositórios

| Repositório | O que é | Stack principal |
|---|---|---|
| [**api**](https://github.com/oikos-circular-environment/api) | API REST, regras de negócio, autenticação, filas e armazenamento | Fastify, Prisma, PostgreSQL, Redis, MinIO |
| [**web**](https://github.com/oikos-circular-environment/web) | Site institucional e painel web para organizações e moderação | Next.js, Tailwind CSS, MapLibre |
| [**mobile**](https://github.com/oikos-circular-environment/mobile) | Aplicativo iOS e Android | Expo, React Native |
| [**survey**](https://github.com/oikos-circular-environment/survey) | Instrumento e painel do teste de usabilidade (ISO 9241-11) | Next.js, tRPC, Drizzle, MySQL |

Cada repositório tem no README como rodar localmente, a estrutura de pastas e a stack completa.

## Arquitetura

```mermaid
flowchart LR
  subgraph Clientes
    M["mobile<br/>Expo / React Native"]
    W["web<br/>Next.js"]
  end
  M -- "REST (oikos-sdk)" --> A["api<br/>Fastify"]
  W -- "REST (oikos-sdk)" --> A
  A --> P[("PostgreSQL")]
  A --> R[("Redis<br/>BullMQ")]
  A --> S[("MinIO<br/>S3")]
  A --> E["Resend<br/>e-mail"]
  M -- "tRPC (survey-api)" --> SV["survey<br/>Next.js + tRPC"]
  SV --> MY[("MySQL")]
  PQ["Pesquisador"] --> SV
```

O app e o painel web consomem a API pelo mesmo SDK, gerado a partir da especificação OpenAPI. O survey é um sistema à parte, com banco e autenticação próprios, que recebe os dados do modo pesquisa do app.

<table>
  <tr>
    <td width="50%">
      <picture>
        <source media="(prefers-color-scheme: dark)" srcset="assets/web-hero-dark.jpg">
        <img src="assets/web-hero-light.jpg" alt="Página inicial do oikos.company">
      </picture>
      <p align="center"><sub>oikos.company</sub></p>
    </td>
    <td width="50%">
      <picture>
        <source media="(prefers-color-scheme: dark)" srcset="assets/survey-hero-dark.jpg">
        <img src="assets/survey-hero-light.jpg" alt="Painel do teste de usabilidade">
      </picture>
      <p align="center"><sub>Painel do survey, com dados fictícios</sub></p>
    </td>
  </tr>
</table>

## Pesquisa

O Oikos nasceu de uma pesquisa de mestrado. A plataforma foi concebida a partir de um estudo com atores da cadeia de resíduos, e a usabilidade do aplicativo é avaliada com um teste autoaplicado que mede eficácia, eficiência e satisfação, seguindo a ISO 9241-11 e o método de Lima, Oliveira e Santana (2013). O instrumento e o cálculo dos indicadores estão no repositório [survey](https://github.com/oikos-circular-environment/survey).

## Registro e licença

O Oikos Economia Circular é registrado no INPI como programa de computador, processo BR 51 2026 008392-3.

<p align="center">
  <img src="assets/inpi-registro.png" width="683" alt="Dados do certificado de registro de programa de computador do Oikos no INPI">
</p>

O código de todos os repositórios é disponibilizado sob a [PolyForm Noncommercial 1.0.0](https://polyformproject.org/licenses/noncommercial/1.0.0). Qualquer pessoa pode estudar, usar, modificar e redistribuir o Oikos para fins não comerciais: uso pessoal, pesquisa, ensino e uso por instituições de ensino, organizações beneficentes, de pesquisa ou de proteção ambiental e órgãos públicos.

Uso comercial, como vender o software, oferecê-lo como serviço pago ou usá-lo como base de um produto, exige uma licença comercial à parte com o titular. Para tratar disso, escreva para christian.cesar@oikos.company.

## Como colaborar

Contribuições são bem-vindas em qualquer repositório:

1. Abra uma issue descrevendo o problema ou a proposta.
2. Crie uma branch a partir de `development` com o nome `<número-da-issue>-<descrição-curta>`, ou trabalhe a partir de um fork.
3. Use [Conventional Commits](https://www.conventionalcommits.org/pt-br/) e abra o pull request para `development`.
