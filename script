import requests
import datetime

# clé API OpenWeather
API_KEY = "27a2bc2af76eda261af74ece43e5c2a0" 

# Coordonnées géographiques des villes
CITIES = {
    "Dakar": {"lat": 14.7167, "lon": -17.4677},
    "Thiès": {"lat": 14.7894, "lon": -16.926},
}

# URL de base pour l'API OpenWeather
BASE_URL = "https://api.openweathermap.org/data/2.5/weather"

def get_weather_data(city_name, lat, lon, api_key):
    """
    Récupère les données météo pour une ville donnée.
    """
    try:
        # Construire la requête
        params = {
            "lat": lat,
            "lon": lon,
            "appid": api_key,
            "units": "metric",  # Pour les températures en Celsius
            "lang": "fr"        # Langue des descriptions météo
        }
        
        response = requests.get(BASE_URL, params=params)
        response.raise_for_status()  # Vérifie les erreurs HTTP
        
        # Analyse des données
        data = response.json()
        
        # Extrait les informations clés
        weather_info = {
            "ville": city_name,
            "température": data["main"]["temp"],
            "pression": data["main"]["pressure"],
            "humidité": data["main"]["humidity"],
            "description": data["weather"][0]["description"],
            "timestamp": datetime.datetime.now().isoformat()
        }
        
        return weather_info
    
    except requests.exceptions.RequestException as e:
        print(f"Erreur lors de la récupération des données pour {city_name}: {e}")
        return None

def main():
    """
    Fonction principale pour récupérer les données météo des villes.
    """
    all_weather_data = []
    
    for city, coords in CITIES.items():
        print(f"Récupération des données pour {city}...")
        weather_data = get_weather_data(city, coords["lat"], coords["lon"], API_KEY)
        if weather_data:
            all_weather_data.append(weather_data)
    
    # Affiche les données récupérées
    for weather in all_weather_data:
        print(weather)

if __name__ == "__main__":
    main()
