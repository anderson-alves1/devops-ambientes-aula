# ETAPA 3 — Diagnóstico, Mudança e Recuperação

**Projeto:** DevOps — Gerenciamento de Ambientes  
**Integrantes:** [Nome do integrante 1] e [Nome do integrante 2]

---

# PARTE A — DIAGNÓSTICO DO AMBIENTE

## 1. Cenário analisado

O ambiente apresenta três problemas principais:

- Homologação e produção utilizam versões diferentes do banco de dados.
- Uma porta de comunicação foi liberada manualmente.
- O conhecimento sobre a configuração completa do ambiente depende de apenas uma pessoa.

Esses problemas dificultam a reprodução dos ambiOn branch main
Your branch is up to date with 'origin/main'.

Untracked files:On branch main
Your branch is up to date with 'origin/main'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        entregas/

nothing added to commit but untracked files present (use "git add" to track)
((.venv) ) @anderson-alves1 ➜ /workspaces/devops-ambientes-aula (main) $ 
  (use "git add <file>..." to include in what will be committed)
        entregas/

nothing added to commit but untracked files present (use "git add" to track)
((.venv) ) @anderson-alves1 ➜ /workspaces/devops-ambientes-aula (main) $entes, aumentam o risco de falhas e tornam a manutenção dependente de intervenções manuais.

## 2. Tabela de diagnóstico

| Problema | Consequência | Estado desejado | Evidência da correção | Camadas afetadas | Classificação da intervenção |
|---|---|---|---|---|---|
| Homologação e produção utilizam versões diferentes do banco de dados. | Diferenças de comportamento podem fazer uma aplicação funcionar na homologação e apresentar erros em produção. | Utilizar versões compatíveis e controladas do banco de dados nos dois ambientes. | Arquivos de configuração e registros que comprovem as versões utilizadas em cada ambiente. | Dados e software básico. | Provisionamento e configuração. |
| Uma porta foi liberada manualmente. | A configuração pode não ser reproduzida em outro ambiente ou após uma reconstrução, além de dificultar o controle de segurança. | Registrar e automatizar a regra de liberação da porta, mantendo apenas o acesso necessário. | Arquivo de configuração versionado e registro da regra aplicada. | Infraestrutura e rede. | Configuração e gerenciamento. |
| O conhecimento da configuração completa depende de uma pessoa. | A equipe pode ficar impedida de manter ou recuperar o ambiente quando essa pessoa não estiver disponível. | Documentar, versionar e automatizar as configurações para que qualquer integrante autorizado consiga reproduzir o ambiente. | Documentação no repositório, arquivos versionados e execução reproduzível por outro integrante. | Todas as camadas envolvidas no ambiente. | Gerenciamento e configuração. |

## 3. Análise das camadas afetadas

- **Infraestrutura e rede:** envolve recursos de execução, máquinas, portas e comunicação entre serviços.
- **Software básico:** envolve ferramentas e serviços necessários para executar a aplicação, como o banco de dados.
- **Dados:** envolve o armazenamento e a compatibilidade das informações.
- **Aplicação:** envolve o funcionamento do sistema que utiliza os serviços e recursos do ambiente.

## 4. Classificação das intervenções

- **Provisionamento:** criação e disponibilização dos recursos necessários para o ambiente.
- **Configuração:** definição de parâmetros, versões, portas e comportamentos dos serviços.
- **Implantação:** disponibilização de uma aplicação ou versão em determinado ambiente.
- **Gerenciamento:** documentação, controle, manutenção e acompanhamento dos recursos e configurações.

## 5. Conclusão do diagnóstico

Os problemas identificados demonstram a importância de manter ambientes padronizados, configurações versionadas e processos automatizados.

A utilização de ferramentas como Docker, Terraform e Ansible contribui para reduzir diferenças entre ambientes, evitar configurações manuais e permitir que outros integrantes da equipe reproduzam a infraestrutura com maior segurança.

---

# PARTE B — PROPOSTA DE MUDANÇA E REVISÃO
## 1. Objetivo

Realizar duas propostas de mudança no projeto, utilizando branches separadas, commits e Pull Requests, com revisão entre os integrantes antes da incorporação das alterações à branch principal (`main`).

## 2. Primeira rodada — Proposta do Integrante B

**Responsável pela proposta:** Integrante B (dupla)(Matheus).

**Responsável pela revisão:** Integrante A(Anderson).

**Arquivo alterado:** `docker/index.html`.

**Alteração realizada:** atualização do texto do título principal da página HTML.

**Efeito esperado:** modificar o título apresentado na página servida pelo Nginx, mantendo as demais configurações do ambiente.

