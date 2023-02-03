```java
    public void test01() throws MalformedURLException {
        java.util.logging.Logger.getLogger("com.gargoylesoftware").setLevel(Level.OFF);
        java.util.logging.Logger.getLogger("org.apache.http.client").setLevel(Level.OFF);
        WebClient webClient=new WebClient(BrowserVersion.CHROME); // 实例化Web客户端
        webClient.setWebStartHandler(new WebStartHandler() {
            @Override
            public void handleJnlpResponse(WebResponse webResponse) {
                System.out.println("handleJnlpResponse");
            }
        });

        WebRequest request=new WebRequest(new URL("https://ip138.com/"));
       // request.setProxyHost("127.0.0.1");
       // request.setProxyPort(7890);
        request.setAdditionalHeader("Referer", "https://ip138.com/");//设置请求报文头里的refer字段
        request.setAdditionalHeader("User-Agent","Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4272.0 Safari/537.36");
        /******配置webClient******/
        //ajax
        webClient.setAjaxController(new NicelyResynchronizingAjaxController());
        //支持js
        webClient.getOptions().setJavaScriptEnabled(true);
        //忽略js错误
        webClient.getOptions().setThrowExceptionOnScriptError(false);
        //忽略css错误
        webClient.setCssErrorHandler(new SilentCssErrorHandler());
        //不执行CSS渲染
        webClient.getOptions().setCssEnabled(true);
        //超时时间
        webClient.getOptions().setTimeout(3000);
        //允许重定向
        webClient.getOptions().setRedirectEnabled(true);
        //允许cookie
        webClient.getCookieManager().setCookiesEnabled(true);
        try {
            HtmlPage page=webClient.getPage(request); // 解析获取页面
            webClient.waitForBackgroundJavaScript(2000);
            // Thread.sleep(1000); // 休息10秒钟 等待htmlunit执行js
            //DomElement domElement= (DomElement) page.getByXPath("//p[@align='center']").get(0);
            DomElement domElement = page.getElementsByTagName("iframe").get(0);
            String src = domElement.getAttribute("src");
            HtmlPage page1 = webClient.getPage("http:" + src);
            HtmlElement p = (HtmlElement) page1.getElementsByTagName("p").get(0);
            System.out.println(p.asText());
            CookieManager cookieManager = webClient.getCookieManager();
            Set<Cookie> cookies = cookieManager.getCookies();
            for (Cookie cookie : cookies) {
                System.out.println(cookie.getDomain()+"====="+cookie.getName()+"====="+cookie.getValue());
            }

        } catch (Exception e) {
            e.printStackTrace();
        }

    }

    @Test
    public void test03() throws IOException {
        //http://localhost:8088/test/demo02.html
        WebClient webClient=new WebClient(BrowserVersion.CHROME); // 实例化Web客户端
        webClient.setAjaxController(new NicelyResynchronizingAjaxController());
        //支持js
        webClient.getOptions().setJavaScriptEnabled(true);
        //忽略js错误
        webClient.getOptions().setThrowExceptionOnScriptError(false);
        //忽略css错误
        webClient.setCssErrorHandler(new SilentCssErrorHandler());
        //不执行CSS渲染
        webClient.getOptions().setCssEnabled(true);
        //超时时间
        webClient.getOptions().setTimeout(3000);
        //允许重定向
        webClient.getOptions().setRedirectEnabled(true);
        //允许cookie
        webClient.getCookieManager().setCookiesEnabled(true);
        WebRequest request=new WebRequest(new URL("http://localhost:8088/test/demo02.html"));
        HtmlPage page = webClient.getPage(request);
        DomElement ss = page.getElementById("ss");
        UnexpectedPage tmppage = ss.click();
        InputStream is = tmppage.getWebResponse().getContentAsStream();
        FileOutputStream output = new FileOutputStream("E:\\1.exe");
        IOUtils.copy(is, output);
    }

    public static void main(String[] args) {
        System.setProperty("webdriver.chrome.driver", "E:\\chromedriver.exe");
        ChromeOptions options = new ChromeOptions();
        options.setBinary("C:\\Users\\Administrator\\Desktop\\chrome-win\\chrome.exe");
        options.addArguments("user-agent=\"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36\"");
        options.addArguments("sec-ch-ua=\"Google Chrome\";v=\"105\", \"Not)A;Brand\";v=\"8\", \"Chromium\";v=\"105\"");
        options.addArguments("sec-ch-ua-platform=\"Windows\"");
        options.addArguments("accept=\"text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9\"");
        options.addArguments("--headless"); //无浏览器模式
        options.addArguments("--no-sandbox");// 为了让root用户也能执行
        // 优化参数
        options.addArguments("--disable-dev-shm-usage");
        options.addArguments("blink-settings=imagesEnabled=false");
        options.addArguments("--disable-gpu");
        ChromeDriver driver = new ChromeDriver(options);//实例化
        driver.manage().timeouts().pageLoadTimeout(300000, TimeUnit.SECONDS);
        driver.get("https://www.baidu.com");
        WebElement eee = driver.findElementByCssSelector("#s_lg_img");
        Actions actions = new Actions(driver);




        /* System.out.println(driver.getPageSource());
        Set<org.openqa.selenium.Cookie> cookies = driver.manage().getCookies();
        for (org.openqa.selenium.Cookie cookie : cookies) {
            System.out.println(cookie.getName()+"===="+cookie.getValue());
        }*/
    }
}
```