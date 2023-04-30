# fix-selenium-bug Chrome opens with "Data;"
# Selenium WebDriver.get(url) does not open the URL

**SAVE 10 HRS OF YOUR LIFE...**  
Ctrl+c, Ctrl+v  

```java
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.chrome.ChromeOptions;

import java.util.concurrent.TimeUnit;

public class Main {
    public static void main(String[] args) {
        System.setProperty("webdriver.chrome.driver","YOUR_PATH_TO_DRIVER_HERE"); //chromedriver 112.0.++ in my situation

        ChromeOptions options = new ChromeOptions();
        options.addArguments("--start-maximized");
        options.addArguments("--test-type");
        options.addArguments("--no-sandbox");
        options.addArguments("--ignore-certificate-errors");
        options.addArguments("--disable-popup-blocking");
        options.addArguments("--disable-default-apps");
        options.addArguments("--disable-extensions-file-access-check");
        options.addArguments("--incognito");
        options.addArguments("--disable-infobars");
        options.addArguments("--disable-gpu");
        options.addArguments("--remote-allow-origins=*");
        options.addArguments("--disable-dev-shm-usage");
        options.addArguments("--disable-notifications"); //delete "Chrome is being controlled by automated test software"
        options.setExperimentalOption("excludeSwitches", new String[]{"enable-automation"}); //delete "Chrome is being controlled by automated test software"

        options.setExperimentalOption("useAutomationExtension", false);
        options.addArguments("--remote-debugging-port=9225");
        ChromeDriver driver = new ChromeDriver(options);

        driver.manage().timeouts().implicitlyWait(5, TimeUnit.SECONDS);
        driver.get("https://google.com/");
        System.out.println(driver.getTitle());
    }
}
```