**Execução:** foi criada a branch `mudanca-integrante-b`, realizada a alteração e registrado o commit `7fcd1b2`.

**Revisão:** o Integrante A analisou a alteração e verificou se ela correspondia à proposta.

**Incorporação:** a alteração foi integrada à branch principal por meio do Pull Request #1.

## 3. Segunda rodada — Proposta do Integrante A

**Responsável pela proposta:** Integrante A.

**Responsável pela revisão:** Integrante B (dupla).

**Arquivo alterado:** `docker/index.html`.

**Alteração realizada:** adição de uma nova seção denominada "Status do Ambiente", apresentando informações sobre o servidor web Nginx e a execução com Docker.

**Efeito esperado:** acrescentar informações à página HTML sem remover o conteúdo existente.

**Execução:** foi criada a branch `mudanca-integrante-a`, realizada a alteração e registrado o commit `f30e03e`.

**Revisão:** o Integrante B analisou a alteração e verificou se o novo conteúdo estava correto e se as configurações existentes foram preservadas.

**Incorporação:** a alteração foi integrada à branch principal por meio do Pull Request #2.

## 4. Verificação das alterações

O histórico do Git foi consultado por meio do comando `git log --oneline --decorate -8`.

Foram identificados os seguintes registros:

- `7fcd1b2` — atualização do título da página.
- `86e8e8b` — merge do Pull Request #1.
- `f30e03e` — adição da seção de status do ambiente.
- `066d671` — merge do Pull Request #2.

A atualização da branch principal foi confirmada por meio do comando `git pull origin main`, que realizou a atualização sem conflitos.

## 5. Resultado

As duas propostas foram realizadas em branches separadas, revisadas pelo outro integrante e incorporadas à versão principal por meio de Pull Requests.

A atividade demonstrou o uso de branches, commits, revisão colaborativa e integração de mudanças no GitHub.

# PARTE C — FALHA E RECUPERAÇÃO

## 1. Falha reproduzida

Foi realizada uma falha controlada no ambiente Docker Compose, alterando o mapeamento da porta do serviço web.

A configuração original era:

    ports:
      - "8080:80"

Para reproduzir o problema, foi alterada para:

    ports:
      - "8080:81"

O contêiner foi reconstruído e iniciado com a configuração incorreta.

## 2. Sintoma observado e hipótese da causa

Ao executar o comando:

    curl --fail --show-error http://localhost:8080

Foi apresentado o seguinte erro:

    curl: (56) Recv failure: Connection reset by peer

A hipótese identificada foi um erro no mapeamento das portas.

A porta 8080 representa a porta de acesso no host, enquanto a porta 81 foi configurada como destino dentro do contêiner. Entretanto, o servidor Nginx utiliza a porta 80 por padrão.

Dessa forma, o encaminhamento estava direcionado para uma porta incorreta.

## 3. Correção aplicada

O arquivo `docker/compose.yaml` foi corrigido, substituindo:

    - "8080:81"

Por:

    - "8080:80"

Depois da alteração, o arquivo foi salvo e o ambiente foi reconstruído com:

    docker compose -f docker/compose.yaml up --build -d

## 4. Verificação da recuperação

Foi executado:

    docker compose -f docker/compose.yaml ps

O resultado confirmou que o contêiner estava em execução e que o mapeamento estava correto:

    0.0.0.0:8080->80/tcp

Em seguida, foi realizado novamente o teste:

    curl --fail --show-error http://localhost:8080

O teste confirmou que a página HTML voltou a responder corretamente.

## 5. Evidências

- **Evidência 1 — Antes da falha:** execução do curl com a página respondendo normalmente.
- **Evidência 2 — Durante a falha:** mensagem `Recv failure: Connection reset by peer`.
- **Evidência 3 — Após a correção:** saída do `docker compose ps`, demonstrando o contêiner ativo e o mapeamento `8080:80`.
- **Evidência 4 — Recuperação:** execução do curl com retorno do HTML da aplicação.

## 6. Conclusão da recuperação

A falha foi identificada por meio do teste de acesso ao serviço. A análise demonstrou que o problema estava no mapeamento incorreto da porta interna do contêiner.

Após a correção de `8080:81` para `8080:80`, o serviço voltou a responder normalmente.

A atividade demonstrou a importância de verificar as configurações de rede, analisar mensagens de erro e validar o funcionamento do ambiente após uma intervenção.
---

# CONCLUSÃO GERAL

A atividade demonstra como o gerenciamento de ambientes com ferramentas de DevOps permite identificar problemas, propor mudanças controladas, automatizar configurações e recuperar serviços após falhas.

A documentação e o versionamento das alterações também permitem que os integrantes da equipe acompanhem a evolução do ambiente e reproduzam os procedimentos realizados.