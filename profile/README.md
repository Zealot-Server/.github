# Zealot

> Plataforma OpenTibia em desenvolvimento: mundo de jogo, cliente desktop, autenticação, portal web, ferramentas de mapa e automação de conteúdo.

O Zealot integra os componentes necessários para desenvolver e operar um mundo OpenTibia moderno. A plataforma mantém servidor, cliente, site e assets alinhados para que a jornada do jogador seja contínua: criar uma conta, fazer login, escolher o personagem e entrar no mundo.

## Serviços

| Serviço | Endereço |
| --- | --- |
| Site e portal da comunidade | [www.zealot.website](https://www.zealot.website) |
| API de login | `https://api.zealot.website/login` |
| Mundo de jogo | `game.zealot.website:7172` |

## Arquitetura

```text
Browser ──► www.zealot.website ──────────────► MyAAC
OTClient ─► api.zealot.website/login ─────────► login-server ─┐
OTClient ─► game.zealot.website:7172 ─────────► Canary ───────┼──► MariaDB
Remere's Map Editor ─► mapas e dados Cyclopedia ───────────────┘
```

## Repositórios

| Repositório | Responsabilidade |
| --- | --- |
| [canary](https://github.com/Zealot-Server/canary) | Servidor C++20/Lua: mundo, protocolos, datapack, scripts, mapa e persistência. |
| [otclient](https://github.com/Zealot-Server/otclient) | Cliente customizado C++/Lua: interface, login HTTP, efeitos, minimapa e assets 1511. |
| [login-server](https://github.com/Zealot-Server/login-server) | Serviço Go de autenticação HTTP/gRPC e lista de personagens. |
| [myaac-main](https://github.com/Zealot-Server/myaac-main) | Portal PHP/Twig: contas, personagens, administração, notícias, comunidade e loja. |
| [tibia-client](https://github.com/Zealot-Server/tibia-client) | Repositório de distribuição e ativos do cliente, mantido como fork. |

O workspace também integra o [Remere's Map Editor](https://github.com/opentibiabr/remeres-map-editor) para edição de mapas e exportação de dados da Cyclopedia.

## Em desenvolvimento

- progressão de XP configurável, gameplay e conteúdo do mundo;
- fluxo de Rookgaard, vocações e continente principal;
- login HTTP, gerenciamento de personagens e ciclo de exclusão/restauração;
- loja, moedas e integração entre servidor, cliente e portal;
- instalação e validação de assets do cliente por hash;
- releases e compatibilidade do cliente para macOS, Windows e Linux;
- minimapa, dados estáticos e exportação de mapa/superfície para a Cyclopedia;
- automação Lua para mapa e pipeline de itens customizados;
- monitoramento, CI/CD e implantação dos serviços.

## Desenvolvimento

O ambiente local usa Docker para levantar MariaDB, Canary, MyAAC e login-server juntos. O Canary, o portal e o login-server compartilham a mesma base; alterações de itens e assets são tratadas como mudanças coordenadas entre o servidor e o cliente.

Cada repositório contém sua própria documentação, requisitos de build e licença.
