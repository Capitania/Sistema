# Imagem base para a compilação
FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build

# Define a versão do framework .NET Framework para 4.7.2
ENV FrameworkPathOverride=/usr/share/dotnet/sdk/3.1.426/FSharp/
ENV FrameworkPathOverride=/usr/share/dotnet/sdk/3.1.426/Microsoft/TargetingPack/3.1.16/

# Diretório de trabalho
WORKDIR /app

# Copiar os arquivos do projeto para o diretório de trabalho
COPY . .

# Restaurar as dependências
RUN dotnet restore

# Compilar o projeto
RUN dotnet build --configuration Release --no-restore

# Publicar o projeto
RUN dotnet publish --configuration Release --output out --no-restore

# Imagem de tempo de execução
FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS runtime

# Diretório de trabalho
WORKDIR /app

# Copiar os arquivos publicados anteriormente
COPY --from=build /app/out .

# Expor a porta em que o aplicativo ASP.NET Core será executado
EXPOSE 80

# Comando para iniciar o aplicativo ASP.NET Core
ENTRYPOINT ["dotnet", "Capitania.Web.Mvc.dll"]
