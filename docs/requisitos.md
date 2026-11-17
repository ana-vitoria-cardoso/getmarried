# Documento de Requisitos — GetMarried.com

| Campo | Valor |
|---|---|
| Projeto | GetMarried.com |
| Versão do documento | 0.1 (rascunho) |
| Data | 17/11/2026 |
| Autora | Ana Vitória Cardoso Queiroz |
| Status | Em revisão |

## 1. Visão geral

O GetMarried.com é uma aplicação web que apoia os noivos na organização do casamento, reunindo em um só lugar as informações do evento, a lista de presentes com reserva e a confirmação de presença dos convidados.

**Objetivos**
- Evitar que os noivos recebam presentes repetidos.
- Centralizar as confirmações de presença, incluindo acompanhantes e crianças.
- Permitir que o convidado se identifique uma única vez.
- Oferecer um assistente de IA para dúvidas dos convidados e consultas dos noivos.

## 2. Atores

| Ator | Descrição |
|---|---|
| Convidado | Pessoa convidada que acessa o app para ver informações, reservar presente e confirmar presença |
| Noivos (administradores) | Gerenciam a lista de presentes e acompanham reservas e confirmações |
| Assistente de IA | Componente automatizado que responde perguntas e sugere presentes |

## 3. Requisitos funcionais

### 3.1 Acesso e identificação
| ID | Requisito | Prioridade |
|---|---|---|
| RF01 | O convidado deve se identificar uma única vez, informando nome e telefone | Alta |
| RF02 | O sistema deve manter o convidado identificado nas demais telas, sem pedir os dados novamente | Alta |
| RF03 | O convidado deve poder sair da sessão | Média |
| RF04 | Os noivos devem acessar o painel administrativo com credenciais próprias | Alta |

### 3.2 Informativos do casamento
| ID | Requisito | Prioridade |
|---|---|---|
| RF05 | O sistema deve exibir data, local, horário e observações do casamento | Alta |
| RF06 | O sistema deve exibir fotos do casal | Média |
| RF07 | O app deve ter um menu lateral (aba vertical) para navegar entre as telas | Alta |

### 3.3 Lista de presentes
| ID | Requisito | Prioridade |
|---|---|---|
| RF08 | O sistema deve listar os presentes com nome, valor estimado e status (disponível ou reservado) | Alta |
| RF09 | Cada presente disponível deve ter um link que abre uma busca na web pelo produto | Alta |
| RF10 | O convidado deve poder ordenar os presentes por preço, do menor para o maior e vice-versa | Alta |
| RF11 | O convidado deve poder informar quanto pretende gastar, e o sistema deve filtrar os presentes dentro desse valor com margem de variação para mais e para menos | Alta |
| RF12 | O convidado deve poder reservar um presente disponível | Alta |
| RF13 | Antes de concluir a reserva, o sistema deve exibir uma caixa de confirmação informando que o presente ficará exclusivo do convidado e indisponível para os demais | Alta |
| RF14 | Presente reservado deve aparecer como "reservado" e **sem link** para os demais convidados | Alta |
| RF15 | O sistema deve impedir que dois convidados reservem o mesmo presente, inclusive em acessos simultâneos | Alta |
| RF16 | O convidado deve poder cancelar a própria reserva, devolvendo o presente à lista | Média |
| RF17 | O sistema deve registrar o convidado e o presente reservado, usando os dados do login | Alta |
| RF18 | Os noivos devem poder cadastrar, editar e remover presentes da lista | Alta |

### 3.4 Confirmação de presença
| ID | Requisito | Prioridade |
|---|---|---|
| RF19 | O convidado deve confirmar presença sem digitar novamente nome e telefone (vêm do login) | Alta |
| RF20 | O convidado deve informar o nome de cada acompanhante da sua família | Alta |
| RF21 | Para cada acompanhante, o convidado deve indicar se é criança menor de 10 anos e, em caso afirmativo, informar a idade | Alta |
| RF22 | O convidado deve poder editar ou cancelar sua confirmação | Média |

### 3.5 Painel dos noivos e exportação
| ID | Requisito | Prioridade |
|---|---|---|
| RF23 | Os noivos devem visualizar todas as reservas (convidado e presente) | Alta |
| RF24 | Os noivos devem visualizar todas as confirmações com seus acompanhantes | Alta |
| RF25 | O sistema deve calcular automaticamente o total de adultos e de crianças confirmados | Média |
| RF26 | O sistema deve exportar reservas e confirmações em arquivo Excel (`.xlsx`) | Alta |

### 3.6 Inteligência artificial
| ID | Requisito | Prioridade |
|---|---|---|
| RF27 | O assistente deve responder dúvidas dos convidados com base nas informações cadastradas do casamento | Alta |
| RF28 | O assistente deve sugerir presentes da lista conforme orçamento e estilo informados pelo convidado | Média |
| RF29 | O painel dos noivos deve ter um assistente que responde perguntas sobre reservas e confirmações consultando o banco de dados | Média |

## 4. Regras de negócio

| ID | Regra |
|---|---|
| RN01 | Um presente só pode ter uma reserva ativa por vez |
| RN02 | Ao cancelar uma reserva, o presente volta a ficar disponível para todos |
| RN03 | Considera-se criança a pessoa com menos de 10 anos; para ela a idade é obrigatória |
| RN04 | Os acompanhantes pertencem à confirmação do convidado titular; eles não têm login próprio |
| RN05 | Cada convidado possui uma única confirmação de presença |
| RN06 | O assistente de IA só responde com base nas informações do casamento e nos dados autorizados; quando não souber, deve dizer que não sabe |
| RN07 | O valor estimado do presente é informado manualmente pelos noivos |

