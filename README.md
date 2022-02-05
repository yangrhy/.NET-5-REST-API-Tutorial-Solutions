# .NET-5-REST-API-Tutorial-Solutions

Hopefully this will help others following this tutorial. My comments on youtube were being auto deleted, so resorting to this for now.

### Possible fix for the 404 error after running the kubernetes pods: 

I found that port 80 was being used by SYSTEM (PID 4). After some googling, I found this on stack overflow:

https://stackoverflow.com/questions/1430141/port-80-is-being-used-by-system-pid-4-what-is-that 

In my case, that ended up being the World Wide Web Publishing Service. Yours could be something different. Stopping the service fixed my problem. First time using kubernetes and docker, so not sure how the networking works, but trying other ports in catalog.yaml would not work for me. If anyone can shed some light on that, please do. 

### Fix for "cannot convert from 'int' to 'System.TimeSpan'" in the TimeCreatedItemAsync_WithItemToCreate_ReturnsCreatedItem() assertion test: 

Just passing the integer (1000) no longer works. This is because the **BeCloseTo()** method has been deprecated in the current version of **FluentAssertions** (ver. 6.4.0 at this particular time) to receive a **TimeSpan** rather than an **integer**. You should pass **TimeSpan.FromMilliseconds(1000)** instead. 
Or be sure to use the same version Julio is using (ver. 5.10.3). 

The assertion should look like this for version 6.4.0:

**createdItem.CreatedDate.Should().BeCloseTo(DateTimeOffset.UtcNow, TimeSpan.FromMilliseconds(1000))**; 


*Good luck and happy coding all!*
