FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["Blog.Core/Blog.Core.csproj", "Blog.Core/"]
COPY ["Blog.Core.Model/Blog.Core.Model.csproj", "Blog.Core.Model/"]
COPY ["Blog.Core.Common/Blog.Core.Common.csproj", "Blog.Core.Common/"]
COPY ["Blog.Core.IRepository/Blog.Core.IRepository.csproj", "Blog.Core.IRepository/"]
COPY ["Blog.Core.Services/Blog.Core.Services.csproj", "Blog.Core.Services/"]
COPY ["Blog.Core.IServices/Blog.Core.IServices.csproj", "Blog.Core.IServices/"]
COPY ["Blog.Core.Repository/Blog.Core.Repository.csproj", "Blog.Core.Repository/"]
RUN dotnet restore "Blog.Core/Blog.Core.csproj"
COPY . .
WORKDIR "/src/Blog.Core"
RUN dotnet build "Blog.Core.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Blog.Core.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Blog.Core.dll"]