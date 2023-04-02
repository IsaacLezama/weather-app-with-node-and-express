# Weather App with NodeJS and Express

## Hello! 👋

This is a project I made with nodejs and express

So I could practice how API's work

In this project I required express, body parser and https to work with routes

The API I consumed is [open weather map](https://openweathermap.org)

### How this work

I make a get request to my server to get the index.html file

```js
app.get("/", function(req, res) {

    res.sendFile(__dirname + "/index.html");
})
```

Where I get a form to receives the input of a city name

Then I make a post request with some parameters to the API

```js
const url = "https://api.openweathermap.org/data/2.5/weather?q=" + query + "&appid=" + appId + "&units=" + unit;
```

and that's where I recieve the response from the server

```js
https.get(url, function(response) {
        response.on("data", function(data) {
            const weatherData = JSON.parse(data);
            const temp = weatherData.main.temp;
            const weatherDescription = weatherData.weather[0].description;
            const icon = weatherData.weather[0].icon;
            const imageURL = "http://openweathermap.org/img/wn/" + icon + "@2x.png";
            res.write("<p>The weather is currently " + weatherDescription + "</p>");
            res.write("<h1>The temperature in " + query + " is " + temp + " degress Celcuis</h1>");
            res.write("<img src=" + imageURL + ">");
            res.send();
        })
    })
```

and I get the weather description, temperature (in celcius) and an image with an icon