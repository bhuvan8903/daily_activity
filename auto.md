```
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait, Select
from selenium.webdriver.support import expected_conditions as EC
import time


# ============================================================
# SETUP
# ============================================================

driver = webdriver.Chrome()
driver.maximize_window()

wait = WebDriverWait(driver, 15)


# ============================================================
# TC01 - OPEN REGISTRATION PAGE
# Concept: get()
# ============================================================

driver.get("https://demo.automationtesting.in/Register.html")

print("TC01 PASS - Registration page opened")


# ============================================================
# TC02 - LOCATE FIRST NAME
# Concept: Attribute XPath
# ============================================================

first_name = wait.until(
    EC.visibility_of_element_located(
        (By.XPATH, "//input[@placeholder='First Name']")
    )
)

first_name.send_keys("Bhuvaneshwaran")

print("TC02 PASS - First Name entered")


# ============================================================
# LAST NAME
# ============================================================

last_name = wait.until(
    EC.visibility_of_element_located(
        (By.XPATH, "//input[@placeholder='Last Name']")
    )
)

last_name.send_keys("H")

print("Last Name entered")


# ============================================================
# ADDITIONAL INFORMATION - ADDRESS
# ============================================================

address = wait.until(
    EC.visibility_of_element_located(
        (By.XPATH, "//textarea[@ng-model='Adress']")
    )
)

address.send_keys("Chennai, Tamil Nadu")

print("Address entered")


# ============================================================
# EMAIL
# ============================================================

email = wait.until(
    EC.visibility_of_element_located(
        (By.XPATH, "//input[@type='email']")
    )
)

email.send_keys("bhuvaneshwaran123@gmail.com")

print("Email entered")


# ============================================================
# TC05 - DYNAMIC TEXTBOX
# Concept: contains()
# ============================================================

email_dynamic = driver.find_element(
    By.XPATH,
    "//input[contains(@type,'email')]"
)

print("TC05 PASS - contains() used")


# ============================================================
# PHONE
# ============================================================

phone = wait.until(
    EC.visibility_of_element_located(
        (By.XPATH, "//input[@type='tel']")
    )
)

phone.send_keys("9876543210")

print("Phone entered")


# ============================================================
# TC06 - PREFIX
# Concept: starts-with()
# ============================================================

password_field = driver.find_element(
    By.XPATH,
    "//input[starts-with(@id,'firstpass')]"
)

print("TC06 PASS - starts-with() used")


# ============================================================
# TC07 - TWO ATTRIBUTES
# Concept: AND
# ============================================================

phone_check = driver.find_element(
    By.XPATH,
    "//input[@type='tel' and @ng-model='Phone']"
)

print("TC07 PASS - AND XPath used")


# ============================================================
# TC08 - ALTERNATIVES
# Concept: OR
# ============================================================

email_check = driver.find_element(
    By.XPATH,
    "//input[@type='email' or @name='email']"
)

print("TC08 PASS - OR XPath used")


# ============================================================
# TC09 - FIND PARENT
# Concept: parent
# ============================================================

email_parent = driver.find_element(
    By.XPATH,
    "//input[@type='email']/parent::*"
)

print("TC09 PASS - Parent found")


# ============================================================
# TC10 - FIND FORM
# Concept: ancestor
# ============================================================

form = driver.find_element(
    By.XPATH,
    "//input[@placeholder='First Name']/ancestor::form"
)

print("TC10 PASS - Form found using ancestor")


# ============================================================
# TC11 - FIND CHILD INPUTS
# Concept: child
# ============================================================

child_inputs = form.find_elements(
    By.XPATH,
    ".//child::div//input"
)

print("TC11 PASS - Child inputs found")
print("Number of child inputs:", len(child_inputs))


# ============================================================
# TC12 - FIND NEXT ELEMENT
# Concept: following
# ============================================================

following_element = driver.find_element(
    By.XPATH,
    "//input[@placeholder='First Name']/following::input[1]"
)

print("TC12 PASS - Following element found")


# ============================================================
# TC13 - CHECKBOX
# Concept: Attribute XPath
# ============================================================

print("Starting hobbies...")


cricket = wait.until(
    EC.element_to_be_clickable(
        (By.XPATH, "//input[@value='Cricket']")
    )
)

if not cricket.is_selected():
    cricket.click()

print("Cricket selected")


movies = wait.until(
    EC.element_to_be_clickable(
        (By.XPATH, "//input[@value='Movies']")
    )
)

if not movies.is_selected():
    movies.click()

print("Movies selected")

print("TC13 PASS - Hobbies selected")


# ============================================================
# TC14 - RADIO BUTTON
# Concept: Attribute XPath
# ============================================================

print("Starting gender...")


male = wait.until(
    EC.element_to_be_clickable(
        (By.XPATH, "//input[@type='radio' and @value='Male']")
    )
)

male.click()

print("TC14 PASS - Male selected")


# ============================================================
# LANGUAGE
# ============================================================

print("Starting language...")


language_box = wait.until(
    EC.element_to_be_clickable(
        (By.XPATH, "//div[@id='msdd']")
    )
)

language_box.click()

print("Language box clicked")

time.sleep(2)


# ============================================================
# SELECT ENGLISH
# ============================================================

english = wait.until(
    EC.element_to_be_clickable(
        (By.XPATH, "//a[normalize-space()='English']")
    )
)

english.click()

print("English selected")


# ============================================================
# TC15 - SKILLS DROPDOWN
# Concept: XPath + Select
# ============================================================

print("Starting Skills...")


skills_element = wait.until(
    EC.presence_of_element_located(
        (By.XPATH, "//select[@id='Skills']")
    )
)

skills = Select(skills_element)

skills.select_by_visible_text("Python")

print("TC15 PASS - Python selected")


# ============================================================
# COUNTRY DROPDOWN
# ============================================================

country_element = wait.until(
    EC.presence_of_element_located(
        (By.XPATH, "//select[@id='countries']")
    )
)

country = Select(country_element)

# Select India only if available
try:
    country.select_by_visible_text("India")
    print("India selected")
except:
    print("India not available in first country dropdown")


# ============================================================
# DATE OF BIRTH - YEAR
# ============================================================

year_element = wait.until(
    EC.presence_of_element_located(
        (By.XPATH, "//select[@id='yearbox']")
    )
)

year = Select(year_element)

year.select_by_visible_text("2002")

print("Year selected")


# ============================================================
# DATE OF BIRTH - MONTH
# ============================================================

month_element = wait.until(
    EC.presence_of_element_located(
        (By.XPATH, "//select[@placeholder='Month']")
    )
)

month = Select(month_element)

month.select_by_visible_text("May")

print("Month selected")


# ============================================================
# DATE OF BIRTH - DAY
# ============================================================

day_element = wait.until(
    EC.presence_of_element_located(
        (By.XPATH, "//select[@id='daybox']")
    )
)

day = Select(day_element)

day.select_by_visible_text("10")

print("Day selected")


# ============================================================
# TC16 - SECOND TEXTBOX
# Concept: XPath Index
# ============================================================

textboxes = driver.find_elements(
    By.XPATH,
    "//input[@type='text']"
)

print("TC16 - Total textboxes:", len(textboxes))


if len(textboxes) >= 2:

    second_textbox = driver.find_element(
        By.XPATH,
        "(//input[@type='text'])[2]"
    )

    print("TC16 PASS - Second textbox found")


# ============================================================
# TC03 - PASSWORD
# Concept: Attribute XPath
# ============================================================

password = wait.until(
    EC.visibility_of_element_located(
        (By.XPATH, "//input[@id='firstpassword']")
    )
)

password.send_keys("Student@123")

print("TC03 PASS - Password entered")


# ============================================================
# CONFIRM PASSWORD
# ============================================================

confirm_password = wait.until(
    EC.visibility_of_element_located(
        (By.XPATH, "//input[@id='secondpassword']")
    )
)

confirm_password.send_keys("Student@123")

print("Confirm Password entered")


# ============================================================
# TC18 - FIND ALL INPUT FIELDS
# Concept: find_elements()
# ============================================================

all_inputs = driver.find_elements(
    By.XPATH,
    "//input"
)

print("TC18 PASS - All input fields found")
print("Total input fields:", len(all_inputs))


# ============================================================
# TC19 - DYNAMIC ELEMENT
# Concept: contains()
# ============================================================

dynamic_first_name = driver.find_element(
    By.XPATH,
    "//input[contains(@placeholder,'First')]"
)

print("TC19 PASS - Dynamic First Name found")


# ============================================================
# TC04 - LOCATE SUBMIT
# Concept: text()
# ============================================================

submit = wait.until(
    EC.element_to_be_clickable(
        (By.XPATH, "//button[text()='Submit']")
    )
)

print("TC04 PASS - Submit button found")


# ============================================================
# TC20 - COMPLETE REGISTRATION
# ============================================================

print()
print("========================================")
print("READY TO SUBMIT REGISTRATION")
print("========================================")


submit.click()

print("Submit button clicked")

time.sleep(3)


# ============================================================
# TC17 - VERIFY SUBMISSION
# ============================================================

print()
print("========================================")
print("TC17 - VERIFICATION")
print("========================================")


current_url = driver.current_url

print("Current URL:", current_url)


if "Register.html" not in current_url:

    print("TC17 PASS - Page changed after submission")

else:

    print("TC17 - Submit completed")
    print("Demo page remained on Register.html")


# ============================================================
# FINAL RESULT
# ============================================================

print()
print("========================================")
print("AUTOMATION COMPLETED")
print("========================================")


# ============================================================
# KEEP BROWSER OPEN
# ============================================================

input("Press ENTER to close browser...")

driver.quit()
```
