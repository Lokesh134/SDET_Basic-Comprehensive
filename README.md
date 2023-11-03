# SDET_Basic-Comprehensive
1.Implement below Program using Java OOPs concepts – Create below three classes and corresponding variables and methods

class Account {
    protected double balance;
    protected double interestRate;

    public Account(double balance, double interestRate) {
        this.balance = balance;
        this.interestRate = interestRate;
    }

    public void calculateInterest() {
        double interest = balance * (interestRate / 100);
        balance += interest;
    }

    public void deposit(double amount) {
        balance += amount;
    }

    public void withdraw(double amount) {
        if (amount <= balance) {
            balance -= amount;
        } else {
            System.out.println("Insufficient balance");
        }
    }

    public void displayBalance() {
        System.out.println("Current balance: $" + balance);
    }
}

class SavingsAccount extends Account {
    public SavingsAccount(double balance, double interestRate) {
        super(balance, interestRate);
    }

    // Additional methods or overrides specific to SavingsAccount can be added here
}

class CurrentAccount extends Account {
    public CurrentAccount(double balance, double interestRate) {
        super(balance, interestRate);
    }

    // Additional methods or overrides specific to CurrentAccount can be added here
}

public class Main {
    public static void main(String[] args) {
        Account account1 = new SavingsAccount(1000.0, 2.5);
        Account account2 = new CurrentAccount(2000.0, 1.5);

        account1.displayBalance();
        account1.calculateInterest();
        account1.displayBalance();

        account2.displayBalance();
        account2.calculateInterest();
        account2.displayBalance();
    }
}




2.Implement below program using Python. Create a Python class Student with two variables (Name, Grade and Age).
Create a display() – To display Name, Grade and Age of an Object created using Student Class.
Create another class School which inherits from Student class and crate another method SchoolStudentDisplay() – which displays Name, Grade and Age. Which object created using School class.

class Student:
    def __init__(self, name, grade, age):
        self.name = name
        self.grade = grade
        self.age = age

    def display(self):
        print(f"Name: {self.name}, Grade: {self.grade}, Age: {self.age}")


class School(Student):
    def school_student_display(self):
        self.display()

# Creating a Student object
student1 = Student("Alice", "A", 16)

# Creating a School object (inherits from Student)
school_student1 = School("Bob", "B", 15)

# Displaying student information using the display method from the Student class
student1.display()

# Displaying student information using the SchoolStudentDisplay method from the School class
school_student1.school_student_display()


3.Launch a below browser in Firefox and verify makemytrip logo is present or not on the Page.
Implement using Selenium with Web Driver concept https://www.makemytrip.com/

 from selenium import webdriver
from selenium.webdriver.common.by import By

# Set the path to the Firefox driver executable
firefox_driver_path = 'path/to/geckodriver'

# Initialize the Firefox WebDriver
driver = webdriver.Firefox(executable_path=firefox_driver_path)

# Open the MakeMyTrip website
driver.get("https://www.makemytrip.com/")

try:
    # Wait for a few seconds to ensure the page loads completely
    driver.implicitly_wait(10)
    
    # Find the logo element using its XPath
    logo_element = driver.find_element(By.XPATH, "//div[@class='mmtHeaderLogoNew']")

    # Check if the logo is displayed on the page
    if logo_element.is_displayed():
        print("MakeMyTrip logo is present on the page.")
    else:
        print("MakeMyTrip logo is not present on the page.")
except Exception as e:
    print("An error occurred:", e)