## 5. Requisitos não funcionais

| ID | Categoria | Requisito |
|---|---|---|
| RNF01 | Usabilidade | Interface simples e legível, pensada também para pessoas com pouca familiaridade com tecnologia |
| RNF02 | Responsividade | Funcionar bem em celulares, já que o acesso será principalmente por link no WhatsApp |
| RNF03 | Segurança | Chaves de API e senhas somente em variáveis de ambiente (`.env`), nunca no repositório |
| RNF04 | Segurança | Validar todos os dados recebidos e proteger o painel dos noivos por autenticação |
| RNF05 | Segurança | Usar HTTPS na publicação |
| RNF06 | Privacidade | Seguir a LGPD: coletar apenas o necessário e informar a finalidade (ver `docs/lgpd.md`) |
| RNF07 | Integridade | O banco deve garantir a unicidade da reserva ativa por presente (restrição no MySQL) |
| RNF08 | Portabilidade | Executar com Docker Compose em um único comando |
| RNF09 | Manutenibilidade | Código organizado em módulos, com testes automatizados nas regras principais |
| RNF10 | Documentação | Documentação mantida em `docs/` e atualizada a cada etapa |
| RNF11 | IA | Respostas do assistente com tempo aceitável e mensagem de erro amigável se o serviço de IA estiver indisponível |
| RNF12 | Dados de exemplo | O repositório público deve conter somente dados fictícios |

## 6. Histórias de usuário

**HU01 — Identificação única**
Como convidado, quero me identificar uma vez para não precisar repetir meus dados a cada ação.
- *Dado* que informei nome e telefone, *quando* reservo um presente ou confirmo presença, *então* o sistema usa meus dados sem pedir de novo.

**HU02 — Ver informações do casamento**
Como convidado, quero ver data, local, horário, observações e fotos para me organizar.
- *Dado* que estou logado, *quando* abro a tela inicial, *então* vejo todas essas informações e o menu lateral.

**HU03 — Filtrar presentes pelo meu orçamento**
Como convidado, quero informar quanto pretendo gastar para ver só os presentes compatíveis.
- *Dado* que informei R$ 200, *quando* aplico o filtro, *então* vejo os presentes dentro desse valor com a margem de variação definida.

**HU04 — Reservar presente**
Como convidado, quero reservar um presente para que ninguém mais o compre.
- *Dado* um presente disponível, *quando* clico em reservar, *então* aparece a caixa de confirmação explicando a exclusividade.
- *Dado* que confirmei, *então* o presente fica reservado para mim e os demais convidados o veem como indisponível, sem link.

**HU05 — Evitar reserva duplicada**
Como noivo, quero que dois convidados não consigam reservar o mesmo item para não receber presentes repetidos.
- *Dado* que dois convidados tentam reservar ao mesmo tempo, *então* apenas um consegue e o outro recebe aviso de que o item foi reservado.

**HU06 — Cancelar reserva**
Como convidado, quero cancelar minha reserva se desistir do presente.
- *Dado* que tenho uma reserva, *quando* cancelo, *então* o presente volta à lista para todos.

**HU07 — Confirmar presença com acompanhantes**
Como convidado, quero confirmar presença e listar quem vem comigo sem que cada pessoa precise fazer login.
- *Dado* que estou logado, *quando* confirmo, *então* informo apenas os acompanhantes e, para cada um, se é criança menor de 10 anos e a idade.

**HU08 — Acompanhar confirmações**
Como noivo, quero ver quantos adultos e crianças confirmaram para planejar o evento.
- *Dado* que estou no painel, *quando* abro as confirmações, *então* vejo a lista e os totais.

**HU09 — Exportar planilhas**
Como noivo, quero baixar reservas e confirmações em Excel para usar fora do sistema.
- *Quando* clico em exportar, *então* recebo um arquivo `.xlsx` com os dados atualizados.

**HU10 — Gerenciar presentes**
Como noivo, quero cadastrar, editar e remover presentes, com valor estimado.

**HU11 — Tirar dúvidas com o assistente**
Como convidado, quero perguntar sobre o casamento (ex.: dress code, horário) e receber resposta imediata.

**HU12 — Receber sugestão de presente**
Como convidado, quero dizer meu orçamento e estilo para receber sugestões de presentes da lista.

**HU13 — Consultar dados por conversa**
Como noivo, quero perguntar ao assistente "quantos confirmaram?" e receber a resposta com base no banco de dados.

## 7. Fora do escopo (versão 0.1)

- Bot ou integração com Telegram
- Campo de restrição alimentar na confirmação de presença
- Pagamento de presentes dentro do app
- Integração com WhatsApp

## 8. Pontos em aberto

Itens que precisam de decisão antes ou durante a implementação:

| # | Ponto | Sugestão inicial |
|---|---|---|
| 1 | Margem do filtro de preço | ±20% do valor informado |
| 2 | Forma de login do convidado | Nome + telefone; evoluir para código de acesso individual se necessário |
| 3 | Como evitar que qualquer pessoa com o link acesse o app | Código de acesso ao convite ou lista de convidados pré-cadastrada |
| 4 | Limite de reservas por convidado | Sem limite na v0.1 |
| 5 | Prazo limite para confirmar presença | Definir data-limite pelos noivos |
| 6 | Armazenamento das fotos do casal | Arquivos locais no frontend na v0.1 |
| 7 | Autenticação dos noivos | Usuário e senha simples, com senha armazenada com hash |
| 8 | Valor estimado dos presentes | Informado manualmente (RN07); não há consulta automática de preço |
