# ARYA-DATAZYME-FIRST-ROUND-ASSIGNMENT
from bs4 import BeautifulSoup
import requests
import re
import json

headers1 = {"User-agent":"Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko)"}
source_url = 'https://health.usnews.com/doctors/city-index/new-jersey'
src0 = requests.get(source_url,headers=headers1).text

cities = BeautifulSoup(src0,'lxml')
finding_city = cities.find_all('div',class_='Content-o0f126-0 content kteJom')
finding_city = finding_city[2]
for a in range(0,1):
    city_list = finding_city.find_all('li',class_='List__ListItem-dl3d8e-1 kfaWAY')
    city_list = city_list[a]
    city_list_link = 'https://health.usnews.com' + city_list.a['href']
    print city_list_link
    src1 = requests.get(city_list_link,headers=headers1).text
    spl = BeautifulSoup(src1,'lxml')
    sp_div = spl.find_all('div',class_='Content-o0f126-0 content kteJom')
    sp_div = sp_div[2]
  
    for b in range(0,1):
            
        sp_list=sp_div.find_all('li',class_='List__ListItem-dl3d8e-1 kfaWAY')
        sp_list = sp_list[b]
        sp_list_link = 'https://health.usnews.com' + sp_list.a['href']  
        print sp_list_link
        url = sp_list_link
        src = requests.get(url,headers=headers1).text
        soup = BeautifulSoup(src,'lxml')
        

        for c in range(0,1):
                    
                doctor_list = soup.find_all('li', class_ = 'block-normal block-loose-for-large-up')
                doctor_list = doctor_list[c]
                doctor_link = doctor_list.h3.a['href']
                doctor_link1 = 'https://health.usnews.com' + doctor_link
                    

                src1 = requests.get(doctor_link1,headers=headers1).text
                soup1 = BeautifulSoup(src1,'lxml')
                doctor_name_l =  []
                doctor_ref = soup1.find('div', class_ ='flex-row relative' ).h1.text
                doctor_name = re.findall('[a-zA-Z0-9]\S*',str(doctor_ref))
                doctor_name = ' '.join(doctor_name)
                doctor_name_l.append(str(doctor_name))
                print doctor_name_l

                doctor_ov_l = []
                doctor_ov1 =' '
                doctor_ov = soup1.find('div', class_ ='block-normal clearfix' ).p.text
                doctor_ov = re.findall('[a-zA-Z0-9]\S*',str(doctor_ov))
                doctor_ov = doctor_ov1.join(doctor_ov)
                doctor_ov_l.append(doctor_ov)
                print doctor_ov_l
                
                doctor_ex_l = []
                doctor_ex = soup1.find_all('span', class_ ='text-large heading-normal-for-small-only right-for-medium-up')
                doctor_ex = doctor_ex[1]
                doctor_ex = doctor_ex.text.strip()
                doctor_ex_l.append(str(doctor_ex))
                print doctor_ex_l

                doctor_lan_l =[] 
                doctor_lan = soup1.find('span', class_ ='text-large heading-normal-for-small-only right-for-medium-up text-right showmore').text.strip()
                doctor_lan_l.append(str(doctor_lan))
                print doctor_lan_l
                
                doctor_loc_l =[]
                doctor_loc1 =' '
                doctor_loc = soup1.find('div', class_ ='flex-small-12 flex-medium-6 flex-large-5').p.span.text.strip()
                doctor_loc = re.findall('[a-zA-Z0-9]\S*',str(doctor_loc))
                doctor_loc = doctor_loc1.join(doctor_loc)
                doctor_loc_l.append(doctor_loc)
                print doctor_loc_l
                
                doctor_aff_l =[]
                doctor_aff = soup1.find('section', class_ ='doctors-hospitals block-loosest').p.text.strip()
                doctor_aff_l.append(str(doctor_aff))
                print doctor_aff_l
                
                doctor_sp_l =[]
                doctor_sp = soup1.find('div', class_ ='flex-row small-between').a.text.strip()
                doctor_sp_l.append(str(doctor_sp))

                doctor_subsp = soup1.find('p', class_ ='text-large block-tight').text
                doctor_sp_l.append(str(doctor_sp))
                print doctor_sp_l
                print ' '
                doctor_ed = soup1.find_all(class_ ="block-loosest")[5]
                doctor_ed1 = doctor_ed.find_all('li')
                doctor_ed5 = ' '
                doctor_ed6 = []
                for i in doctor_ed1:
                    doctor_ed2 = str(i.text)
                    doctor_ed2 = re.findall('[a-zA-Z0-9]\S*',doctor_ed2)
                    doctor_ed2 = doctor_ed5.join(doctor_ed2)
                    doctor_ed6.append(doctor_ed2)
                print doctor_ed6
                print ' '
                doctor_cert2 = []
                doctor_cert1 = ' '  
                doctor_ed3 = soup1.find_all(class_ ="block-loosest")[6]
                doctor_ed14 = doctor_ed3.find_all('li')
                for i in doctor_ed14:
                    doctor_cert = str(i.text)
                    doctor_cert = re.findall('[a-zA-Z0-9]\S*',doctor_cert)
                    doctor_cert = doctor_cert1.join(doctor_cert)
                    doctor_cert2.append(doctor_cert)
                print doctor_cert2
                
                
                c += 1
        b += 1
    a += 1
