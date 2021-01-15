# PageRank  
Is a way of measuring the importance of web pages. It can be understood as an algorithm used by Google Search to rank web pages in their search results.  
This repository contains certain files of code tasked with implementing a simple **Search Spider**, **Page Ranker** and a **Visualizer**. To be precise, the program crawls a website and pulls a series of pages into the database (SQLite in our case), recording the links between the pages.  


### Workflow  
The python file `spider.py` is tasked with accepting a URL from the user and pulling series of pages into the database, which happens to be SQLite in our case because of the presence of a default package named *sqlite3* in python. A thing to remember is that if we restart the program again and tell it to crawl more pages, it will not re-crawl any pages already in the database. Upon restart it goes to a random non-crawled page and starts there. So **each successive run of spider.py is additive**.  

If we want to dump the contents of the *spider.sqlite* file, we can simply run the `spdump.py` file. This shows the number of incoming links, the old page rank, the new page rank, the ID of the page, and the URL of the page. **The spdump.py program only shows pages that have at least one incoming link to them**.

Once we have a few pages in the database, we can run Page Rank on the pages using the `sprank.py` program. We simply tell it how many Page Rank iterations to run. We can dump the content of the database again to see that the page rank has been updated.

We can run `sprank.py` as many times as we like and it will simply refine the page rank the more times we run it. We can even run sprank.py a few times and then go spider a few more pages with spider.py and then run sprank.py to converge the page ranks.

If at any point of time we feel that we want to re-calculate the page rank without re-spidering the web pages, we can simply take the help of `spreset.py`, and all the web pages will be set to a rank of *1.0*.  

### Visualization  
_**We'll have to keep in mind to run `sprank.py` long enough so that the page ranks converge.**_  
Finally, if we'd want to visualize the current top pages in terms of page rank, we'd run `spjson.py` file to write the pages out in JSON format to be viewed in a web browser. The JSON output will then be created on `spider.js` file. We'll be prompted for the number of nodes to be visualized. We can view this data by opening the file `force.html` in our browser. This shows an automatic layout of nodes and links. We can click and drag any node and play around!  

This visualization is provided using the force layout called `d3.v2.js`, which is a JavaScript library for producing dynamic, interactive data visualization in web browsers.  

_**PS : **_ If we re-run the other utilities and then re-run *spjson.py* - we merely have to press refresh in the browser to get the new data from *spider.js*.
