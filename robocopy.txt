@echo off
color 02
mode con: cols=85 lines=35
setlocal
cls

echo  ######################## BEM VINDO ###############################################
echo  # ASSISTENTE DE TRANSFERENCIA DE ARQUIVOS COM ROBOCOPY SIGA AS INSTRUCOES ABAIXO #
echo  ##################################################################################
echo Defina o caminho de origem
set /p origem="Insira o caminho da pasta de origem: "

echo Validando caminho de origem
if not exist "%origem%" (
    echo O caminho de origem especificado não é válido.
    pause
    exit /b
)

cls

echo Defina o caminho de destino
set /p destino="Insira o caminho da pasta de destino: "

echo Validando caminho de destino
if not exist "%destino%" (
    echo O caminho de destino especificado não é válido.
    pause
    exit /b
)

cls

echo ########################################## 
echo #  ASSISTENTE TRANFERENCIA COM ROBOCOPY  #
echo ##########################################
echo.
echo Escolha a operacao desejada:
echo 1. Copiar
echo 2. Mover
echo 3. Backup
set /p opcao="Opcao: "

if "%opcao%"=="1" (
    set opcao=/E /ZB
    set opdesc=COPIAR
) else if "%opcao%"=="2" (
    set opcao=/MOVE /ZB
    set opdesc=MOVER
) else if "%opcao%"=="3" (
    set opcao=/MIR /ZB
    set opdesc=BACKUP
) else (
    echo Opção inválida.
    pause
    exit /b
)

cls

echo ##################################################
echo #  Menu de opcoes de tamanho da transferencia    #
echo ##################################################
echo.
echo Escolha o tamanho da transferencia em bits:
echo 1. 64
echo 2. 128
echo 3. 256

set /p tamanho="Tamanho da transferência (em bits): "

echo Aguarde ate a tarefa ser comcluida

cls
robocopy "%origem%" "%destino%" %opcao% /MT:%tamanho% /LOG+:log.txt


cls

echo.
echo ####################
echo # Tarefa Concluida #
echo ####################
echo.
echo Informacoes do destino apos a transferencia:
echo.
DIR "%destino%"

pause null
