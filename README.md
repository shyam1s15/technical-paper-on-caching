
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

As we can see Clairvoyant is fastest but due to implementation issues, again facebook team has to find another solution which can support their heavy traffic as well as hardware.

Again to overcome this problem, they have switched to another algorithm called **BlockCache** which applies the Segmented LRU logic to large fixed-size blocks of items.

In a nutshell, BlockCache restricts its writes to fixed-sized blocks that are aligned in the SSD’s logical address space. These logical blocks were configured to be 64MiB and contain hundreds of photos and video blobs with varying sizes.

BlockCache is more emphasize on High hit rate & lower write amplification so does not decreases the throughput and the lifespan of the SSD.

For more detailed Reseach please visit [Facebook Research or click me](https://research.facebook.com/blog/2016/04/the-evolution-of-advanced-caching-in-the-facebook-cdn/)