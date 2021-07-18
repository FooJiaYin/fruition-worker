# fruition-worker

This project is based on https://github.com/stephenou/fruitionsite

Since notion update the domain of public page, some modification on worker.js is needed:

Add the following code before `else if ((url.pathname.startsWith('/api'))) {`
```
else if ((url.pathname.startsWith('/api/v3/getPublicPageData'))) {
      // Forward API
      response = await fetch(url.toString(), {
        body: request.body,
        headers: {
          'content-type': 'application/json;charset=UTF-8',
          'user-agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/80.0.3987.163 Safari/537.36'
        },
        method: 'POST',
      });
      response = new Response(response.body, response);
      response.headers.set('Access-Control-Allow-Origin', '*');
      response.body.delete('requireInterstitial');
      return response;
    }
```

Please refer to https://github.com/stephenou/fruitionsite/issues/97
