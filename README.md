# Como configurar/instalar/usar o `depurar os erros do Linux com o journalctl` no `Linux Ubuntu`

## Resumo

Neste documento estão contidos os principais comandos e configurações para configurar/instalar/usar o `depurar os erros do Linux com o journalctl` no `Linux Ubuntu`.

## _Abstract_

_This document contains the main commands and settings for configuring/installing/using the `depurar os erros do Linux com o journalctl` on `Linux Ubuntu`._

## Descrição [2]

### `journalctl`

`journalctl` é uma ferramenta de linha de comando no sistema `Linux` que permite acessar e visualizar `logs` do sistema mantidos pelo `systemd-journald`. Ele fornece uma interface conveniente para analisar registros de inicialização, mensagens do kernel, registros de serviços e eventos do sistema. Com o `journalctl`, os usuários podem filtrar e pesquisar registros com base em várias opções, como intervalo de tempo, nível de prioridade e origem do registro, facilitando a depuração e análise de problemas do sistema.

### `lightdm`

O LightDM é um gerenciador de exibição (display manager) leve e flexível para sistemas Linux. Ele fornece uma interface gráfica de login para os usuários, permitindo que escolham entre diferentes sessões e usuários para acessar o sistema. O LightDM é altamente personalizável e suporta diferentes ambientes de desktop, como GNOME, KDE, Xfce, entre outros, tornando-o uma escolha popular para distribuições Linux que buscam uma solução de gerenciamento de exibição eficiente e customizável.

### `dbus`

DBus é um sistema de comunicação entre processos (IPC) usado em sistemas Linux para permitir a comunicação entre diferentes aplicativos em um ambiente de desktop. Ele fornece um barramento de mensagens que os aplicativos podem usar para trocar informações e invocar métodos em outros processos de forma assíncrona. O DBus é amplamente utilizado em ambientes de desktop Linux, como GNOME e KDE, para facilitar a integração entre os diferentes componentes do sistema, como aplicativos, serviços e gerenciadores de janelas. Ele oferece um mecanismo eficiente e seguro para a comunicação entre processos, ajudando a melhorar a interoperabilidade e a funcionalidade do sistema operacional.


## 1. Como configurar/instalar/usar o `depurar os erros do Linux com o journalctl` no `Linux Ubuntu` [1][3]

Para configurar/instalar/usar o `depurar os erros do Linux com o journalctl` no `Linux Ubuntu`, você pode seguir estes passos:

1. Abra o `Terminal Emulator`. Você pode fazer isso pressionando: `Ctrl + Alt + T`

2. Certifique-se de que seu sistema esteja limpo e atualizado.

    2.1 Limpar o `cache` do gerenciador de pacotes `apt`. Especificamente, ele remove todos os arquivos de pacotes (`.deb`) baixados pelo `apt` e armazenados em `/var/cache/apt/archives/`. Digite o seguinte comando: `sudo apt clean` 
    
    2.2 Remover pacotes `.deb` antigos ou duplicados do cache local. É útil para liberar espaço, pois remove apenas os pacotes que não podem mais ser baixados (ou seja, versões antigas de pacotes que foram atualizados). Digite o seguinte comando: `sudo apt autoclean`

    2.3 Remover pacotes que foram automaticamente instalados para satisfazer as dependências de outros pacotes e que não são mais necessários. Digite o seguinte comando: `sudo apt autoremove -y`

    2.4 Buscar as atualizações disponíveis para os pacotes que estão instalados em seu sistema. Digite o seguinte comando e pressione `Enter`: `sudo apt update`

    2.5 **Corrigir pacotes quebrados**: Isso atualizará a lista de pacotes disponíveis e tentará corrigir pacotes quebrados ou com dependências ausentes: `sudo apt --fix-broken install`

    2.6 Limpar o `cache` do gerenciador de pacotes `apt`. Especificamente, ele remove todos os arquivos de pacotes (`.deb`) baixados pelo `apt` e armazenados em `/var/cache/apt/archives/`. Digite o seguinte comando: `sudo apt clean` 
    
    2.7 Para ver a lista de pacotes a serem atualizados, digite o seguinte comando e pressione `Enter`:  `sudo apt list --upgradable`

    2.8 Realmente atualizar os pacotes instalados para as suas versões mais recentes, com base na última vez que você executou `sudo apt update`. Digite o seguinte comando e pressione `Enter`: `sudo apt full-upgrade -y`


