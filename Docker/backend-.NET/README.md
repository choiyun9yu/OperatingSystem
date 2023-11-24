# .NET Dockerfile 

## 1. 배포 준비

    % dotnet watch run  // 어플리케이션 동작에 문제가 없는지 확인

    % dotnet publish -c Release     // 어플리케이션을 /project-name/bin/Release/net7.0/publish 경로에 컴파일
                                    // 이때 project-name.dll 파일이 실행파일

## 2. Dockerfile 만들기

    FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build-env
    WORKDIR /{project-name}
    
    # Copy everything
    COPY . ./
    # Restore as distinct layers
    RUN dotnet restore
    # Build and publish a release
    RUN dotnet publish -c Release -o out
    
    # Build runtime image
    FROM mcr.microsoft.com/dotnet/aspnet:7.0
    WORKDIR /{project-name}
    COPY --from=build-env /{project-name}/out .
    ENTRYPOINT ["dotnet", "{project-name}.dll"]

## 3. 이미지 빌드

    % docker build -t {이미지 태그 명} -f Dockerfile .

## 4. 컨테이너 만들기

    % docker create --name {컨테이너 명} {앞에서 만든 이미지 태그 명}

## 5. 도커 시작

    % docker start core-counter