# Close the browser
driver.quit()



 4.Launch a below browser in Chrome and click on Flights and Select OneWay to enter FROM and TO locations. ((Find the WebElements (Flights, OneWay, FROM and To Webelements using XPaths) https://www.makemytrip.com/
Note: While Implementing above Program, write generic functions to interact with the browser.

from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys

def click_element_by_xpath(driver, xpath):
    element = driver.find_element(By.XPATH, xpath)
    element.click()

def send_keys_to_element_by_xpath(driver, xpath, keys):
    element = driver.find_element(By.XPATH, xpath)
    element.send_keys(keys)

# Set the path to the Chrome driver executable
chrome_driver_path = 'path/to/chromedriver'

# Initialize the Chrome WebDriver
driver = webdriver.Chrome(executable_path=chrome_driver_path)

# Open the MakeMyTrip website
driver.get("https://www.makemytrip.com/")

try:
    # Wait for a few seconds to ensure the page loads completely
    driver.implicitly_wait(10)
    
    # Click on the "Flights" menu
    click_element_by_xpath(driver, "//li[@data-cy='menu_Flights']")

    # Click on "OneWay"
    click_element_by_xpath(driver, "//li[@data-cy='oneWayTrip']")

    # Enter the "FROM" location (e.g., Delhi) using the generic function
    send_keys_to_element_by_xpath(driver, "//input[@id='fromCity']", "Delhi")
    driver.implicitly_wait(5)  # Wait for the autocomplete options to appear
    driver.find_element(By.XPATH, "//p[text()='Delhi']").click()

    # Enter the "TO" location (e.g., Mumbai) using the generic function
    send_keys_to_element_by_xpath(driver, "//input[@id='toCity']", "Mumbai")
    driver.implicitly_wait(5)  # Wait for the autocomplete options to appear
    driver.find_element(By.XPATH, "//p[text()='Mumbai']").click()
    
    # Optionally, you can submit the form or perform other actions here
except Exception as e:
    print("An error occurred:", e)

# Close the browser
driver.quit()



5.Implement 3 and 4 Programs using TestNG Concepts and write it using @Test annotation.
To launch the browser (Repeated code) maintain it in @BeforeMethod annotation
Generate TestNG HTML Reports and find the Test Results


import org.openqa.selenium.By;
import org.openqa.selenium.Keys;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.annotations.AfterMethod;
import org.testng.annotations.BeforeMethod;
import org.testng.annotations.Test;

public class TestNGProgram3 {
    WebDriver driver;

    @BeforeMethod
    public void setup() {
        // Set the path to the Chrome driver executable
        System.setProperty("webdriver.chrome.driver", "path/to/chromedriver");
        // Initialize the Chrome WebDriver
        driver = new ChromeDriver();
    }

    @Test
    public void testMakeMyTripFlights() {
        driver.get("https://www.makemytrip.com/");

        // Click on the "Flights" menu
        driver.findElement(By.xpath("//li[@data-cy='menu_Flights']")).click();
    }

    @AfterMethod
    public void teardown() {
        // Close the browser
        driver.quit();
    }
}





import org.openqa.selenium.By;
import org.openqa.selenium.Keys;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.annotations.AfterMethod;
import org.testng.annotations.BeforeMethod;
import org.testng.annotations.Test;

public class TestNGProgram4 {
    WebDriver driver;

    @BeforeMethod
    public void setup() {
        // Set the path to the Chrome driver executable
        System.setProperty("webdriver.chrome.driver", "path/to/chromedriver");
        // Initialize the Chrome WebDriver
        driver = new ChromeDriver();
    }

    @Test
    public void testMakeMyTripFlightsAndSelectOneWay() {
        driver.get("https://www.makemytrip.com/");

        // Click on the "Flights" menu
        driver.findElement(By.xpath("//li[@data-cy='menu_Flights']")).click();

        // Click on "OneWay"
        driver.findElement(By.xpath("//li[@data-cy='oneWayTrip']")).click();

        // Enter the "FROM" location (e.g., Delhi)
        driver.findElement(By.xpath("//input[@id='fromCity']").sendKeys("Delhi");
        // Wait for the autocomplete options to appear
        driver.findElement(By.xpath("//p[text()='Delhi']")).click();

        // Enter the "TO" location (e.g., Mumbai)
        driver.findElement(By.xpath("//input[@id='toCity']").sendKeys("Mumbai");
        // Wait for the autocomplete options to appear
        driver.findElement(By.xpath("//p[text()='Mumbai']")).click();
    }

    @AfterMethod
    public void teardown() {
        // Close the browser
        driver.quit();
    }
}


6.Create a Maven Project and implement all the programs in Maven Project and add all the necessary Jars and run all the programs using Maven Commands

mvn archetype:generate -DgroupId=com.example -DartifactId=automation-example -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

<dependencies>
    <dependency>
        <groupId>org.seleniumhq.selenium</groupId>
        <artifactId>selenium-java</artifactId>
        <version>3.141.59</version> <!-- Use the latest version -->
    </dependency>
    <dependency>
        <groupId>org.testng</groupId>
        <artifactId>testng</artifactId>
        <version>7.4.0</version> <!-- Use the latest version -->
    </dependency>
</dependencies>

import org.openqa.selenium.By;
import org.openqa.selenium.Keys;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.annotations.AfterMethod;
import org.testng.annotations.BeforeMethod;
import org.testng.annotations.Test;

public class TestNGProgram4 {
    WebDriver driver;

    @BeforeMethod
    public void setup() {
        // Set the path to the Chrome driver executable
        System.setProperty("webdriver.chrome.driver", "path/to/chromedriver");
        // Initialize the Chrome WebDriver
        driver = new ChromeDriver();
    }

    @Test
    public void testMakeMyTripFlightsAndSelectOneWay() {
        driver.get("https://www.makemytrip.com/");

        // Click on the "Flights" menu
        driver.findElement(By.xpath("//li[@data-cy='menu_Flights']")).click();

        // Click on "OneWay"
        driver.findElement(By.xpath("//li[@data-cy='oneWayTrip']")).click();

        // Enter the "FROM" location (e.g., Delhi)
        driver.findElement(By.xpath("//input[@id='fromCity']").sendKeys("Delhi");
        // Wait for the autocomplete options to appear
        driver.findElement(By.xpath("//p[text()='Delhi']")).click();

        // Enter the "TO" location (e.g., Mumbai)
        driver.findElement(By.xpath("//input[@id='toCity']").sendKeys("Mumbai");
        // Wait for the autocomplete options to appear
        driver.findElement(By.xpath("//p[text()='Mumbai']")).click();
    }

    @AfterMethod
    public void teardown() {
        // Close the browser
        driver.quit();
    }
}


mvn compile

mvn test

mvn surefire-report:report

mvn clean



