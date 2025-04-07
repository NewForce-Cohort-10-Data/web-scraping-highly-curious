## Webscraping

In this exercise, you'll practice using BeautifulSoup to parse the content of a web page. The page that you'll be scraping, https://realpython.github.io/fake-jobs/, contains job listings. Your job is to extract the data on each job and convert into a pandas DataFrame.

1. Start by performing a GET request on the url above and convert the response into a BeautifulSoup object.  
a. Use the .find method to find the tag containing the first job title ("Senior Python Developer"). Hint: can you find a tag type and/or a class that could be helpful for extracting this information? Extract the text from this title.  
b. Now, use what you did for the first title, but extract the job title for all jobs on this page. Store the results in a list.  
c. Finally, extract the companies, locations, and posting dates for each job. For example, the first job has a company of "Payne, Roberts and Davis", a location of "Stewartbury, AA", and a posting date of "2021-04-08". Ensure that the text that you extract is clean, meaning no extra spaces or other characters at the beginning or end.  
d. Take the lists that you have created and combine them into a pandas DataFrame. 

2. Next, add a column that contains the url for the "Apply" button. Try this in two ways.   
    a. First, use the BeautifulSoup find_all method to extract the urls.  
    b. Next, get those same urls in a different way. Examine the urls and see if you can spot the pattern of how they are constructed. Then, build the url using the elements you have already extracted. Ensure that the urls that you created match those that you extracted using BeautifulSoup. Warning: You will need to do some string cleaning and prep in constructing the urls this way. For example, look carefully at the urls for the "Software Engineer (Python)" job and the "Scientist, research (maths)" job.
    
3. Finally, we want to get the job description text for each job.  
    a. Start by looking at the page for the first job, https://realpython.github.io/fake-jobs/jobs/senior-python-developer-0.html. Using BeautifulSoup, extract the job description paragraph.  
    b. We want to be able to do this for all pages. Write a function which takes as input a url and returns the description text on that page. For example, if you input "https://realpython.github.io/fake-jobs/jobs/television-floor-manager-8.html" into your function, it should return the string "At be than always different American address. Former claim chance prevent why measure too. Almost before some military outside baby interview. Face top individual win suddenly. Parent do ten after those scientist. Medical effort assume teacher wall. Significant his himself clearly very. Expert stop area along individual. Three own bank recognize special good along.".  
    c. Use the [.apply method](https://pandas.pydata.org/docs/reference/api/pandas.Series.apply.html) on the url column you created above to retrieve the description text for all of the jobs.

    #########################################################################################

    BONUS
    ## Webscraping Bonus

1. Navigate to https://www.billboard.com/charts/hot-100/. Using BeautifulSoup, extract out the This Week, artist, song, Last Week, Peak Position, and Weeks on Chart values into a pandas DataFrame. Hint: The HTML for the number one ranked song is slightly different from that of the rest of the songs.

2. After getting the code working for the current chart, navigate to last week's chart. Notice how the url for the page changes. Write a function which will, given a date, return a pandas DataFrame containing the Billboard chart data for that date.

3. Write a loop to retrieve the Billboard chart data for the last 10 weeks.


NIGHTMARE MODE
## Web Scraping the Ryman Calendar

In this exercise, your objective is to use BeautifulSoup in order to obtain a dataset of upcoming events at the Ryman. This information is available at https://ryman.com/events/, but you will take the contents of this website and convert it into a pandas DataFrame.

The website splits the events across multiple pages, but start by just working on the first page. Later on in the exercise, you'll take what you've done for the first page and apply it across other pages.

1. Start by using either the inspector or by viewing the page source. Can you identify a tag that might be helpful for finding the names of all performers? For now, just worry about the headliner and don't worry about the opener. (Eg. For Vince Gill, featuring Wendy Moten, we only care about Vince Gill.) Make use of this to create a list containing just the names of each inductee.

2. Next, try and find a tag that could be used to find the date and time for each show. Extract these into a list. Challenge: Convert these into two lists, one containing the date and the other containing the time. (Eg. split Mar 9, 2023 8:00 PM into Mar 9, 2023 and 8:00 PM.) 

3. Take the lists you created on parts 1 and 2 and convert them into a pandas DataFrame.

4. **Bonus #1:**: Add to your data frame the opening act for all shows that list an opener.

5. **Bonus #2:**: Now, let's see if we can get the results beyond the first page. For this, you'll need to Web Developer Tools of your browser and navigate to the Network tab. Click the "Load More Events" button and you should see a GET request to the www.ryman.com domain.  
    a. Inspect this request and you should see that it goes to a URL like "https://www.ryman.com/events/events_ajax/24?category=0&venue=0&team=0&exclude=&per_page=12&came_from_page=event-list-page". In your Jupyter notebook, send a get request to this url and inspect the results.  
    b. You should find that the results that you get are HTML, but that they are not exactly formatted in a way that can be parsed. See if you can clean up the results set so that you can extract out the same information as above.  
    c. Create a DataFrame that contains data for the next 60 shows.