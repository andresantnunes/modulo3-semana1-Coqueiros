# realiza a herança da imagem padrão do dotnet da microsoft
FROM mcr.microsoft.com/dotnet/sdk:7.0 as build-env

# identifica o arquivo de trabalho como o /src
WORKDIR /src

# Cache dos arquivos de execução do projeto
COPY src/*.csproj .
RUN dotnet restore --use-current-runtime  

# Copia os arquivos do src para máquina virtual local, essa máquina é interna ao docker
COPY src .

RUN dotnet publish src.sln -c Release -o /publish


FROM mcr.microsoft.com/dotnet/aspnet:7.0 as runtime
WORKDIR /publish
COPY --from=build-env /publish .
EXPOSE 80
ENTRYPOINT ["dotnet", "myWebApp.dll"]
