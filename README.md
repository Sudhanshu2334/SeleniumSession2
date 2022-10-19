package com.runner;

import java.time.Duration;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

import io.cucumber.java.en.Given;
import io.cucumber.java.en.Then;
import io.cucumber.java.en.When;
import io.github.bonigarcia.wdm.WebDriverManager;
import pages.Loginpage;

public class Teststep_Pom {
	
	WebDriver driver;
	Loginpage login;
	
	@Given("browser is open")
	public void browser_is_open() {
		WebDriverManager.chromedriver().setup();
		WebDriver driver = new ChromeDriver();
		login=new Loginpage(driver);
		driver.manage().window().maximize();
		driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(30));
		driver.manage().timeouts().pageLoadTimeout(Duration.ofSeconds(30));
		driver.navigate().to("https://example.testproject.io/web/");
	}

	@Given("user is on login page")
	public void user_is_on_login_page() {
		System.out.println("browser is open");
	  
	}
	@When("user enters email as {string}   and  password as {string}")
	public void user_enters_email_as_and_password_as(String username, String password) {
		login.enteremail(username);
		login.enterpassword(password);	
	}

	@When("user clicks on login")
	public void user_clicks_on_login() {
     login.click_login();
	System.out.println("user is on login page");
	}

	@Then("user is navigated to the home page")
	public void user_is_navigated_to_the_home_page() throws Exception {
		driver.findElement(By.id("logout")).isDisplayed();
		Thread.sleep(2000);
		driver.close();
	}

}



	
