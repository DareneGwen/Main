<!DOCTYPE html>\
<html>
<head>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title> Easy Weather</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>

<div class="card">
    <div class="search">
        <input type="text" placeholder="enter city name" spellcheck="false">
        <button><img src="images/searchhhh.png"></button>
    </div>
    <div class="error">
        <p>invalid city name</p>
    </div>
    <div class="weather">
        <img src="images/rainn.png" class="weather-icon">
        <h1 class="temp">22°c</h1>
        <h2 class="city">Pasig City</h2>
        <div class="details">
            <div class="col">
                <img src="images/humidityy.png">
                <div>
                    <p class="humidity">50%</p>
                    <p>humidity</p>
                </div>
            </div>
            <div class="col">
                <img src="images/wind.png">
                <div>
                    <p class="wind">15 km/h</p>
                    <p>wind Speed</p>
                </div>
            </div>
        </div>
    </div>
</div>

<script>

const apiKey = "eaae3127d0f7bca11dfe28ad8364fac0";
const apiUrl = "https://api.openweathermap.org/data/2.5/weather?units=metric&q=";

const searchBox = document.querySelector(".search input");
const searchBtn = document.querySelector(".search button");
const weatherIcon = document.querySelector(".weather-icon");

async function checkWeather(city){
    const response = await fetch(apiUrl + city + `&appid=${apiKey}`);

    if(response.status == 404){
    document.querySelector(".error").style. display = "block";
    document.querySelector(".weather").style. display = "none";
    }else{
        var data = await response.json();

    document.querySelector(".city").innerHTML = data.name;
    document.querySelector(".temp").innerHTML =  Math.round(data.main.temp ) + "°c";
    document.querySelector(".humidity").innerHTML = data.main.humidity  + "%";
    document.querySelector(".wind").innerHTML = data.wind.speed + " km/h";

if(data.weather[0].main == "Clouds"){
     weatherIcon.src = "images/clouds.png";
}
else if(data.weather[0].main == "Clear"){
    weatherIcon.src = "images/clearr.png";
}
else if(data.weather[0].main == "Rain"){
    weatherIcon.src = "images/rainn.png";
}
else if(data.weather[0].main == "Drizzle"){
    weatherIcon.src = "images/drizle.png";
}
else if(data.weather[0].main == "Mist"){
    weatherIcon.src = "images/mist.png";  
}
else if(data.weather[0].main == "Snow"){
    weatherIcon.src = "images/snow.png";  
}

document.querySelector(".weather").style.display = "block";
document.querySelector(".error").style. display = "none";
    }

    

}


searchBtn.addEventListener("click", ()=>{
    checkWeather(searchBox.value);
})


</script>


</body>
</html>
 
