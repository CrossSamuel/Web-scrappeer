# Web-scrappeer
A simple Web scrapper
#import libary for web scrapping
from bs4 import BeautifulSoup as Soup
import re
import request as HTTP

#Main Function for scraping
def main(emotion):

    #IMDb url for drama genere of movie against emotion sad
    if(emotion == "Sad"):
        urlhere = 'http://www.imdb.com/search/title?genres=drama&title_type=feature&sort=moviemeter, asc'

    #Drama genre of movie against emotion Disgust
    elif(emotion == 'Disgust'):
        urlhere = 'http://www.imdb.com/search/title?genres=Musical&title_type=feature&sort=moviemeter, asc'

    #Family genre of movie against emotion Anger
    elif(emotion == 'Anger'):
        urlhere = 'http://www.imdb.com/search/title?genres=Family&title_type=feature&sort=moviemeter, asc'

    #Thriller genre of movie against emotion Anticipation
    elif(emotion == 'Anticipation'):
        urlhere = 'http://www.imdb.com/search/title?genres=Thriller&title_type=feature&sort=moviemeter, asc'

    
    # genre of movie against emotion Fear 
    elif(emotion == "Fear"): 
        urlhere = 'http://www.imdb.com/search/title?genres=sport&title_type=feature&sort=moviemeter, asc'
  
    #Thriller genre of movie against emotion Enjoyment 
    elif(emotion == "Enjoyment"): 
        urlhere = 'http://www.imdb.com/search/title?genres=thriller&title_type=feature&sort=moviemeter, asc'
  
    #Western genre of movie against emotion Trust 
    elif(emotion == "Trust"): 
        urlhere = 'http://www.imdb.com/search/title?genres=western&title_type=feature&sort=moviemeter, asc'
  
    #Film_noir genre of movie against emotion Surprise 
    elif(emotion == "Surprise"): 
        urlhere = 'http://www.imdb.com/search/title?genres=film_noir&title_type=feature&sort=moviemeter, asc'
  
    # HTTP request to get the data of the whole page 
    response = HTTP.get(urlhere) 
    data = response.text 
  
    # Parsing the data using 
    # BeautifulSoup 
    soup = SOUP(data, "lxml") 
  
    # Extract movie titles from the data using regex 
    title = soup.find_all("a", attrs = {"href" : re.compile(r'\/title\/tt+\d*\/')}) 
    return title 
  
# Driver Function 
if __name__ == '__main__': 
  
    emotion = input("Enter the emotion: ") 
    a = main(emotion) 
    count = 0
  
    if(emotion == "Disgust" or emotion == "Anger"
                           or emotion =="Surprise"
                           or emotion == "sad" ): 
  
        for i in a: 
  
            # Splitting each line of the IMDb data to scrape movies 
            tmp = str(i).split('>;') 
  
            if(len(tmp) == 3): 
                print(tmp[1][:-3]) 
  
            if(count > 13): 
                break
            count += 1
    else: 
        for i in a: 
            tmp = str(i).split('>') 
  
            if(len(tmp) == 3): 
                print(tmp[1][:-3]) 
  
            if(count > 11): 
                break
            count+=1
