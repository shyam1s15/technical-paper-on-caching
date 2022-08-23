
# Caching

Hello readers, Thankyou for giving me time, It would take 5 mins of read, please enjoy yourself the article.

Caching is technique to store & access frequently used data from one place,  applications perform dramatically faster and cost significantly less at scale.

## Different Caching Approaches

Major web developement Caching types are

    1.  Web Caching (Browser/ Proxy/ Gateway
        * Browser Caching (quickly navigate pages) 
        * Proxy Gateway Cache (E.g.: DNS data that resolve domain names)
    2.  Data Caching
        * DB driven apps
        * stores frequent used data to server & reduce round trips to & from DB
    3.  Application/ Output Caching
        * stores raw html pages ( if your js/ react app does not update, try hard refresh in browser )
        * EX (headers/ footers)
    4.  Distributed Caching/ Clustered Caching
        * Fanng products & tech uses special distributed servers to allow webserver to retrive data
          quickly to & from these server to get access of contents quickly (some celebreties photos/videos). 

## Super technical stuffs ahead/ Case Study on Facebook Caching

Facebook Content Distribution Network (FBCDN) is responsible to provide photos and videos to all it's users.
where FBCDN uses **(Heystack, f4)** it's backend caching system.

These Caches are stored on NAND - flash based ssds which give high speed data access.

```Caching is all about Hit rates, thus Meta is using various algorithms, one of the best is clairvoyant```
The clairvoyant algorithm relies on future information and is unattainable in practice, but provides an upper bound on achievable hit ratios.
![Caching Algorithm Mesurement](/images/algorithm_measures.png)
<!-- https://github.com/shyam1s15/technical-paper-on-caching/blob/master/images/algorithm_measures.png -->
As we can see Clairvoyant is fastest but due to implementation issues, again facebook team has to find another solution which can support their heavy traffic as well as hardware.

Again to overcome this problem, they have switched to another algorithm called **BlockCache** which applies the Segmented LRU logic to large fixed-size blocks of items.

In a nutshell, BlockCache restricts its writes to fixed-sized blocks that are aligned in the SSD’s logical address space. These logical blocks were configured to be 64MiB and contain hundreds of photos and video blobs with varying sizes.

BlockCache is more emphasize on High hit rate & lower write amplification so does not decreases the throughput and longer the lifespan of the SSD.

### Web Caching (Browser/Proxy/Gateway)

Browser, Proxy, and Gateway caching work differently but have the same goal: to reduce overall network traffic and latency. Browser caching is controlled at the individual user level; where as, proxy and gateway is on a much larger scale. 

The latter two allow for cached information to be shared across larger groups of users. Commonly cached data could be DNS (Domain Name Server) data, used to resolve domain names to the IP addresses and mail server records.

This data type changes infrequently and is best cached for longer periods of time by the Proxy and/or Gateway servers. Browser caching helps users quickly navigate pages they have recently visited. 

This caching feature is free to take advantage of and is often overlooked by most hosting companies and many developers.

### Data Caching

Data caching is a very important tool when you have database driven applications or CMS solutions, and this is my favorite type of caching. 

It’s best used for frequent calls to data that does not change rapidly. Data caching will help your website or application load faster giving your users a better experience. 

 It does this by avoiding extra trips to the DB to retrieve data sets that it knows has not changed. It stores the data in local memory on the server which is the fastest way to retrieve information on a web server. 

 The database is the bottle neck for almost all web application, so the fewer DB calls the better. Most DB solutions will also make an attempt to cache frequently used queries in order to reduce turnaround time. For example, MS SQL uses Execution Plans for Store Procedures and Queries to speed up the process time.

### Application/Output Caching

Most CMS have built in cache mechanisms; however, many users don’t understand them and simply ignore them. It’s best to understand what data cache options you have and to implement them whenever possible. 

Application/Output caching can drastically reduce your website load time and reduce server overhead. 

Different than Data Caching, which stores raw data sets, Application/Output Caching often utilizes server level caching techniques that cache raw HTML. 

It can be per page of data, parts of a page (headers/footers) or module data, but it is usually HTML markup. 

 ### Distributed Caching

Distributed Caching is for the big dogs. Most high volume systems like Google, YouTube, Amazon and many others use this technique. This approach allows the web servers to pull and store from distributed server’s memory.

Once implemented, it allow the web server to simply serve pages and not have to worry about running out of memory. This allows the distributed cache to be made up of a cluster of cheaper machines only serving up memory. 

Once the cluster is setup, you can add new machine of memory at any time without disrupting your users. Ever notice how these large companies like Google can return results so quickly when they have hundreds of thousands of simultaneous users? They use Clustered Distributed Caching along with other techniques to infinitely store the data in memory because memory retrieval is faster than file or DB retrieval.


### References
* For more detailed Reseach please visit [Facebook Research or click me](https://research.facebook.com/blog/2016/04/the-evolution-of-advanced-caching-in-the-facebook-cdn/)

* [ MIT article on memory/ Distributed Caching ](https://timilearning.com/posts/mit-6.824/lecture-16-memcache-at-facebook/#:~:text=Facebook%20uses%20memcached%20to%20reduce,as%20a%20look%2Daside%20cache )

* [Instagram Application Caching system ](https://instagram-engineering.com/making-instagram-com-faster-part-3-cache-first-6f3f130b9669?gi=28587970898b)

* [ Tutorial Discussion ]( https://www.tutorialspoint.com/asp.net/asp.net_data_caching.htm )

* [Article on web-caching](https://www.geeksforgeeks.org/web-caching-and-conditional-get-statements/)