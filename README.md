# automated-whatsapp-online-tracker
find thebelow codeand documentation its a step by step process 
1)pip install selenium
2)download the chrome driver as according to your browser version,my chrome browser version is Version 99.0.4844.51 (Official Build) (64-bit)
driver download link:https://chromedriver.chromium.org/downloads,
i extracted the chrome.exe file and save in my desktop ,and copy its path which i have used in the code.

in ur python editor write this code and save as test.py
3)from selenium import webdriver

browser = webdriver.Chrome(r"C:\Users\LENOVO\OneDrive\Desktop\chromedriver.exe")
browser.get('http://www.google.com')
You should now see a browser window opening and loading the Google homepage.
####WRITING CODE FOR TIME SPAN
from datetime import datetime
now=datetime.now()
current_time=now.strftime("%H:%M:%S")

from selenium import webdriver
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.common.by import By
import time
import os

# XPath selectors
NEW_CHAT_BTN = '/html[1]/body[1]/div[1]/div[1]/div[1]/div[3]/div[1]/header[1]/div[2]/div[1]/span[1]/div[2]/div[1]/span[1]'
INPUT_TXT_BOX = '/html[1]/body[1]/div[1]/div[1]/div[1]/div[2]/div[1]/span[1]/div[1]/span[1]/div[1]/div[1]/div[1]/label[1]/div[1]/div[2]'
ONLINE_STATUS_LABEL = '/html[1]/body[1]/div[1]/div[1]/div[1]/div[4]/div[1]/header[1]/div[2]/div[2]/span[1]'

# Replace below with the list of targets to be tracked
TARGETS = {'"contact name"': 'phone number 1', '"contactname2"': 'phonenumber2'}

# Replace below path with the absolute path
browser = webdriver.Chrome(r"C:\Users\LENOVO\OneDrive\Desktop\chromedriver.exe")

# Load Whatsapp Web page
browser.get("https://web.whatsapp.com/")
wait = WebDriverWait(browser, 600)

while True:
    # Clear screen
    os.system('cls')

    # For each target
    for target in TARGETS:
        tryAgain = True

        # Wait untill new chat button is visible
        new_chat_title = wait.until(EC.presence_of_element_located((By.XPATH, NEW_CHAT_BTN)))

        while (tryAgain):
            try:
                # Click on new chat button
                new_chat_title.click()

                # Wait untill input text box is visible
                input_box = wait.until(EC.presence_of_element_located((By.XPATH, INPUT_TXT_BOX)))

                time.sleep(0.5)

                # Write phone number
                input_box.send_keys(TARGETS[target])

                time.sleep(1)

                # Press enter to confirm the phone number
                input_box.send_keys(Keys.ENTER)

                time.sleep(5)
                tryAgain = False

                try:
                    try:
                        browser.find_element_by_xpath(ONLINE_STATUS_LABEL)
                        print(target + ' is online')
                        print("At:",current_time)
                    except:
                        print(target + ' is offline')
                        print("At:",current_time)
                    time.sleep(1)
                except:
                    print('Exception 1')
                    time.sleep(10)
            except:
                print('Exception 2')
                time.sleep(4)
