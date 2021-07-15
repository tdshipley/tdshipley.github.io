---
title: 'Making a GET Request in C# using HttpClient'
date: 2016-01-26T09:33:08+00:00
author: Thomas
layout: single
categories:
  - 'C#'
  - WebAPI
---
With my new job at [New Orbit](https://www.neworbit.co.uk/) I am moving towards full stack web development in [ASP.NET](http://www.asp.net/) and [AngularJS](https://angularjs.org/). The first issue I encountered was how to make a GET request to an external API.

## WebClient vs HttpWebRequest vs HttpClient. Which one?!

It doesn't help that are multiple options. Such as the WebClient, HttpWebRequest and HttpClient classes which all can be used to make a GET request - so which one to choose? _Diogo Nunes_ has a nice [discussion](http://www.diogonunes.com/blog/webclient-vs-httpclient-vs-httpwebrequest/) of the differences. After speaking with one of the Principle developers here it seemed HttpClient was the best option. Compared to WebClient it is closer to the HTTP specification and is less verbose than HttpWebRequest. Although it does need .NET 4.5 which may be an issue on older projects.

## An Example

Below is an example of how to use HttpClient to make a GET request to your target API. In this instance, I was looking to get my user profile information from GitHub for as part of a wider experiment with AngularJS. Although in practice you might be better off using the [Octokit](https://github.com/octokit/octokit.net) library for interactions with the GitHub API.

Most of the code is straightforward enough. The only subtlety is adding a _User-Agent_ header which is required by the GitHub API. It is added at line 21 which creates the User-Agent in the JSON header of the request.

```csharp
namespace API.Controllers
{
    public class GithubController : ApiController
    {
        private const string _address = "https://api.github.com/users/tdshipley";
        private const string _userAgent = "TestApp";

        // GET api/<controller>
        public async Task<string> Get()
        {
            var result = await GetAsync(_address);

            return result.ToString();
        }

        private async Task<JObject> GetAsync(string uri)
        {
            HttpClient client = new HttpClient();

            client.DefaultRequestHeaders.Add("Authorization", "token ADD YOUR OAUTH TOKEN");
            client.DefaultRequestHeaders.Add("User-Agent", _userAgent);
            var content = await client.GetStringAsync(uri);

            return JObject.Parse(content);
        }
    }
}
```