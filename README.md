# Importar os dados
import pandas as pd
from time import sleep

# Dados Web
from selenium import webdriver  # Navegador
from selenium.webdriver.common.by import By  # Elementos
from selenium.webdriver.chrome.service import Service

#Lógica
arquivo_desafio = 'challenge.xlsx'
url_do_site = 'https://rpachallenge.com/'

df = pd.read_excel(arquivo_desafio)
chrome = webdriver.Chrome(service=Service("chromedriver.exe"))  # Inicializar o navegador fora do loop
chrome.get(url_do_site)  # Abrir o site uma vez fora do loop

sleep(5)

for index, row in df.iterrows():
    elemento_texto_FirstName = chrome.find_element(By.XPATH, '//*[@ng-reflect-name="labelFirstName"]')
    elemento_texto_FirstName.send_keys(str(row['FirstName']))

    elemento_texto_LastName = chrome.find_element(By.XPATH, '//*[@ng-reflect-name="labelLastName"]')
    elemento_texto_LastName.send_keys(row['Last Name'])

    elemento_texto_CompanyName = chrome.find_element(By.XPATH, '//*[@ng-reflect-name="labelCompanyName"]')
    elemento_texto_CompanyName.send_keys(str(row['Company Name']))

    elemento_texto_RoleinCompany = chrome.find_element(By.XPATH, '//*[@ng-reflect-name="labelRole"]')
    elemento_texto_RoleinCompany.send_keys(str(row['Role in Company']))

    elemento_texto_Address = chrome.find_element(By.XPATH, '//*[@ng-reflect-name="labelAddress"]')
    elemento_texto_Address.send_keys(str(row['Address']))

    elemento_texto_Email = chrome.find_element(By.XPATH,'//*[@ng-reflect-name="labelEmail"]')
    elemento_texto_Email.send_keys(str(row['Email']))

    elemento_texto_PhoneNumber = chrome.find_element(By.XPATH,'//*[@ng-reflect-name="labelPhone"]')
    elemento_texto_PhoneNumber.send_keys(row['Phone Number'])
                                               
    elemento_texto_Submit = chrome.find_element(By.XPATH, '/html/body/app-root/div[2]/app-rpa1/div/div[2]/form/input')
    elemento_texto_Submit.click()

# Manter o navegador aberto após a execução
print("Finalizado")
input("Pressione Enter para fechar o navegador...")
