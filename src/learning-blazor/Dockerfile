FROM mcr.microsoft.com/dotnet/sdk:5.0.301-buster-slim AS publish

WORKDIR /src/learning-blazor
COPY ["src/learning-blazor/learning-blazor.csproj", "."]
RUN dotnet restore "learning-blazor.csproj"
COPY src/learning-blazor .
RUN dotnet publish "learning-blazor.csproj" -c Release -o /app/publish

FROM nginx:1.20.0 AS stage-nginx

WORKDIR /app
COPY --from=publish /app/publish/wwwroot .
COPY /src/learning-blazor/nginx.conf /etc/nginx/nginx.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
