# criar a maquina virtual e prepara o ambiente dotnet para a execução do programa
FROM mcr.microsoft.com/dotnet/sdk:7.0 as build-env
# defino o meu arquivo de trabalho dentro do container
WORKDIR /src
# carregando as dependecias no container
# ganho de performance depois da 1ª execução
COPY src/*.csproj .
RUN dotnet restore --use-current-runtime
# copio da pasta src que está na minha máquina para dentro do container
COPY src .

# complia a aplicação dentro do container
# salva a aplicação compilada no /publish
RUN dotnet publish hello.sln -c Release -o /publish
FROM mcr.microsoft.com/dotnet/aspnet:7.0 as runtime
WORKDIR /publish
# busco as informações do /publish para executar no container
COPY --from=build-env /publish .
EXPOSE 80
ENTRYPOINT [ "dotnet", "hello.ddl" ]


