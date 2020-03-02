구글에서 만든 jib을 사용해서 docker 엔진을 사용하지 않고 docker 이미지를 생성하고 허브에 push하는 방법을 알아본다. 레퍼런스에서 자세한 설명이 있으니 최대한 빠르게 하는 방법만 요약한다.

 

pom 파일에 아래와 같이 설정

<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
        <plugin>
            <groupId>com.google.cloud.tools</groupId>
            <artifactId>jib-maven-plugin</artifactId>
            <version>2.1.0</version>
            <configuration>
                <from>
                    <image>openjdk:alpine</image>
                </from>
                <to>
                    <image>registry.hub.docker.com/v0o0v/springboot-docker-demo</image>
                    <auth>
                        <username>v0o0v</username>
                        <!--suppress UnresolvedMavenProperty -->
                        <password>${env.REGISTRY_PASSWORD}</password>
                    </auth>
                </to>
                <container>
                    <ports>
                        <port>8080</port>
                    </ports>
                </container>
            </configuration>
        </plugin>
    </plugins>
</build>

<from>은 docker이미지가 추가될 원본 이미지 설정

<to>는 어디로 push할지 설정.  본문에는 docker 허브로 설정되어 있지만 다른 도커 레지스트리 어떤 곳이든 가능.  <auth>에 계정 인증 정보를 넣어야 하는데 암호 같은 경우에 환경변수로 빼고 메이븐 실행시 넣어준다.  빨간색 부분이 암호를 넣어주는 부분이다. 

자세한 내용은 아래 링크 참고

 

