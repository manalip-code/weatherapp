


import requests

# Your OpenWeatherMap API key
API_KEY = "95c6749f036c9d73df72446f4d809b32"


def get_weather(city):

    # API URL
    url = f"https://api.openweathermap.org/data/2.5/weather?q={city}&appid={API_KEY}&units=metric"

    try:
        response = requests.get(url, timeout=5)
        data = response.json()

        # Handle invalid city name
        if response.status_code != 200:
            print("\n❌ Error:", data.get("message", "City not found"))
            return

        # Extract weather details
        temperature = data["main"]["temp"]
        humidity = data["main"]["humidity"]
        weather_condition = data["weather"][0]["description"]
        wind_speed = data["wind"]["speed"]

        # Display weather details
        print("\n🌤 Weather Report")
        print("-------------------------")
        print(f"City: {city.title()}")
        print(f"Temperature: {temperature}°C")
        print(f"Humidity: {humidity}%")
        print(f"Condition: {weather_condition.title()}")
        print(f"Wind Speed: {wind_speed} m/s")

    except requests.exceptions.RequestException:
        print("\n Error: Unable to connect to weather service.")


def main():
    city = input("Enter city name: ")
    get_weather(city)


if __name__ == "__main__":
    main()
