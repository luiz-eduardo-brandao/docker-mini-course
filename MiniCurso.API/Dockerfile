FROM mcr.microsoft.com/dotnet/sdk:8.0
EXPOSE 80 5000 5213

ENV ASPNETCORE_URLS=http://+:5000;https://+:5001

COPY bin/Release/net8.0/publish/ App/
WORKDIR /App
ENTRYPOINT [ "dotnet", "MiniCurso.API.dll" ]