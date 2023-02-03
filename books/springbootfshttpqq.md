#### spring boot 发送http请求
```
		<dependency>
			<groupId>org.apache.httpcomponents</groupId>
			<artifactId>httpclient</artifactId>
			<version>4.5.2</version>
		</dependency>

 HttpComponentsClientHttpRequestFactory factory =
                new HttpComponentsClientHttpRequestFactory();

        HttpClient httpClient =
                HttpClientBuilder.create()
                        .setRedirectStrategy(new LaxRedirectStrategy())
                        .build();

        factory.setHttpClient(httpClient);


        RestTemplate restTemplate = new RestTemplate();
        HttpHeaders headers = new HttpHeaders();
        headers.set("user-agent",
                "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.97 Safari/537.36");
        headers.set("cookie", "my_user_id=haha123; UN=1231923;gr_user_id=welcome_yhh;");
        restTemplate.setRequestFactory(factory);

        HttpEntity<String> res = restTemplate.exchange("http://gg.gg/maotv10", HttpMethod.GET, new HttpEntity<>(null, headers),String.class);
        String body = res.getBody();
```