Investigando Erros do Sistema no `Linux Ubuntu` com `journalctl`

Para abrir o `journal` pelo `Terminal Emulator` e investigar erros do sistema no `Linux Ubuntu`, você pode seguir os seguintes passos:

1. **Abra o `Terminal Emulator`**: Você pode abrir o Terminal pressionando: `Ctrl + Alt + T` 

2. **Uso Básico do `journalctl`**: Para ver todos os logs do sistema, simplesmente digite `journalctl` e pressione `Enter`.

3. **Filtrar Logs por Unidade do `systemd`**: Para ver logs de uma unidade específica, use `journalctl -u nome_da_unidade`. Exemplo: `journalctl -u apache2` para ver `logs` do Apache.

4. **Filtrar Logs por Período de Tempo**: Para ver `logs` de um período específico:

    4.1 Você pode usar `-o desde,até`. Exemplo para ver logs de hoje: `journalctl --since today`
    
    4.2 Para um período específico: `journalctl --since "2023-04-01 00:00:00" --until "2023-04-02 00:00:00"` 

5. **Navegar pelos Logs**: Quando estiver visualizando os `logs`, você pode usar as teclas de seta para cima e para baixo para navegar. Pressione `q` para sair.

6. **Pesquisar por Erros Específicos**: Para filtrar por níveis de severidade, use a opção `-p` (prioridade), seguida do nível de `log` desejado. Exemplo, mostrará apenas as mensagens de erro: `journalctl -p err`

    6.1 Para usar o comando `journalctl -p err` e mostrar somente os erros da data de hoje, você pode combinar a opção -p com a opção --since para filtrar por entradas de log de um certo nível de severidade (neste caso, erros) a partir de um determinado momento (neste caso, hoje). O comando ficaria assim: `journalctl -p err --since today`

7. **Visualização Interativa**: Para uma visualização mais interativa, você pode usar o comando a seguir, isso pode ser útil para investigar problemas recentes: `journalctl -xe`

8. Para consultar somente os erros que ocorreram após a última reinicialização do sistema, você pode usar o comando `journalctl` combinando o filtro de nível de prioridade para erros (`-p err`) com a opção `-b`, que especifica o `"boot"` ou a reinicialização do sistema a partir da qual você deseja começar a visualização dos `logs`. O comando seria assim: `journalctl -b -p err`

    A opção `-b` sem qualquer argumento adicional mostra os `logs` do `boot` atual (última reinicialização). Se você quiser ver os erros de `boots` específicos, você pode adicionar um número após `-b` (por exemplo, `-b -1` para o boot anterior ao atual).

9. **Seguir Logs em Tempo Real**: Para acompanhar novas entradas de log em tempo real, use a opção `-f`, similar ao comando `tail -f`.

Exemplo de comando para filtrar por erros desde um dia específico:



### 1.1 Reiniciar o `lightdm` e/ou o `dbus` sem ter que reiniciar o computador para depurar os erros

1. **Reinicie o LightDM**: `sudo systemctl restart lightdm` ou `sudo systemctl restart dbus`

    **ATENÇÂO**: Perceber que, dependendo do erro, usar um comando ou o outro **NÃO** é uma opção, às vezes, um dos comandos irá ajudar em um erro e o outro em outro. Sendo assim, é recomendável testar com os dois comandos.

## 2. Código completo para configurar/instalar/usar

Para configurar/instalar/usar o `depurar os erros do Linux com o journalctl` no `Linux Ubuntu` sem precisar digitar linha por linha, você pode seguir estas etapas:

1. Abra o `Terminal Emulator`. Você pode fazer isso pressionando: `Ctrl + Alt + T`

2. Digite o seguinte comando e pressione `Enter`:

    ```
    NÃO há.
    ```


## Referências

[1] OPENAI. ***Extrair arquivo .rar Linux.*** Disponível em: <https://chat.openai.com/c/b315251f-5bf4-48bb-8c0b-d306db412439> (texto adaptado). Acessado em: 02/04/2023 17:11.

[2] OPENAI. ***Vs code: editor popular.*** Disponível em: <https://chat.openai.com/c/b640a25d-f8e3-4922-8a3b-ed74a2657e42> (texto adaptado). Acessado em: 02/04/2024 17:10.

