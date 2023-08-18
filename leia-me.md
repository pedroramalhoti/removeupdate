Criar um arquivo batch para desinstalar uma atualização do Windows por meio de uma GPO (Política de Grupo) envolve alguns passos. Primeiro, vamos criar o arquivo batch e, em seguida, orientá-lo sobre como implementar esse arquivo usando uma GPO.

### 1. Criando o arquivo batch

Suponha que você deseja remover a atualização com a ID "KB1234567" (substitua "KB1234567" pelo número da atualização que você deseja remover):

```batch
@echo off
wusa /uninstall /kb:1234567 /quiet /norestart
```

Salve isso em um arquivo com a extensão `.bat`, por exemplo, `removeUpdate.bat`.

### 2. Implantando o arquivo batch via GPO

1. Abra o `Gerenciamento de Política de Grupo` no servidor.
2. No painel esquerdo, navegue até o local onde você deseja criar a nova GPO (geralmente em uma Unidade Organizacional específica).
3. Clique com o botão direito na Unidade Organizacional desejada e selecione `Criar um GPO neste domínio e vinculá-lo aqui`.
4. Dê um nome para a GPO e clique em OK.
5. Clique com o botão direito na nova GPO criada e selecione `Editar`.
6. Navegue até `Configuração do Computador` > `Políticas` > `Configurações do Windows` > `Scripts (Inicialização/Desligamento)`.
7. No painel direito, dê um duplo clique em `Inicialização` ou `Desligamento`, dependendo de quando você deseja que o script seja executado.
8. No pop-up, clique em `Adicionar` e, em seguida, `Procurar` para selecionar o arquivo batch que você criou anteriormente.
9. Após adicionar o script, clique em `OK`.
10. Feche o Editor de Política de Grupo.

Após essas etapas, a próxima vez que os computadores na Unidade Organizacional selecionada forem iniciados ou desligados (dependendo de sua escolha), eles executarão o script batch e tentarão desinstalar a atualização especificada.

**Nota**: É altamente recomendado testar o arquivo batch manualmente em uma máquina de teste antes de implementá-lo em todo o domínio, para garantir que ele funcione como esperado e não cause nenhum problema não intencional.
