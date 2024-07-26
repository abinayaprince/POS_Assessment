//TEST CASE 01:
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.interactions.Actions;
import org.openqa.selenium.JavascriptExecutor;
import java.util.List;
import java.util.Set;
import java.util.concurrent.TimeUnit;


public class POS_001 {
    public static void main(String[] args) {
        System.setProperty("webdriver.chrome.driver", "C:\Program Files (x86)\Google\Chrome\Application\chrome.exe"); 
        WebDriver driver = new ChromeDriver();

        try {
            driver.get("https://pos.com.my");

            JavascriptExecutor js = (JavascriptExecutor) driver;
            js.executeScript("window.scrollBy(0,350)", "");

            WebElement buyInsuranceButton = driver.findElement(By.xpath("//button[text()='Buy Insurance']"));
            buyInsuranceButton.click();

            driver.manage().timeouts().implicitlyWait(3, TimeUnit.SECONDS);
            Set<String> windowHandles = driver.getWindowHandles();
            String newTabHandle = (String) windowHandles.toArray()[windowHandles.size() - 1];
            driver.switchTo().window(newTabHandle);

            String expectedUrl = "https://insurance.pos.com.my";
            String actualUrl = driver.getCurrentUrl();

            if (actualUrl.equals(expectedUrl)) {
                System.out.println("Test Passed: URL is correct.");
            } else {
                System.out.println("Test Failed: Expected URL '" + expectedUrl + "', but got '" + actualUrl + "'.");
            }

            WebElement driveCarButton = driver.findElement(By.xpath("//button[text()='I drive a car']"));
            driveCarButton.click();
            driver.manage().timeouts().implicitlyWait(2, TimeUnit.SECONDS); // Wait for the section to appear

            WebElement newSection = driver.findElement(By.xpath("//h2[text()='Ok, let’s get to know you']"));
            List<WebElement> fields = driver.findElements(By.xpath("//input[@type='text']"));

            if (newSection.isDisplayed() && fields.size() == 5) {
                System.out.println("Test Passed: 'I drive a car' button shows new section with 5 fields.");
            } else {
                System.out.println("Test Failed: New section or fields not found for 'I drive a car'.");
            }

            driver.navigate().refresh();
            driver.manage().timeouts().implicitlyWait(3, TimeUnit.SECONDS);

            WebElement rideMotorcycleButton = driver.findElement(By.xpath("//button[text()='I ride a motorcycle']"));
            rideMotorcycleButton.click();
            driver.manage().timeouts().implicitlyWait(2, TimeUnit.SECONDS); // Wait for the section to appear

            newSection = driver.findElement(By.xpath("//h2[text()='Ok, let’s get to know you']"));
            fields = driver.findElements(By.xpath("//input[@type='text']"));

            if (newSection.isDisplayed() && fields.size() == 5) {
                System.out.println("Test Passed: 'I ride a motorcycle' button shows new section with 5 fields.");
            } else {
                System.out.println("Test Failed: New section or fields not found for 'I ride a motorcycle'.");
            }
        } finally {
            driver.quit();
        }
    }
}


//TEST CASE :02

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.interactions.Actions;
import java.util.Set;
import java.util.concurrent.TimeUnit;

public class POS_002 {
    public static void main(String[] args) {
        System.setProperty("webdriver.chrome.driver", "C:\Program Files (x86)\Google\Chrome\Application\chrome.exe");
        WebDriver driver = new ChromeDriver();

        try {
            driver.get("https://pos.com.my");

            Actions actions = new Actions(driver);
            WebElement sendMenu = driver.findElement(By.xpath("//a[text()='Send']"));
            actions.moveToElement(sendMenu).perform();

            WebElement parcelOption = driver.findElement(By.xpath("//a[text()='Parcel']"));
            parcelOption.click();

            driver.manage().timeouts().implicitlyWait(3, TimeUnit.SECONDS);
            String expectedUrlSendParcel = "https://www.pos.com.my/parcel";
            String actualUrlSendParcel = driver.getCurrentUrl();

            if (actualUrlSendParcel.equals(expectedUrlSendParcel)) {
                System.out.println("Test Passed: Navigated to Send Parcel page.");
            } else {
                System.out.println("Test Failed: Expected URL '" + expectedUrlSendParcel + "', but got '" + actualUrlSendParcel + "'.");
            }

            WebElement createShipmentButton = driver.findElement(By.xpath("//button[text()='Create shipment now']"));
            actions.moveToElement(createShipmentButton).perform();
            createShipmentButton.click();

            driver.manage().timeouts().implicitlyWait(3, TimeUnit.SECONDS);
            Set<String> windowHandles = driver.getWindowHandles();
            String newTabHandle = (String) windowHandles.toArray()[windowHandles.size() - 1];
            driver.switchTo().window(newTabHandle);

            String expectedUrlConsignment = "https://send.pos.com.my/home/e-connote?lg=en";
            String actualUrlConsignment = driver.getCurrentUrl();

            if (actualUrlConsignment.equals(expectedUrlConsignment)) {
                System.out.println("Test Passed: URL is correct for e-Consignment Note forms.");
            } else {
                System.out.println("Test Failed: Expected URL '" + expectedUrlConsignment + "', but got '" + actualUrlConsignment + "'.");
            }

            WebElement senderInfoSection = driver.findElement(By.xpath("//h2[text()='Sender Info']"));
            WebElement receiverInfoSection = driver.findElement(By.xpath("//h2[text()='Receiver Info']"));
            WebElement parcelInfoSection = driver.findElement(By.xpath("//h2[text()='Parcel Info']"));
            WebElement summarySection = driver.findElement(By.xpath("//h2[text()='Summary']"));

            if (senderInfoSection.isDisplayed() && receiverInfoSection.isDisplayed() &&
                parcelInfoSection.isDisplayed() && summarySection.isDisplayed()) {
                System.out.println("Test Passed: All required sections are displayed.");
            } else {
                System.out.println("Test Failed: One or more required sections are missing.");
            }
        } finally {
            driver.quit();
        }
    }
}
