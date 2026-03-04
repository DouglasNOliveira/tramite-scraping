# TramiteScraping

## Sobre
Este repositório contém o notebook `fluxo_extracao_tramite.ipynb`, usado para automatizar a coleta de dados de processos no Trâmite (TCE-PR) e atualizar uma planilha Excel compartilhada.

O fluxo foi pensado para uso por equipe não técnica, com execução célula a célula no VS Code/Jupyter.

## O que o notebook faz
Para cada link informado, o notebook:
1. Abre o sistema no navegador (Selenium/Chrome).
2. Faz login com usuário e senha.
3. Tenta carregar a página do processo com retentativas automáticas em caso de erro (incluindo tela "500 Ops").
4. Extrai os campos:
   - `link_processo`
   - `processo`
   - `assunto_subassunto`
   - `entidade`
   - `autuacao`
   - `conclusao_cacs` (coluna manual, preenchida em branco)
5. Atualiza o Excel sem duplicar registros já existentes (deduplicação por `link_processo`).
6. Fecha o navegador automaticamente ao final.

## Pré-requisitos
- Windows com VS Code.
- Python 3 instalado.
- Extensão Python/Jupyter no VS Code.
- Google Chrome instalado.
- Acesso ao Trâmite (credenciais válidas).
- Arquivo Excel em pasta sincronizada do OneDrive/SharePoint.

## Estrutura principal
- `fluxo_extracao_tramite.ipynb`: notebook principal.

## Como usar
1. Abra o notebook no VS Code.
2. Execute a primeira célula de instalação (uma única vez por máquina).
3. Reinicie o kernel do notebook.
4. Na célula de configuração, informe:
   - `LINKS_PROCESSO` (um ou mais links)
   - `USUARIO`
   - `SENHA`
   - `PASTA_EXCEL_SINCRONIZADA` e `ARQUIVO_EXCEL`
5. Execute as células na ordem.

## Importante para uso em equipe
- Todos devem usar o mesmo arquivo Excel na pasta sincronizada do SharePoint/Teams.
- Evite execução simultânea de várias pessoas no mesmo momento para reduzir risco de conflito de escrita.
- Evite manter o Excel aberto no Teams/Excel Web enquanto o notebook grava.

## Solução de problemas
- **Erro 500 na página**: o notebook já tenta recarregar automaticamente.
- **Links colados/concatenados**: o notebook separa links concatenados automaticamente.
- **Registros duplicados**: há deduplicação por `link_processo` na etapa de gravação.
- **Navegador não fecha**: verificar se `FECHAR_NAVEGADOR_AUTO = True` na configuração.

## Segurança
- Não versionar credenciais no Git.
- Preencha `USUARIO` e `SENHA` apenas localmente.
