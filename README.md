# dsa
webscrapping

import requests
from bs4 import BeautifulSoup

HEADERS = ({'User-Agent':
			'Mozilla/5.0 (Windows NT 10.0; Win64; x64) \
			AppleWebKit/537.36 (KHTML, like Gecko) \
			Chrome/90.0.4430.212 Safari/537.36',
			'Accept-Language': 'en-US, en;q=0.5'})

# Scrape the data
def getdata(site_url):
	res = requests.get(site_url, headers=HEADERS)
	return res.text

def gethtml(site_url):

	# pass the url
	# into getdata function
	data = getdata(site_url)
	soup = BeautifulSoup(data, 'html.parser')

	# display html code
	return (soup)

site_url = "https://www.amazon.in/Columbia-Mens-wind-\
resistant-Glove/dp/B0772WVHPS/?_encoding=UTF8&pd_rd\
_w=d9RS9&pf_rd_p=3d2ae0df-d986-4d1d-8c95-aa25d2ade606&pf\
_rd_r=7MP3ZDYBBV88PYJ7KEMJ&pd_rd_r=550bec4d-5268-41d5-\
87cb-8af40554a01e&pd_rd_wg=oy8v8&ref_=pd_gw_cr_cartx&th=1"

soup = gethtml(site_url)
#print(soup)

def getCustomerName(soup):
    # find the Html tag
    # with find()
    # and convert into string
    data_string = ""
    custumer_list = []
  
    for item in soup.find_all("span", class_="a-profile-name"):
        data_string = data_string + item.get_text()
        custumer_list.append(data_string)
        data_string = ""
    return custumer_list
  
  
custumer_res = getCustomerName(soup)
print(custumer_res)




