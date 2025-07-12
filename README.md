# Fusion-# ==============================================================================
# Paramètres Généraux du Bot
# ==============================================================================

# Token de votre bot Telegram
BOT_TOKEN = "7902342551:AAG6r1QA2GTMZcmcsWHi36Ivd_PVeMXULOs"

# ID du groupe privé où le bot enverra des notifications (ex: alertes quotas, archives)
PRIVATE_GROUP_ID = "-1001234567890"

# Message de démarrage affiché dans la console au lancement du bot
STARTUP_MESSAGE = """
===================================================
🚀 Bot IA Démarré ! 🚀
Version: 1.0.0
Prêt à interagir. Tapez vos commandes ou questions.
===================================================
"""

# ==============================================================================
# Configuration des Chemins de Fichiers
# ==============================================================================

# Répertoire de base pour les données du bot (logs, historiques, quotas, etc.)
BASE_DIR = Path(__file__).parent.parent / "bot_data"
BASE_DIR.mkdir(parents=True, exist_ok=True)

# Chemin du fichier de log principal
LOG_FILE = BASE_DIR / "bot_activity.log"

# Chemin du fichier de log pour les erreurs critiques
ERROR_LOG_PATH = BASE_DIR / "bot_errors.log"

# Fichier pour stocker l'état de santé des endpoints API
ENDPOINT_HEALTH_FILE = BASE_DIR / "endpoint_health.json"

# Fichier pour stocker les informations de quota d'utilisation des APIs
QUOTAS_FILE = BASE_DIR / "api_quotas.json"

# Fichier pour stocker le statut de performance et de diversification des IA
IA_STATUS_FILE = BASE_DIR / "ia_status.json"

# Répertoire pour archiver les pages web
ARCHIVES_DIR = "archives"

# Fichier pour stocker l'historique de chat de chaque utilisateur
USER_CHAT_HISTORY_FILE = "chat_history.json"

# Taille maximale des fichiers (ex: images pour OCR) en octets (10 MB)
MAX_FILE_SIZE = 10 * 1024 * 1024
MAX_IMAGE_SIZE = 10 * 1024 * 1024 # Taille maximale pour les images OCR

# ==============================================================================
# Configuration des APIs (Clés et Paramètres)
# ==============================================================================

# Clés API (Hardcodées comme demandé)
GEMINI_API_KEYS = [
    "YOUR_GEMINI_API_KEY_1",
    "YOUR_GEMINI_API_KEY_2"
]
OCR_API_KEYS = [
    "K8900987654321",
    "K1234567890987"
]
DEEPSEEK_API_KEYS = [
    "sk-ef08317d125947b3a1ce5916592bef00",
    "sk-d73750d96142421cb1098c7056dd7f01"
]
SERPER_API_KEY = "YOUR_SERPER_API_KEY_HERE"
WOLFRAMALPHA_APP_IDS = [
    "YOUR_WOLFRAMALPHA_APP_ID_1",
    "YOUR_WOLFRAMALPHA_APP_ID_2"
]
TAVILY_API_KEYS = [
    "YOUR_TAVILY_API_KEY_1",
    "YOUR_TAVILY_API_KEY_2"
]
APIFLASH_ACCESS_KEY = "YOUR_APIFLASH_ACCESS_KEY_HERE"
CRAWLBASE_API_KEY = "YOUR_CRAWLBASE_API_KEY_HERE"
DETECTLANGUAGE_API_KEY = "YOUR_DETECTLANGUAGE_API_KEY_HERE"
GUARDIAN_API_KEY = "YOUR_GUARDIAN_API_KEY_HERE"
IP2LOCATION_API_KEY = "YOUR_IP2LOCATION_API_KEY_HERE"
SHODAN_API_KEY = "YOUR_SHODAN_API_KEY_HERE"
WEATHERAPI_KEY = "YOUR_WEATHERAPI_KEY_HERE"
CLOUDMERSIVE_API_KEY = "YOUR_CLOUDMERSIVE_API_KEY_HERE"
GREYNOISE_API_KEY = "YOUR_GREYNOISE_API_KEY_HERE"
PULSEDIVE_API_KEY = "YOUR_PULSEDIVE_API_KEY_HERE"
STORMGLASS_API_KEY = "YOUR_STORMGLASS_API_KEY_HERE"
LOGINRADIUS_API_KEY = "YOUR_LOGINRADIUS_API_KEY_HERE"
JSONBIN_API_KEY = "YOUR_JSONBIN_API_KEY_HERE"
HUGGINGFACE_API_KEYS = [
    "hf_YOUR_HUGGINGFACE_API_KEY_1",
    "hf_YOUR_HUGGINGFACE_API_KEY_2"
]
TWILIO_ACCOUNT_SID = "ACxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
TWILIO_AUTH_TOKEN = "your_twilio_auth_token"
ABSTRACTAPI_API_KEYS = [
    "YOUR_ABSTRACTAPI_API_KEY_1",
    "YOUR_ABSTRACTAPI_API_KEY_2"
]
GOOGLE_CUSTOM_SEARCH_API_KEYS = [
    "YOUR_GOOGLE_CUSTOM_SEARCH_API_KEY_1",
    "YOUR_GOOGLE_CUSTOM_SEARCH_API_KEY_2"
]
GOOGLE_CUSTOM_SEARCH_CX_LIST = [
    "YOUR_GOOGLE_CUSTOM_SEARCH_CX_1",
    "YOUR_GOOGLE_CUSTOM_SEARCH_CX_2"
]
RANDOMMER_API_KEY = "YOUR_RANDOMMER_API_KEY_HERE"
TOMORROWIO_API_KEY = "YOUR_TOMORROWIO_API_KEY_HERE"
OPENWEATHERMAP_API_KEY = "YOUR_OPENWEATHERMAP_API_KEY_HERE"
MOCKAROO_API_KEY = "YOUR_MOCKAROO_API_KEY_HERE"
OPENPAGERANK_API_KEY = "YOUR_OPENPAGERANK_API_KEY_HERE"
RAPIDAPI_KEY = "YOUR_RAPIDAPI_KEY_HERE"


# Configuration détaillée des endpoints API
API_CONFIG = {
    "GEMINI_API": [
        {
            "endpoint_name": f"Gemini Chat (Key {i+1})",
            "url": "https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash-latest:generateContent",
            "method": "POST",
            "key": key,
            "key_field": "key",
            "key_location": "param",
            "timeout": 60,
            "health_check_params": {"prompt": "test"},
            "health_check_url_suffix": f"?key={key}"
        }
        for i, key in enumerate(GEMINI_API_KEYS)
    ],
    "OCR_API": [
        {
            "endpoint_name": f"OCR.space (Key {i+1})",
            "url": "https://api.ocr.space/parse/image",
            "method": "POST",
            "key": key,
            "key_field": "apikey",
            "key_location": "header",
            "timeout": 30,
            "fixed_headers": {"Content-Type": "application/json"},
            "health_check_json": {"base64Image": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAQAAAC1HAwCAAAAC0lEQVR42mNkYAAAAAYAAjCB0C8AAAAASUVORK5CYII=", "language": "eng"}, # Minimal valid base64 for health check
        }
        for i, key in enumerate(OCR_API_KEYS)
    ],
    "DEEPSEEK": [
        {
            "endpoint_name": f"DeepSeek Chat (Key {i+1})",
            "url": "https://api.deepseek.com/chat/completions",
            "method": "POST",
            "key": key,
            "key_field": "Authorization",
            "key_location": "header",
            "key_prefix": "Bearer ",
            "timeout": 60,
            "fixed_headers": {"Content-Type": "application/json"},
            "health_check_json": {"model": "deepseek-chat", "messages": [{"role": "user", "content": "hi"}]}
        }
        for i, key in enumerate(DEEPSEEK_API_KEYS)
    ],
    "SERPER": [
        {
            "endpoint_name": "Serper Search",
            "url": "https://google.serper.dev/search",
            "method": "POST",
            "key": SERPER_API_KEY,
            "key_field": "X-API-KEY",
            "key_location": "header",
            "timeout": 30,
            "fixed_headers": {"Content-Type": "application/json"},
            "health_check_json": {"q": "test"}
        }
    ],
    "WOLFRAMALPHA": [
        {
            "endpoint_name": f"WolframAlpha Query (App ID {i+1})",
            "url": "http://api.wolframalpha.com/v2/query",
            "method": "GET",
            "key": app_id,
            "key_field": "appid",
            "key_location": "param",
            "timeout": 30,
            "fixed_params": {"output": "json"},
            "health_check_params": {"input": "2+2", "output": "json"}
        }
        for i, app_id in enumerate(WOLFRAMALPHA_APP_IDS)
    ],
    "TAVILY": [
        {
            "endpoint_name": f"Tavily Search (Key {i+1})",
            "url": "https://api.tavily.com/parse",
            "method": "POST",
            "key": key,
            "key_field": "apikey",
            "key_location": "header",
            "timeout": 30,
            "fixed_headers": {"Content-Type": "application/json"},
            "health_check_json": {"query": "test", "max_results": 1}
        }
        for i, key in enumerate(TAVILY_API_KEYS)
    ],
    "APIFLASH": [
        {
            "endpoint_name": "ApiFlash Screenshot",
            "url": "https://api.apiflash.com/v1/urltoimage",
            "method": "GET",
            "key": APIFLASH_ACCESS_KEY,
            "key_field": "access_key",
            "key_location": "param",
            "timeout": 45,
            "health_check_params": {"url": "example.com", "format": "jpeg"}
        }
    ],
    "CRAWLBASE": [
        {
            "endpoint_name": "Crawlbase Scraper",
            "url": "https://api.crawlbase.com/",
            "method": "GET",
            "key": CRAWLBASE_API_KEY,
            "key_field": "token",
            "key_location": "param",
            "timeout": 60,
            "health_check_params": {"url": "http://example.com", "format": "json"}
        },
        {
            "endpoint_name": "Crawlbase JS Scraper",
            "url": "https://api.crawlbase.com/js",
            "method": "GET",
            "key": CRAWLBASE_API_KEY,
            "key_field": "token",
            "key_location": "param",
            "timeout": 90,
            "health_check_params": {"url": "http://example.com", "format": "json"}
        }
    ],
    "DETECTLANGUAGE": [
        {
            "endpoint_name": "DetectLanguage Detect",
            "url": "https://ws.detectlanguage.com/0.2/detect",
            "method": "POST",
            "key": DETECTLANGUAGE_API_KEY,
            "key_field": "X-Detectlanguage-Api-Key",
            "key_location": "header",
            "timeout": 15,
            "fixed_headers": {"Content-Type": "application/json"},
            "health_check_json": {"q": "Hello world"}
        }
    ],
    "GUARDIAN": [
        {
            "endpoint_name": "Guardian Content",
            "url": "https://content.guardianapis.com/search",
            "method": "GET",
            "key": GUARDIAN_API_KEY,
            "key_field": "api-key",
            "key_location": "param",
            "timeout": 20,
            "health_check_params": {"q": "test"}
        }
    ],
    "IP2LOCATION": [
        {
            "endpoint_name": "IP2Location Geolocation",
            "url": "https://api.ip2location.com/v2/",
            "method": "GET",
            "key": IP2LOCATION_API_KEY,
            "key_field": "key",
            "key_location": "param",
            "timeout": 10,
            "health_check_params": {"ip": "8.8.8.8", "addon": "country,city"}
        }
    ],
    "SHODAN": [
        {
            "endpoint_name": "Shodan API Info",
            "url": "https://api.shodan.io/api-info",
            "method": "GET",
            "key": SHODAN_API_KEY,
            "key_field": "key",
            "key_location": "param",
            "timeout": 15,
            "health_check_url_suffix": f"?key={SHODAN_API_KEY}"
        },
        {
            "endpoint_name": "Shodan Host Info",
            "url": "https://api.shodan.io/shodan/host",
            "method": "GET",
            "key": SHODAN_API_KEY,
            "key_field": "key",
            "key_location": "param",
            "timeout": 20,
            "health_check_url_suffix": f"/8.8.8.8?key={SHODAN_API_KEY}"
        }
    ],
    "WEATHERAPI": [
        {
            "endpoint_name": "WeatherAPI Current",
            "url": "http://api.weatherapi.com/v1/current.json",
            "method": "GET",
            "key": WEATHERAPI_KEY,
            "key_field": "key",
            "key_location": "param",
            "timeout": 15,
            "health_check_params": {"q": "London"}
        }
    ],
    "CLOUDMERSIVE": [
        {
            "endpoint_name": "Cloudmersive Validate Domain",
            "url": "https://api.cloudmersive.com/validate/domain/full",
            "method": "POST",
            "key": CLOUDMERSIVE_API_KEY,
            "key_field": "Apikey",
            "key_location": "header",
            "timeout": 20,
            "fixed_headers": {"Content-Type": "application/json"},
            "health_check_json": {"domain": "example.com"}
        }
    ],
    "GREYNOISE": [
        {
            "endpoint_name": "GreyNoise IP Lookup",
            "url": "https://api.greynoise.io/v3/community",
            "method": "GET",
            "key": GREYNOISE_API_KEY,
            "key_field": "key",
            "key_location": "header",
            "timeout": 20,
            "health_check_url_suffix": "/8.8.8.8"
        }
    ],
    "PULSEDIVE": [
        {
            "endpoint_name": "Pulsedive Indicator",
            "url": "https://pulsedive.com/api/v1/indicator.php",
            "method": "GET",
            "key": PULSEDIVE_API_KEY,
            "key_field": "key",
            "key_location": "param",
            "timeout": 25,
            "fixed_params": {"pretty": "1"},
            "health_check_params": {"indicator": "8.8.8.8", "pretty": "1"}
        }
    ],
    "STORMGLASS": [
        {
            "endpoint_name": "StormGlass Weather",
            "url": "https://api.stormglass.io/v2/weather/point",
            "method": "GET",
            "key": STORMGLASS_API_KEY,
            "key_field": "Authorization",
            "key_location": "header",
            "timeout": 30,
            "health_check_params": {"lat": 0, "lng": 0, "params": "airTemperature", "start": 0, "end": 0},
            "health_check_url_suffix": "?lat=0&lng=0&params=airTemperature&start=0&end=0"
        }
    ],
    "LOGINRADIUS": [
        {
            "endpoint_name": "LoginRadius Ping",
            "url": "https://api.loginradius.com/identity/v2/auth/ping",
            "method": "GET",
            "key": LOGINRADIUS_API_KEY,
            "key_field": "apiKey",
            "key_location": "param",
            "timeout": 10,
            "health_check_url_suffix": f"?apiKey={LOGINRADIUS_API_KEY}"
        }
    ],
    "JSONBIN": [
        {
            "endpoint_name": "Bin Create",
            "url": "https://api.jsonbin.io/v3/b",
            "method": "POST",
            "key": JSONBIN_API_KEY,
            "key_field": "X-Master-Key",
            "key_location": "header",
            "timeout": 20,
            "fixed_headers": {"Content-Type": "application/json", "X-Bin-Private": "true"},
            "health_check_json": {"test": "data"}
        },
        {
            "endpoint_name": "Bin Access",
            "url": "https://api.jsonbin.io/v3/b",
            "method": "GET",
            "key": JSONBIN_API_KEY,
            "key_field": "X-Master-Key",
            "key_location": "header",
            "timeout": 20,
            "health_check_url_suffix": "/60c7b9b0f1a9a87d2b7b7b7b"
        }
    ],
    "HUGGINGFACE": [
        {
            "endpoint_name": f"HuggingFace Inference (Key {i+1})",
            "url": "https://api-inference.huggingface.co/models/",
            "method": "POST",
            "key": key,
            "key_field": "Authorization",
            "key_location": "header",
            "key_prefix": "Bearer ",
            "timeout": 60,
            "fixed_headers": {"Content-Type": "application/json"},
            "health_check_url_suffix": "distilbert-base-uncased-finetuned-sst-2-english",
            "health_check_json": {"inputs": "Hello world"}
        }
        for i, key in enumerate(HUGGINGFACE_API_KEYS)
    ],
    "TWILIO": [
        {
            "endpoint_name": "Account Balance",
            "url": f"https://api.twilio.com/2010-04-01/Accounts/{TWILIO_ACCOUNT_SID}/Balance.json",
            "method": "GET",
            "key": (TWILIO_ACCOUNT_SID, TWILIO_AUTH_TOKEN),
            "key_location": "auth_basic",
            "timeout": 20,
            "health_check_url_suffix": ""
        }
    ],
    "ABSTRACTAPI": [
        {
            "endpoint_name": f"Email Validation (Key {i+1})",
            "url": "https://emailvalidation.abstractapi.com/v1/?",
            "method": "GET",
            "key": key,
            "key_field": "api_key",
            "key_location": "param",
            "timeout": 15,
            "health_check_params": {"email": "test@example.com"}
        }
        for i, key in enumerate(ABSTRACTAPI_API_KEYS)
    ] + [
        {
            "endpoint_name": f"Phone Validation (Key {i+1})",
            "url": "https://phonevalidation.abstractapi.com/v1/?",
            "method": "GET",
            "key": key,
            "key_field": "api_key",
            "key_location": "param",
            "timeout": 15,
            "health_check_params": {"phone": "14151234567"}
        }
        for i, key in enumerate(ABSTRACTAPI_API_KEYS)
    ] + [
        {
            "endpoint_name": f"Exchange Rates (Key {i+1})",
            "url": "https://exchangerates.abstractapi.com/v1/live",
            "method": "GET",
            "key": key,
            "key_field": "api_key",
            "key_location": "param",
            "timeout": 15,
            "health_check_params": {"base": "USD"}
        }
        for i, key in enumerate(ABSTRACTAPI_API_KEYS)
    ] + [
        {
            "endpoint_name": f"Holidays (Key {i+1})",
            "url": "https://holidays.abstractapi.com/v1/",
            "method": "GET",
            "key": key,
            "key_field": "api_key",
            "key_location": "param",
            "timeout": 15,
            "health_check_params": {"country": "US", "year": "2023", "month": "1", "day": "1"}
        }
        for i, key in enumerate(ABSTRACTAPI_API_KEYS)
    ],
    "GOOGLE_CUSTOM_SEARCH": [
        {
            "endpoint_name": f"Google Custom Search (API Key {i+1}, CX {j+1})",
            "url": "https://www.googleapis.com/customsearch/v1",
            "method": "GET",
            "key": GOOGLE_CUSTOM_SEARCH_API_KEYS[i],
            "key_field": "key",
            "key_location": "param",
            "timeout": 30,
            "fixed_params": {"cx": GOOGLE_CUSTOM_SEARCH_CX_LIST[j]},
            "health_check_params": {"q": "test", "cx": GOOGLE_CUSTOM_SEARCH_CX_LIST[j]}
        }
        for i in range(len(GOOGLE_CUSTOM_SEARCH_API_KEYS))
        for j in range(len(GOOGLE_CUSTOM_SEARCH_CX_LIST))
    ],
    "RANDOMMER": [
        {
            "endpoint_name": "Randommer Phone Numbers",
            "url": "https://randommer.io/api/Phone/Generate",
            "method": "GET",
            "key": RANDOMMER_API_KEY,
            "key_field": "X-Api-Key",
            "key_location": "header",
            "timeout": 15,
            "fixed_headers": {"Content-Type": "application/json"},
            "health_check_params": {"CountryCode": "US", "Quantity": 1}
        }
    ],
    "TOMORROW.IO": [
        {
            "endpoint_name": "Tomorrow.io Weather",
            "url": "https://api.tomorrow.io/v4/weather/realtime",
            "method": "GET",
            "key": TOMORROWIO_API_KEY,
            "key_field": "apikey",
            "key_location": "param",
            "timeout": 20,
            "health_check_params": {"location": "42.3478,-71.0466", "fields": "temperature"}
        }
    ],
    "OPENWEATHERMAP": [
        {
            "endpoint_name": "OpenWeatherMap Current",
            "url": "https://api.openweathermap.org/data/2.5/weather",
            "method": "GET",
            "key": OPENWEATHERMAP_API_KEY,
            "key_field": "appid",
            "key_location": "param",
            "timeout": 15,
            "health_check_params": {"q": "London"}
        }
    ],
    "MOCKAROO": [
        {
            "endpoint_name": "Mockaroo Generate Data",
            "url": "https://api.mockaroo.com/api/generate.json",
            "method": "GET",
            "key": MOCKAROO_API_KEY,
            "key_field": "key",
            "key_location": "param",
            "timeout": 30,
            "health_check_params": {"count": 1, "fields": '[{"name":"id","type":"Row Number"}]'}
        }
    ],
    "OPENPAGERANK": [
        {
            "endpoint_name": "OpenPageRank Domains",
            "url": "https://openpagerank.com/api/v1.0/getPageRank",
            "method": "GET",
            "key": OPENPAGERANK_API_KEY,
            "key_field": "api_key",
            "key_location": "param",
            "timeout": 20,
            "health_check_params": {"domains[]": ["google.com"]}
        }
    ],
    "RAPIDAPI": [
        {
            "endpoint_name": "RapidAPI Programming Joke",
            "url": "https://programming-jokes-api.p.rapidapi.com/jokes/random",
            "method": "GET",
            "key": RAPIDAPI_KEY,
            "key_field": "X-RapidAPI-Key",
            "key_location": "header",
            "timeout": 20,
            "fixed_headers": {"X-RapidAPI-Host": "programming-jokes-api.p.rapidapi.com"},
            "health_check_url_suffix": ""
        },
        {
            "endpoint_name": "RapidAPI Currency List Quotes",
            "url": "https://currency-exchange.p.rapidapi.com/listquotes",
            "method": "GET",
            "key": RAPIDAPI_KEY,
            "key_field": "X-RapidAPI-Key",
            "key_location": "header",
            "timeout": 20,
            "fixed_headers": {"X-RapidAPI-Host": "currency-exchange.p.rapidapi.com"},
            "health_check_url_suffix": ""
        },
        {
            "endpoint_name": "RapidAPI Random Fact",
            "url": "https://random-facts-api.p.rapidapi.com/api/random",
            "method": "GET",
            "key": RAPIDAPI_KEY,
            "key_field": "X-RapidAPI-Key",
            "key_location": "header",
            "timeout": 20,
            "fixed_headers": {"X-RapidAPI-Host": "random-facts-api.p.rapidapi.com"},
            "health_check_url_suffix": ""
        }
    ]
}

# ==============================================================================
# Configuration des Modèles Gemini
# ==============================================================================

# Paramètres de génération pour l'API Gemini
GEMINI_TEMPERATURE = 0.7
GEMINI_TOP_P = 0.95
GEMINI_TOP_K = 40
GEMINI_MAX_OUTPUT_TOKENS = 8192

# Paramètres de sécurité pour l'API Gemini
GEMINI_SAFETY_SETTINGS = [
    {"category": "HARM_CATEGORY_HARASSMENT", "threshold": "BLOCK_NONE"},
    {"category": "HARM_CATEGORY_HATE_SPEECH", "threshold": "BLOCK_NONE"},
    {"category": "HARM_CATEGORY_SEXUALLY_EXPLICIT", "threshold": "BLOCK_NONE"},
    {"category": "HARM_CATEGORY_DANGEROUS_CONTENT", "threshold": "BLOCK_NONE"},
]

# ==============================================================================
# Configuration des Outils (Tool Calling)
# ==============================================================================

# Définition des outils que le bot peut utiliser via le "Function Calling"
TOOL_CONFIG = {
    "serper_query": {
        "description": "Effectue une recherche web via l'API Serper et retourne les snippets pertinents.",
        "parameters": {
            "type": "object",
            "properties": {
                "query_text": {"type": "string", "description": "La requête de recherche."}
            },
            "required": ["query_text"]
        }
    },
    "wolframalpha_query": {
        "description": "Interroge WolframAlpha pour des calculs, des faits ou des données complexes.",
        "parameters": {
            "type": "object",
            "properties": {
                "input_text": {"type": "string", "description": "La requête à soumettre à WolframAlpha."}
            },
            "required": ["input_text"]
        }
    },
    "tavily_query": {
        "description": "Effectue une recherche web avancée via l'API Tavily, fournissant des extraits et une réponse directe.",
        "parameters": {
            "type": "object",
            "properties": {
                "query_text": {"type": "string", "description": "La requête de recherche."},
                "max_results": {"type": "integer", "description": "Nombre maximum de résultats à retourner.", "default": 3}
            },
            "required": ["query_text"]
        }
    },
    "run_in_sandbox": {
        "description": "Exécute du code Python ou Shell dans un environnement sandbox simulé et retourne la sortie.",
        "parameters": {
            "type": "object",
            "properties": {
                "code": {"type": "string", "description": "Le code à exécuter."},
                "language": {"type": "string", "description": "Le langage du code ('python' ou 'shell').", "enum": ["python", "shell"], "default": "python"}
            },
            "required": ["code"]
        }
    },
    "perform_ocr_api": {
        "description": "Effectue une reconnaissance optique de caractères (OCR) sur une image donnée par URL et retourne le texte extrait.",
        "parameters": {
            "type": "object",
            "properties": {
                "image_url": {"type": "string", "description": "L'URL de l'image à traiter par OCR."}
            },
            "required": ["image_url"]
        }
    },
    "fetch_and_archive_pages": {
        "description": "Récupère le contenu de pages web spécifiées, les archive localement et envoie les liens d'archive au groupe privé.",
        "parameters": {
            "type": "object",
            "properties": {
                "links": {"type": "array", "items": {"type": "string"}, "description": "Liste des URLs des pages à archiver."},
                "user_id": {"type": "string", "description": "L'ID de l'utilisateur demandant l'archivage."}
            },
            "required": ["links", "user_id"]
        }
    },
    "ocr_extract_text": {
        "description": "Extrait le texte d'une image encodée en base64 en utilisant l'OCR. Utile pour les images directement fournies dans le chat.",
        "parameters": {
            "type": "object",
            "properties": {
                "image_base64": {"type": "string", "description": "L'image encodée en base64, incluant le préfixe mimeType (ex: 'data:image/png;base64,...')."}
            },
            "required": ["image_base64"]
        }
    },
    "apiflash_query": {
        "description": "Capture une capture d'écran d'une URL via ApiFlash et retourne l'URL de l'image capturée.",
        "parameters": {
            "type": "object",
            "properties": {
                "url": {"type": "string", "description": "L'URL de la page à capturer."}
            },
            "required": ["url"]
        }
    },
    "crawlbase_query": {
        "description": "Scrape le contenu HTML ou JavaScript d'une URL via Crawlbase. Utilisez 'use_js' pour les pages dynamiques.",
        "parameters": {
            "type": "object",
            "properties": {
                "url": {"type": "string", "description": "L'URL de la page à scraper."},
                "use_js": {"type": "boolean", "description": "Définir à true pour le scraping JavaScript.", "default": False}
            },
            "required": ["url"]
        }
    },
    "detectlanguage_query": {
        "description": "Détecte la langue d'un texte via DetectLanguage API.",
        "parameters": {
            "type": "object",
            "properties": {
                "text": {"type": "string", "description": "Le texte dont la langue doit être détectée."}
            },
            "required": ["text"]
        }
    },
    "guardian_query": {
        "description": "Recherche des articles de presse via l'API The Guardian.",
        "parameters": {
            "type": "object",
            "properties": {
                "query_text": {"type": "string", "description": "La requête de recherche pour les articles."}
            },
            "required": ["query_text"]
        }
    },
    "ip2location_query": {
        "description": "Géolocalise une adresse IP via IP2Location API.",
        "parameters": {
            "type": "object",
            "properties": {
                "ip_address": {"type": "string", "description": "L'adresse IP à géolocaliser."}
            },
            "required": ["ip_address"]
        }
    },
    "shodan_query": {
        "description": "Interroge Shodan pour des informations sur un hôte IP ou des informations sur la clé API.",
        "parameters": {
            "type": "object",
            "properties": {
                "query_text": {"type": "string", "description": "L'adresse IP à rechercher ou vide pour les infos de la clé API."}
            },
            "required": []
        }
    },
    "weatherapi_query": {
        "description": "Récupère les conditions météorologiques actuelles pour une localisation via WeatherAPI.",
        "parameters": {
            "type": "object",
            "properties": {
                "location": {"type": "string", "description": "La ville ou le code postal pour la météo."}
            },
            "required": ["location"]
        }
    },
    "cloudmersive_query": {
        "description": "Vérifie la validité et le type d'un domaine via Cloudmersive API.",
        "parameters": {
            "type": "object",
            "properties": {
                "domain": {"type": "string", "description": "Le nom de domaine à vérifier."}
            },
            "required": ["domain"]
        }
    },
    "greynoise_query": {
        "description": "Analyse une adresse IP pour détecter des activités 'bruit' (malveillantes) via GreyNoise.",
        "parameters": {
            "type": "object",
            "properties": {
                "ip_address": {"type": "string", "description": "L'adresse IP à analyser."}
            },
            "required": ["ip_address"]
        }
    },
    "pulsedive_query": {
        "description": "Analyse un indicateur de menace (IP, domaine, URL) via Pulsedive.",
        "parameters": {
            "type": "object",
            "properties": {
                "indicator": {"type": "string", "description": "L'indicateur de menace à analyser (IP, domaine, URL)."},
                "type": {"type": "string", "description": "Le type d'indicateur ('auto', 'ip', 'domain', 'url').", "default": "auto"}
            },
            "required": ["indicator"]
        }
    },
    "stormglass_query": {
        "description": "Récupère les données météorologiques maritimes pour une coordonnée (latitude, longitude) via StormGlass.",
        "parameters": {
            "type": "object",
            "properties": {
                "lat": {"type": "number", "format": "float", "description": "La latitude."},
                "lng": {"type": "number", "format": "float", "description": "La longitude."},
                "params": {"type": "string", "description": "Paramètres météo à récupérer (ex: 'airTemperature,waveHeight').", "default": "airTemperature,waveHeight"}
            },
            "required": ["lat", "lng"]
        }
    },
    "loginradius_query": {
        "description": "Effectue un simple ping à l'API LoginRadius pour vérifier sa disponibilité.",
        "parameters": {
            "type": "object",
            "properties": {}
        }
    },
    "jsonbin_query": {
        "description": "Crée un nouveau 'bin' JSON ou accède à un bin existant via Jsonbin.io.",
        "parameters": {
            "type": "object",
            "properties": {
                "data": {"type": "object", "description": "Les données JSON à sauvegarder lors de la création d'un bin.", "nullable": True},
                "private": {"type": "boolean", "description": "Indique si le bin doit être privé (true) ou public (false).", "default": True},
                "bin_id": {"type": "string", "description": "L'ID du bin existant à accéder (si pas de 'data').", "nullable": True}
            },
            "required": []
        }
    },
    "huggingface_query": {
        "description": "Effectue une inférence sur un modèle HuggingFace (ex: classification de texte, génération).",
        "parameters": {
            "type": "object",
            "properties": {
                "model_name": {"type": "string", "description": "Le nom du modèle HuggingFace à utiliser (ex: 'distilbert-base-uncased-finetuned-sst-2-english').", "default": "distilbert-base-uncased-finetuned-sst-2-english"},
                "input_text": {"type": "string", "description": "Le texte d'entrée pour l'inférence."}
            },
            "required": ["input_text"]
        }
    },
    "twilio_query": {
        "description": "Récupère le solde du compte Twilio.",
        "parameters": {
            "type": "object",
            "properties": {}
        }
    },
    "abstractapi_query": {
        "description": "Interroge diverses APIs d'AbstractAPI (validation email/téléphone, taux de change, jours fériés).",
        "parameters": {
            "type": "object",
            "properties": {
                "input_value": {"type": "string", "description": "La valeur d'entrée (email, numéro de téléphone, code pays, devise de base)."},
                "api_type": {"type": "string", "description": "Le type d'API AbstractAPI à utiliser ('PHONE_VALIDATION', 'EMAIL_VALIDATION', 'EXCHANGE_RATES', 'HOLIDAYS').", "enum": ["PHONE_VALIDATION", "EMAIL_VALIDATION", "EXCHANGE_RATES", "HOLIDAYS"]}
            },
            "required": ["api_type"]
        }
    },
    "google_custom_search_query": {
        "description": "Effectue une recherche personnalisée Google via l'API Custom Search.",
        "parameters": {
            "type": "object",
            "properties": {
                "query_text": {"type": "string", "description": "La requête de recherche."}
            },
            "required": ["query_text"]
        }
    },
    "randommer_query": {
        "description": "Génère des numéros de téléphone aléatoires via Randommer.io.",
        "parameters": {
            "type": "object",
            "properties": {
                "country_code": {"type": "string", "description": "Le code pays (ex: 'US', 'FR').", "default": "US"},
                "quantity": {"type": "integer", "description": "Le nombre de numéros à générer.", "default": 1}
            },
            "required": []
        }
    },
    "tomorrowio_query": {
        "description": "Récupère les prévisions météorologiques via Tomorrow.io.",
        "parameters": {
            "type": "object",
            "properties": {
                "location": {"type": "string", "description": "La localisation (nom de ville, code postal ou coordonnées)."},
                "fields": {"type": "array", "items": {"type": "string"}, "description": "Liste des champs météo à récupérer (ex: ['temperature', 'humidity']).", "default": ["temperature", "humidity", "windSpeed"]}
            },
            "required": ["location"]
        }
    },
    "openweathermap_query": {
        "description": "Récupère les conditions météorologiques actuelles pour une localisation via OpenWeatherMap.",
        "parameters": {
            "type": "object",
            "properties": {
                "location": {"type": "string", "description": "La ville ou le code postal pour la météo."}
            },
            "required": ["location"]
        }
    },
    "mockaroo_query": {
        "description": "Génère des données de test via Mockaroo.",
        "parameters": {
            "type": "object",
            "properties": {
                "count": {"type": "integer", "description": "Le nombre d'enregistrements à générer.", "default": 1},
                "fields_json": {"type": "string", "description": "Une chaîne JSON décrivant les champs à générer (ex: '[{\"name\":\"name\",\"type\":\"Full Name\"}]').", "nullable": True}
            },
            "required": []
        }
    },
    "openpagerank_query": {
        "description": "Récupère le PageRank de domaines via OpenPageRank.",
        "parameters": {
            "type": "object",
            "properties": {
                "domains": {"type": "array", "items": {"type": "string"}, "description": "Liste des noms de domaine à vérifier."}
            },
            "required": ["domains"]
        }
    },
    "rapidapi_query": {
        "description": "Interroge diverses APIs disponibles via RapidAPI (blagues, taux de change, faits aléatoires).",
        "parameters": {
            "type": "object",
            "properties": {
                "api_name": {"type": "string", "description": "Le nom de l'API RapidAPI à utiliser (ex: 'Programming Joke', 'Currency List Quotes', 'Random Fact').", "enum": ["Programming Joke", "Currency List Quotes", "Random Fact"]},
                "kwargs": {"type": "object", "description": "Arguments supplémentaires spécifiques à l'API RapidAPI appelée.", "additionalProperties": True}
            },
            "required": ["api_name"]
        }
    }
}

# ==============================================================================
# Paramètres du Chat et de la Mémoire
# ==============================================================================

# Longueur maximale de l'historique du chat à conserver en mémoire et sur disque
MAX_CHAT_HISTORY_LENGTH = 20

# ==============================================================================
# Paramètres des Checks de Santé des Endpoints
# ==============================================================================

# Activer ou désactiver les checks de santé périodiques des endpoints API
ENABLE_HEALTH_CHECKS = True

# Intervalle en secondes entre chaque exécution des checks de santé
HEALTH_CHECK_INTERVAL_SECONDS = 2700

import json
import logging
from datetime import datetime, timezone
from pathlib import Path
import re
import asyncio
import os
from typing import Any, Optional, Dict

# Import des constantes du fichier de configuration
from config import LOG_FILE, ERROR_LOG_PATH, BASE_DIR, MAX_FILE_SIZE, API_CONFIG, TOOL_CONFIG

# ==== Configuration du logging ====
# Configure le logger principal pour le bot
logger = logging.getLogger("bot_logger")
logger.setLevel(logging.INFO)

# Crée le répertoire de base si nécessaire
BASE_DIR.mkdir(parents=True, exist_ok=True)

# Gestionnaire pour le fichier de log principal
file_handler = logging.FileHandler(LOG_FILE)
file_handler.setLevel(logging.INFO)
formatter = logging.Formatter('%(asctime)s - %(levelname)s - %(message)s')
file_handler.setFormatter(formatter)
logger.addHandler(file_handler)

# Gestionnaire pour les erreurs critiques (fichier séparé)
error_file_handler = logging.FileHandler(ERROR_LOG_PATH)
error_file_handler.setLevel(logging.ERROR)
error_file_handler.setFormatter(formatter)
logger.addHandler(error_file_handler)

# Gestionnaire pour la console (logs en temps réel)
console_handler = logging.StreamHandler()
console_handler.setLevel(logging.INFO)
console_handler.setFormatter(formatter)
logger.addHandler(console_handler)

# Verrou pour les opérations de fichier asynchrones
_file_lock: Optional[asyncio.Lock] = None

def set_file_lock(lock: asyncio.Lock):
    """Définit l'instance du verrou asyncio pour les opérations de fichier."""
    global _file_lock
    _file_lock = lock

def log_message(message: str, level: str = "info"):
    """
    Enregistre un message dans le fichier de log et la console.
    Args:
        message (str): Le message à enregistrer.
        level (str): Le niveau de log ('debug', 'info', 'warning', 'error', 'critical').
    """
    if level == "debug":
        logger.debug(message)
    elif level == "info":
        logger.info(message)
    elif level == "warning":
        logger.warning(message)
    elif level == "error":
        logger.error(message)
    elif level == "critical":
        logger.critical(message)
    else:
        logger.info(f"Niveau de log inconnu '{level}': {message}")

def get_current_time() -> datetime:
    """Retourne l'heure actuelle en UTC."""
    return datetime.now(timezone.utc)

def format_datetime(dt: datetime) -> str:
    """Formate un objet datetime en chaîne de caractères lisible."""
    return dt.strftime("%Y-%m-%d %H:%M:%S UTC")

async def load_json(file_path: Path, default_value: Any = None) -> Any:
    """
    Charge les données d'un fichier JSON de manière asynchrone.
    Crée le fichier avec une valeur par défaut si inexistant.
    Args:
        file_path (Path): Le chemin du fichier JSON.
        default_value (Any): La valeur à retourner si le fichier n'existe pas ou est vide.
    Returns:
        Any: Le contenu du fichier JSON ou la valeur par défaut.
    """
    if _file_lock is None:
        log_message("Le verrou de fichier n'est pas initialisé dans utils.py. Initialisation par défaut.", level="warning")
        global _file_lock
        _file_lock = asyncio.Lock()

    try:
        if not file_path.exists():
            log_message(f"Fichier non trouvé: {file_path}. Création avec valeur par défaut.", level="info")
            await save_json(file_path, default_value if default_value is not None else {})
            return default_value if default_value is not None else {}
        
        async with _file_lock:
            return await asyncio.to_thread(_load_json_sync, file_path)
    except json.JSONDecodeError:
        log_message(f"Erreur de décodage JSON pour le fichier: {file_path}. Le fichier pourrait être corrompu. Retourne la valeur par défaut.", level="error")
        await save_json(file_path, default_value if default_value is not None else {})
        return default_value if default_value is not None else {}
    except Exception as e:
        log_message(f"Erreur inattendue lors du chargement du JSON {file_path}: {e}", level="error")
        return default_value if default_value is not None else {}

def _load_json_sync(file_path: Path) -> Any:
    """Fonction synchrone pour charger le JSON, appelée par asyncio.to_thread."""
    with open(file_path, 'r', encoding='utf-8') as f:
        return json.load(f)

async def save_json(file_path: Path, data: Any):
    """
    Sauvegarde les données dans un fichier JSON de manière asynchrone.
    Args:
        file_path (Path): Le chemin du fichier JSON.
        data (Any): Les données à sauvegarder.
    """
    if _file_lock is None:
        log_message("Le verrou de fichier n'est pas initialisé dans utils.py. Initialisation par défaut.", level="warning")
        global _file_lock
        _file_lock = asyncio.Lock()

    try:
        file_path.parent.mkdir(parents=True, exist_ok=True)
        
        async with _file_lock:
            await asyncio.to_thread(_save_json_sync, file_path, data)
        log_message(f"Données sauvegardées dans {file_path}", level="debug")
    except Exception as e:
        log_message(f"Erreur lors de la sauvegarde du JSON {file_path}: {e}", level="error")

def _save_json_sync(file_path: Path, data: Any):
    """Fonction synchrone pour sauvegarder le JSON, appelée par asyncio.to_thread."""
    with open(file_path, 'w', encoding='utf-8') as f:
        json.dump(data, f, indent=4)

def neutralize_urls(text: str) -> str:
    """
    Remplace les URLs dans le texte par une version neutralisée pour éviter les problèmes de sécurité
    ou les tentatives d'accès non désirées par le modèle.
    """
    url_pattern = re.compile(r'https?://[^\s/$.?#].[^\s]*', re.IGNORECASE)
    
    neutralized_text = url_pattern.sub("[LIEN_NEUTRALISÉ]", text)
    return neutralized_text

def find_tool_by_name(tool_name: str) -> Optional[Dict[str, Any]]:
    """
    Recherche un outil dans TOOL_CONFIG par son nom.
    Args:
        tool_name (str): Le nom de l'outil à rechercher.
    Returns:
        Optional[Dict[str, Any]]: Le dictionnaire de configuration de l'outil si trouvé, sinon None.
    """
    return TOOL_CONFIG.get(tool_name)

async def append_to_file(file_path: Path, content: str):
    """
    Ajoute du contenu à un fichier, en créant le fichier/répertoire si nécessaire.
    Gère la rotation du fichier si sa taille dépasse MAX_FILE_SIZE.
    """
    if _file_lock is None:
        log_message("Le verrou de fichier n'est pas initialisé dans utils.py. Initialisation par défaut.", level="warning")
        global _file_lock
        _file_lock = asyncio.Lock()

    file_path.parent.mkdir(parents=True, exist_ok=True)

    if file_path.exists() and file_path.stat().st_size + len(content.encode('utf-8')) > MAX_FILE_SIZE:
        rotate_file(file_path)

    async with _file_lock:
        await asyncio.to_thread(_append_to_file_sync, file_path, content)

def _append_to_file_sync(file_path: Path, content: str):
    """Fonction synchrone pour ajouter du contenu à un fichier."""
    with open(file_path, 'a', encoding='utf-8') as f:
        f.write(content + "\n")

def rotate_file(file_path: Path):
    """
    Effectue une rotation de fichier simple: renomme le fichier actuel avec un horodatage.
    """
    timestamp = datetime.now(timezone.utc).strftime("%Y%m%d_%H%M%S")
    new_path = file_path.parent / f"{file_path.stem}_{timestamp}{file_path.suffix}"
    try:
        os.rename(file_path, new_path)
        log_message(f"Fichier {file_path.name} renommé en {new_path.name} pour rotation.", level="info")
    except OSError as e:
        log_message(f"Erreur lors de la rotation du fichier {file_path.name}: {e}", level="error")

import time
import httpx
import json
import base64
import asyncio
import re 
import traceback
from typing import Dict, Any, Optional, Union, List, Tuple

# Import des constantes et fonctions utilitaires
from config import API_CONFIG, ENDPOINT_HEALTH_FILE, MAX_IMAGE_SIZE, GEMINI_TEMPERATURE, GEMINI_TOP_P, GEMINI_TOP_K, GEMINI_MAX_OUTPUT_TOKENS, GEMINI_SAFETY_SETTINGS
from utils import load_json, save_json, get_current_time, format_datetime, log_message, neutralize_urls

class EndpointHealthManager:
    """
    Gère la santé des endpoints API et sélectionne le meilleur endpoint disponible
    en fonction de critères comme la latence, le taux de succès et le nombre d'erreurs.
    C'est un singleton pour s'assurer qu'il n'y a qu'une seule instance de gestionnaire de santé.
    """
    _instance = None
    _initialized = False

    def __new__(cls, *args, **kwargs):
        """Implémente le patron de conception Singleton."""
        if cls._instance is None:
            cls._instance = super(cls, cls).__new__(cls)
        return cls._instance

    def __init__(self):
        """Initialise le gestionnaire."""
        if self._initialized:
            return
        self.health_status = {}

    async def init_manager(self):
        """
        Initialise le gestionnaire de santé de manière asynchrone.
        Charge l'état de santé persistant et s'assure que tous les endpoints sont suivis.
        """
        if not self._initialized:
            self.health_status = await load_json(ENDPOINT_HEALTH_FILE, {})
            self._initialize_health_status()
            self._initialized = True
            log_message("Gestionnaire de santé des endpoints initialisé.")

    def _initialize_health_status(self):
        """
        Initialise ou met à jour le statut de santé pour tous les endpoints configurés dans `API_CONFIG`.
        Ajoute les nouveaux endpoints et s'assure que toutes les clés nécessaires sont présentes.
        """
        updated = False
        for service_name, endpoints_config in API_CONFIG.items():
            if service_name not in self.health_status:
                self.health_status[service_name] = {}
                updated = True
            for endpoint_config in endpoints_config:
                endpoint_key = f"{endpoint_config['endpoint_name']}-{str(endpoint_config['key'])}"
                if endpoint_key not in self.health_status[service_name]:
                    self.health_status[service_name][endpoint_key] = {
                        "latency": 0.0,
                        "success_rate": 1.0,
                        "last_checked": None,
                        "error_count": 0,
                        "total_checks": 0,
                        "is_healthy": True
                    }
                    updated = True
        if updated:
            asyncio.create_task(save_json(ENDPOINT_HEALTH_FILE, self.health_status))
            log_message("Statut de santé des endpoints initialisé/mis à jour.")

    async def run_health_check_for_service(self, service_name: str):
        """
        Exécute des checks de santé pour tous les endpoints d'un service donné.
        Tente d'appeler l'endpoint avec des paramètres de santé prédéfinis.
        """
        endpoints_config = API_CONFIG.get(service_name)
        if not endpoints_config:
            log_message(f"Aucune configuration d'endpoint trouvée pour le service: {service_name}", level="warning")
            return

        log_message(f"Lancement du health check pour le service: {service_name}")
        for endpoint_config in endpoints_config:
            endpoint_key = f"{endpoint_config['endpoint_name']}-{str(endpoint_config['key'])}"
            start_time = time.monotonic()
            success = False
            try:
                request_method = endpoint_config.get("method", "GET")
                url = endpoint_config["url"]
                
                params = endpoint_config.get("health_check_params", endpoint_config.get("fixed_params", {})).copy()
                json_data = endpoint_config.get("health_check_json", endpoint_config.get("fixed_json", {})).copy()
                headers = endpoint_config.get("fixed_headers", {}).copy()
                auth = None
                
                check_timeout = endpoint_config.get("timeout", 5)

                if "health_check_url_suffix" in endpoint_config:
                    url += endpoint_config["health_check_url_suffix"]

                key_field = endpoint_config.get("key_field")
                key_location = endpoint_config.get("key_location")
                key_prefix = endpoint_config.get("key_prefix", "")
                api_key = endpoint_config["key"]

                if key_field and key_location:
                    if key_location == "param":
                        params[key_field] = api_key
                    elif key_location == "header":
                        headers[key_field] = f"{key_prefix}{api_key}"
                    elif key_location == "auth_basic":
                        if isinstance(api_key, tuple) and len(api_key) == 2:
                            auth = httpx.BasicAuth(api_key[0], api_key[1])
                        else:
                            log_message(f"Clé API pour auth_basic non valide pour {service_name}:{endpoint_key}", level="error")
                            success = False
                            continue

                async with httpx.AsyncClient(timeout=check_timeout) as client:
                    response = await client.request(request_method, url, params=params, headers=headers, json=json_data, auth=auth)
                    response.raise_for_status()
                    success = True
            except httpx.HTTPStatusError as e:
                log_level = "warning"
                if 400 <= e.response.status_code < 500 and e.response.status_code != 429:
                    log_level = "debug" 
                log_message(f"Health check pour {endpoint_key} ({service_name}) a échoué (HTTP {e.response.status_code}): {e.response.text}", level=log_level)
                success = False
            except httpx.RequestError as e:
                log_message(f"Health check pour {endpoint_key} ({service_name}) a échoué (Réseau): {e}", level="warning")
                success = False
            except Exception as e:
                log_message(f"Health check pour {endpoint_key} ({service_name}) a échoué (Inattendu): {e}", level="error")
                success = False
            finally:
                latency = time.monotonic() - start_time
                self.update_endpoint_health(service_name, endpoint_key, success, latency)
        log_message(f"Health check terminé pour le service: {service_name}")

    def update_endpoint_health(self, service_name: str, endpoint_key: str, success: bool, latency: float):
        """
        Met à jour le statut de santé d'un endpoint spécifique.
        Utilise une moyenne glissante pour le taux de succès et la latence.
        """
        if service_name not in self.health_status:
            self.health_status[service_name] = {}
        if endpoint_key not in self.health_status[service_name]:
            self.health_status[service_name][endpoint_key] = {
                "latency": 0.0,
                "success_rate": 1.0,
                "last_checked": None,
                "error_count": 0,
                "total_checks": 0,
                "is_healthy": True
            }

        status = self.health_status[service_name][endpoint_key]
        status["total_checks"] += 1
        status["last_checked"] = format_datetime(get_current_time())

        alpha = 0.1
        if success:
            status["error_count"] = max(0, status["error_count"] - 1)
            status["success_rate"] = status["success_rate"] * (1 - alpha) + 1.0 * alpha
            status["latency"] = status["latency"] * (1 - alpha) + latency * alpha
        else:
            status["error_count"] += 1
            status["success_rate"] = status["success_rate"] * (1 - alpha) + 0.0 * alpha
            status["latency"] = status["latency"] * (1 - alpha) + 10.0 * alpha 

        if status["error_count"] >= 3 or status["success_rate"] < 0.5:
            status["is_healthy"] = False
        else:
            status["is_healthy"] = True
        
        asyncio.create_task(save_json(ENDPOINT_HEALTH_FILE, self.health_status))
        log_message(f"Santé de {service_name}:{endpoint_key} mise à jour: Succès: {success}, Latence: {latency:.2f}s, Taux Succès: {status['success_rate']:.2f}, Sain: {status['is_healthy']}", level="debug" if not status["is_healthy"] else "info")

    def get_best_endpoint(self, service_name: str) -> Optional[Dict]:
        """
        Sélectionne le meilleur endpoint pour un service donné basé sur son statut de santé.
        Priorise les endpoints sains, puis les moins mauvais en cas d'absence d'endpoints sains.
        """
        service_health = self.health_status.get(service_name)
        if not service_health:
            log_message(f"Aucune donnée de santé pour le service {service_name}. Retourne None.", level="warning")
            return None

        best_endpoint_key = None
        best_score = -float('inf')

        healthy_endpoints = [
            (key, status) for key, status in service_health.items() if status["is_healthy"]
        ]

        if not healthy_endpoints:
            log_message(f"Aucun endpoint sain pour le service {service_name}. Tentative de sélection d'un endpoint non sain.", level="warning")
            all_endpoints = service_health.items()
            if not all_endpoints: 
                return None
            
            sorted_endpoints = sorted(all_endpoints, key=lambda item: (item[1]["error_count"], item[1]["latency"]))
            best_endpoint_key = sorted_endpoints[0][0]
            log_message(f"Fallback: Endpoint {best_endpoint_key} sélectionné pour {service_name} (non sain).", level="warning")
        else:
            for endpoint_key, status in healthy_endpoints:
                score = (status["success_rate"] * 100) - (status["latency"] * 10) - (status["error_count"] * 5)
                if score > best_score:
                    best_score = score
                    best_endpoint_key = endpoint_key
            log_message(f"Meilleur endpoint sélectionné pour {service_name}: {best_endpoint_key} (Score: {best_score:.2f})")

        if best_endpoint_key:
            for endpoint_config in API_CONFIG.get(service_name, []):
                current_endpoint_key = f"{endpoint_config['endpoint_name']}-{str(endpoint_config['key'])}"
                if current_endpoint_key == best_endpoint_key:
                    return endpoint_config
        return None

# Instancier le gestionnaire de santé des endpoints (sera initialisé dans main.py)
endpoint_health_manager = EndpointHealthManager()

def set_endpoint_health_manager_global(manager: EndpointHealthManager):
    """
    Permet d'injecter l'instance du gestionnaire de santé des endpoints.
    Ceci est utilisé pour s'assurer que tous les clients API utilisent la même instance.
    """
    global endpoint_health_manager
    endpoint_health_manager = manager

class APIClient:
    """
    Classe de base pour tous les clients API.
    Elle gère la sélection dynamique d'endpoints, les réessais en cas d'échec
    et l'intégration avec le gestionnaire de santé des endpoints.
    """
    def __init__(self, name: str, endpoint_health_manager: EndpointHealthManager):
        self.name = name
        self.endpoints_config = API_CONFIG.get(name, [])
        self.endpoint_health_manager = endpoint_health_manager
        if not self.endpoints_config:
            log_message(f"Client API {self.name} initialisé sans configuration d'endpoint.", level="error")

    async def _make_request(self, params: Optional[Dict] = None, headers: Optional[Dict] = None, 
                            json_data: Optional[Dict] = None, timeout: Optional[int] = None, 
                            max_retries: int = 3, initial_delay: float = 1.0, 
                            url: Optional[str] = None, method: Optional[str] = None, 
                            key_field: Optional[str] = None, key_location: Optional[str] = None, 
                            api_key: Optional[Union[str, Tuple[str, str]]] = None, 
                            fixed_params: Optional[Dict] = None, fixed_headers: Optional[Dict] = None, 
                            fixed_json: Optional[Dict] = None) -> Optional[Union[Dict, str, bytes]]:
        """
        Méthode interne pour effectuer les requêtes HTTP en utilisant le meilleur endpoint avec réessais.
        """
        
        selected_endpoint_config = None
        endpoint_key_for_health = "Dynamic"

        if url and method:
            selected_endpoint_config = {
                "url": url,
                "method": method,
                "key_field": key_field,
                "key_location": key_location,
                "key": api_key,
                "fixed_params": fixed_params if fixed_params is not None else {},
                "fixed_headers": fixed_headers if fixed_headers is not None else {},
                "fixed_json": fixed_json if fixed_json is not None else {},
                "endpoint_name": "Dynamic",
                "timeout": timeout if timeout is not None else 30
            }
            if api_key:
                endpoint_key_for_health = f"Dynamic-{str(api_key)}"
            log_message(f"Requête dynamique pour {self.name} vers {url}")
        else:
            selected_endpoint_config = self.endpoint_health_manager.get_best_endpoint(self.name)
            if not selected_endpoint_config:
                log_message(f"Aucun endpoint sain ou disponible pour {self.name}.", level="error")
                return {"error": True, "message": f"Aucun endpoint sain ou disponible pour {self.name}."}
            endpoint_key_for_health = f"{selected_endpoint_config['endpoint_name']}-{str(selected_endpoint_config['key'])}"
            log_message(f"Endpoint sélectionné pour {self.name}: {selected_endpoint_config['endpoint_name']}")
            timeout = timeout if timeout is not None else selected_endpoint_config.get("timeout", 30)

        url_to_use = selected_endpoint_config["url"]
        method_to_use = selected_endpoint_config["method"]

        request_params = selected_endpoint_config.get("fixed_params", {}).copy()
        request_headers = selected_endpoint_config.get("fixed_headers", {}).copy()
        request_json_data = selected_endpoint_config.get("fixed_json", {}).copy()
        auth = None

        if params:
            request_params.update(params)
        if headers:
            request_headers.update(headers)
        if json_data:
            request_json_data.update(json_data)

        key_field_to_use = selected_endpoint_config.get("key_field")
        key_location_to_use = selected_endpoint_config.get("key_location")
        key_prefix = selected_endpoint_config.get("key_prefix", "")
        api_key_to_use = selected_endpoint_config["key"]

        if key_field_to_use and key_location_to_use:
            if key_location_to_use == "param":
                request_params[key_field_to_use] = api_key_to_use
            elif key_location_to_use == "header":
                request_headers[key_field_to_use] = f"{key_prefix}{api_key_to_use}"
            elif key_location_to_use == "auth_basic":
                if isinstance(api_key_to_use, tuple) and len(api_key_to_use) == 2:
                    auth = httpx.BasicAuth(api_key_to_use[0], api_key_to_use[1])
                else:
                    log_message(f"Clé API pour auth_basic non valide pour {self.name}:{endpoint_key_for_health}", level="error")
                    self.endpoint_health_manager.update_endpoint_health(self.name, endpoint_key_for_health, False, 0.0)
                    return {"error": True, "message": "Configuration d'authentification basique invalide."}

        current_delay = initial_delay
        for attempt in range(max_retries):
            start_time = time.monotonic()
            success = False
            try:
                async with httpx.AsyncClient(timeout=timeout) as client:
                    response = await client.request(method_to_use, url_to_use, params=request_params, headers=request_headers, json=request_json_data, auth=auth)
                    response.raise_for_status()
                    success = True
                    
                    content_type = response.headers.get("Content-Type", "").lower()
                    if "application/json" in content_type:
                        try:
                            return response.json()
                        except json.JSONDecodeError:
                            log_message(f"API {self.name} réponse non JSON valide (tentative {attempt+1}/{max_retries}): {response.text[:200]}...", level="warning")
                            if attempt < max_retries - 1:
                                await asyncio.sleep(current_delay)
                                current_delay *= 2
                                continue
                            return {"error": True, "message": "Réponse API non JSON valide.", "raw_response": response.text}
                    else:
                        log_message(f"API {self.name} a renvoyé un Content-Type non JSON: {content_type}", level="info")
                        return response.content

            except httpx.HTTPStatusError as e:
                log_message(f"API {self.name} erreur HTTP (tentative {attempt+1}/{max_retries}): {e.response.status_code} - {e.response.text}", level="warning")
                if 400 <= e.response.status_code < 500 and e.response.status_code != 429:
                    log_message(f"API {self.name}: Erreur client {e.response.status_code}, pas de réessai.", level="error")
                    self.endpoint_health_manager.update_endpoint_health(self.name, endpoint_key_for_health, False, e.response.elapsed.total_seconds())
                    return {"error": True, "status_code": e.response.status_code, "message": e.response.text}
                
                if attempt < max_retries - 1:
                    log_message(f"API {self.name}: Réessai dans {current_delay:.2f}s...", level="info")
                    await asyncio.sleep(current_delay)
                    current_delay *= 2
            except httpx.RequestError as e:
                log_message(f"API {self.name} erreur de requête (tentative {attempt+1}/{max_retries}): {e}", level="warning")
                if attempt < max_retries - 1:
                    log_message(f"API {self.name}: Réessai dans {current_delay:.2f}s...", level="info")
                    await asyncio.sleep(current_delay)
                    current_delay *= 2
            except Exception as e:
                log_message(f"API {self.name} erreur inattendue (tentative {attempt+1}/{max_retries}): {e}", level="error")
                self.endpoint_health_manager.update_endpoint_health(self.name, endpoint_key_for_health, False, time.monotonic() - start_time)
                return {"error": True, "message": str(e)}
            finally:
                if not success:
                    latency = time.monotonic() - start_time
                    self.endpoint_health_manager.update_endpoint_health(self.name, endpoint_key_for_health, False, latency)
        
        log_message(f"API {self.name}: Toutes les tentatives ont échoué après {max_retries} réessais.", level="error")
        return {"error": True, "message": f"Échec de la requête après {max_retries} tentatives."}

    async def query(self, *args, **kwargs) -> Any:
        """
        Méthode abstraite pour interroger l'API.
        Doit être implémentée par chaque sous-classe de client API.
        """
        raise NotImplementedError("La méthode query doit être implémentée par les sous-classes.")

# --- Clients API Spécifiques ---

class GeminiAPIClient(APIClient):
    """Client pour l'API Gemini, hérite de APIClient pour la gestion de santé."""
    def __init__(self):
        super().__init__("GEMINI_API", endpoint_health_manager)
        self.model_name = "gemini-1.5-flash-latest"
        self.generation_config = {
            "temperature": GEMINI_TEMPERATURE,
            "top_p": GEMINI_TOP_P,
            "top_k": GEMINI_TOP_K,
            "max_output_tokens": GEMINI_MAX_OUTPUT_TOKENS,
        }
        self.safety_settings = GEMINI_SAFETY_SETTINGS
        log_message(f"GeminiApiClient initialisé avec le modèle par défaut: {self.model_name}")

    async def generate_content(self, prompt: str, chat_history: List[Dict], image_data: Optional[str] = None, model: Optional[str] = None, tools: Optional[List[Dict]] = None) -> Union[Dict, str]:
        """Génère du contenu textuel ou multimodal en utilisant l'API Gemini."""
        model_to_use = model if model else self.model_name
        
        contents = []
        for msg in chat_history:
            role = "user" if msg["role"] == "user" else "model"
            contents.append({"role": role, "parts": msg["parts"]})

        if contents and contents[-1]["role"] == "user":
            contents[-1]["parts"].append({"text": prompt})
        else:
            contents.append({"role": "user", "parts": [{"text": prompt}]})

        if image_data:
            if "," in image_data:
                mime_type_part, base64_data = image_data.split(",", 1)
                mime_type = mime_type_part.split(":", 1)[1].split(";", 1)[0]
            else:
                mime_type = "image/jpeg" 
                base64_data = image_data

            if contents and contents[-1]["role"] == "user":
                contents[-1]["parts"].append({
                    "inlineData": {
                        "mimeType": mime_type,
                        "data": base64_data
                    }
                })
                log_message(f"Image ajoutée au prompt Gemini (mimeType: {mime_type}).")
            else:
                log_message("Impossible d'ajouter l'image au prompt Gemini: le dernier message n'est pas un utilisateur.", level="warning")

        payload = {
            "contents": contents,
            "generationConfig": self.generation_config,
            "safetySettings": self.safety_settings
        }

        if tools:
            payload["tools"] = tools

        log_message(f"Appel à Gemini API pour le modèle {model_to_use}...")
        
        # L'URL de l'endpoint Gemini peut varier en fonction du modèle.
        # On prend l'URL de base du premier endpoint configuré et on y ajoute le modèle.
        base_url_from_config = self.endpoints_config[0]["url"].split(':generateContent')[0]
        dynamic_url = f"{base_url_from_config}:{model_to_use}:generateContent"

        # Les headers et la clé API seront gérés par _make_request via la sélection d'endpoint
        response = await self._make_request(
            url=dynamic_url,
            method="POST",
            json_data=payload,
            timeout=60 # Utilise le timeout de la méthode _make_request
        )

        if response and not response.get("error"):
            return response
        return f"❌ Erreur Gemini: {response.get('message', 'Inconnu')}" if response else "❌ Erreur Gemini: Réponse vide ou erreur interne."

class OCRApiClient(APIClient):
    """Client pour l'API OCR.space, hérite de APIClient pour la gestion de santé."""
    def __init__(self):
        super().__init__("OCR_API", endpoint_health_manager)
        log_message("OCRApiClient initialisé.")

    async def query(self, image_base64: str) -> str:
        """
        Effectue une requête OCR à l'API OCR.space.
        `image_base64` doit être la chaîne base64 de l'image, incluant le préfixe mimeType.
        """
        payload = {
            "base64Image": image_base64,
            "language": "fre",
            "isOverlayRequired": False,
            "OCREngine": 2
        }
        
        # Les headers et la clé API seront gérés par _make_request via la sélection d'endpoint
        log_message("Appel à OCR.space API...")
        response = await self._make_request(
            json_data=payload,
            method="POST",
            timeout=30
        )

        if response and not response.get("error"):
            if response.get("IsErroredOnProcessing"):
                error_message = response.get("ErrorMessage", ["Erreur inconnue lors du traitement OCR."])
                log_message(f"Erreur OCR.space: {error_message}", level="error")
                return f"❌ Erreur OCR: {', '.join(error_message)}"
            
            parsed_text = ""
            if "ParsedResults" in response and response["ParsedResults"]:
                for parsed_result in response["ParsedResults"]:
                    parsed_text += parsed_result.get("ParsedText", "") + "\n"
            
            if parsed_text.strip():
                log_message("OCR.space: Texte extrait avec succès.")
                return parsed_text.strip()
            else:
                log_message("OCR.space: Aucun texte extrait.", level="warning")
                return "Aucun texte n'a pu être extrait de l'image."
        return f"❌ Erreur OCR: {response.get('message', 'Inconnu')}" if response else "❌ Erreur OCR: Réponse vide ou erreur interne."

class DeepSeekClient(APIClient):
    def __init__(self):
        super().__init__("DEEPSEEK", endpoint_health_manager)

    async def query(self, prompt: Union[str, List[Dict]], model: str = "deepseek-chat") -> str:
        """Interroge l'API DeepSeek pour des complétions de chat."""
        if isinstance(prompt, str):
            messages = [{"role": "user", "content": prompt}]
        else:
            messages = prompt

        payload = {"model": model, "messages": messages}
        response = await self._make_request(json_data=payload)
        if response and not response.get("error"):
            content = response.get("choices", [{}])[0].get("message", {}).get("content")
            if content:
                return content
            return "DeepSeek: Pas de contenu de réponse trouvé."
        return f"DeepSeek: Erreur: {response.get('message', 'Inconnu')}" if response else "DeepSeek: Réponse vide ou erreur interne."

class SerperClient(APIClient):
    def __init__(self):
        super().__init__("SERPER", endpoint_health_manager)

    async def query(self, query_text: str) -> str:
        """Effectue une recherche web via l'API Serper."""
        payload = {"q": query_text}
        response = await self._make_request(json_data=payload)
        if response and not response.get("error"):
            organic_results = response.get("organic", [])
            if organic_results:
                snippet = organic_results[0].get("snippet", "Pas de snippet.")
                link = organic_results[0].get("link", "")
                return f"Serper (recherche web):\n{snippet} {neutralize_urls(link)}"
            return "Serper: Aucune information trouvée."
        return f"Serper: Erreur: {response.get('message', 'Inconnu')}" if response else "Serper: Réponse vide ou erreur interne."

class WolframAlphaClient(APIClient):
    def __init__(self):
        super().__init__("WOLFRAMALPHA", endpoint_health_manager)

    async def query(self, input_text: str) -> str:
        """Interroge WolframAlpha pour des calculs ou des faits."""
        params = {"input": input_text}
        response = await self._make_request(params=params)
        if response and not response.get("error"):
            pods = response.get("queryresult", {}).get("pods", [])
            if pods:
                for pod in pods:
                    if pod.get("title") in ["Result", "Input interpretation", "Decimal approximation"]:
                        subpods = pod.get("subpods", [])
                        if subpods and subpods[0].get("plaintext"):
                            return f"WolframAlpha:\n{subpods[0]['plaintext']}"
                if pods and pods[0].get("subpods") and pods[0]["subpods"][0].get("plaintext"):
                    return f"WolframAlpha:\n{pods[0]['subpods'][0]['plaintext']}"
            return "WolframAlpha: Pas de résultat clair."
        return f"WolframAlpha: Erreur: {response.get('message', 'Inconnu')}" if response else "WolframAlpha: Réponse vide ou erreur interne."

class TavilyClient(APIClient):
    def __init__(self):
        super().__init__("TAVILY", endpoint_health_manager)

    async def query(self, query_text: str, max_results: int = 3) -> str:
        """Effectue une recherche web avancée via l'API Tavily."""
        payload = {"query": query_text, "max_results": max_results}
        response = await self._make_request(json_data=payload)
        if response and not response.get("error"):
            results = response.get("results", [])
            answer = response.get("answer", "Aucune réponse directe trouvée.")

            output = f"Tavily (recherche web):\nRéponse directe: {answer}\n"
            if results:
                output += "Extraits pertinents:\n"
                for i, res in enumerate(results[:max_results]):
                    output += f"- {res.get('title', 'N/A')}: {res.get('content', 'N/A')} {neutralize_urls(res.get('url', ''))}\n"
            return output
        return f"Tavily: Erreur: {response.get('message', 'Inconnu')}" if response else "Tavily: Réponse vide ou erreur interne."

class ApiFlashClient(APIClient):
    def __init__(self):
        super().__init__("APIFLASH", endpoint_health_manager)

    async def query(self, url: str) -> str:
        """Capture une capture d'écran d'une URL via ApiFlash."""
        params = {"url": url, "format": "jpeg", "full_page": "true"}
        response_content = await self._make_request(params=params)

        if isinstance(response_content, bytes):
            selected_endpoint_config = self.endpoint_health_manager.get_best_endpoint(self.name)
            if selected_endpoint_config:
                capture_url = f"{selected_endpoint_config['url']}?access_key={selected_endpoint_config['key']}&url={url}&format=jpeg&full_page=true"
                return f"ApiFlash (capture d'écran): {neutralize_urls(capture_url)} (Vérifiez le lien pour l'image)"
            return "ApiFlash: Impossible de générer l'URL de capture."
        elif isinstance(response_content, dict) and response_content.get("error"):
            return f"ApiFlash: Erreur: {response_content.get('message', 'Inconnu')}"
        else:
            log_message(f"ApiFlash a renvoyé un type de réponse inattendu: {type(response_content)}", level="warning")
            return f"ApiFlash: Réponse inattendue de l'API. {response_content}"

class CrawlbaseClient(APIClient):
    def __init__(self):
        super().__init__("CRAWLBASE", endpoint_health_manager)

    async def query(self, url: str, use_js: bool = False) -> str:
        """Scrape le contenu HTML ou JavaScript d'une URL via Crawlbase."""
        params = {"url": url, "format": "json"}
        
        selected_endpoint_config = None
        if use_js:
            for config in API_CONFIG.get(self.name, []):
                if "JS Scraper" in config.get("endpoint_name", ""):
                    selected_endpoint_config = config
                    break
        
        if not selected_endpoint_config: 
            selected_endpoint_config = self.endpoint_health_manager.get_best_endpoint(self.name)

        if not selected_endpoint_config:
            return f"Crawlbase: Aucun endpoint sain ou disponible pour {self.name}."

        response = await self._make_request(
            params=params,
            url=selected_endpoint_config["url"],
            method=selected_endpoint_config["method"],
            key_field=selected_endpoint_config["key_field"],
            key_location=selected_endpoint_config["key_location"],
            api_key=selected_endpoint_config["key"],
            fixed_params=selected_endpoint_config.get("fixed_params", {}),
            timeout=selected_endpoint_config.get("timeout")
        )

        if response and not response.get("error"):
            body = response.get("body")
            if body:
                try:
                    decoded_body = base64.b64decode(body).decode('utf-8', errors='ignore')
                    return f"Crawlbase (contenu web):\n{decoded_body[:1000]}..."
                except Exception:
                    return f"Crawlbase (contenu web - brut):\n{body[:1000]}..."
            return "Crawlbase: Contenu non trouvé."
        return f"Crawlbase: Erreur: {response.get('message', 'Inconnu')}" if response else "Crawlbase: Réponse vide ou erreur interne."

class DetectLanguageClient(APIClient):
    def __init__(self):
        super().__init__("DETECTLANGUAGE", endpoint_health_manager)

    async def query(self, text: str) -> str:
        """Détecte la langue d'un texte via DetectLanguage API."""
        payload = {"q": text}
        response = await self._make_request(json_data=payload)
        if response and not response.get("error"):
            detections = response.get("data", {}).get("detections", [])
            if detections:
                first_detection = detections[0]
                lang = first_detection.get("language")
                confidence = first_detection.get("confidence")
                return f"Langue détectée: {lang} (confiance: {confidence})"
            return "DetectLanguage: Aucune langue détectée."
        return f"DetectLanguage: Erreur: {response.get('message', 'Inconnu')}" if response else "DetectLanguage: Réponse vide ou erreur interne."

class GuardianClient(APIClient):
    def __init__(self):
        super().__init__("GUARDIAN", endpoint_health_manager)

    async def query(self, query_text: str) -> str:
        """Recherche des articles de presse via l'API The Guardian."""
        params = {"q": query_text}
        response = await self._make_request(params=params)
        if response and not response.get("error"):
            results = response.get("response", {}).get("results", [])
            if results:
                output = "Articles The Guardian:\n"
                for res in results[:3]:
                    output += f"- {res.get('webTitle', 'N/A')}: {res.get('fields', {}).get('trailText', 'N/A')} {neutralize_urls(res.get('webUrl', ''))}\n"
                return output
            return "Guardian: Aucun article trouvé."
        return f"Guardian: Erreur: {response.get('message', 'Inconnu')}" if response else "Guardian: Réponse vide ou erreur interne."

class IP2LocationClient(APIClient):
    def __init__(self):
        super().__init__("IP2LOCATION", endpoint_health_manager)

    async def query(self, ip_address: str) -> str:
        """Géolocalise une adresse IP via IP2Location API."""
        params = {"ip": ip_address}
        response = await self._make_request(params=params)
        if response and not response.get("error"):
            if "country_name" in response:
                return f"IP2Location (Géolocalisation IP {ip_address}): Pays: {response['country_name']}, Ville: {response.get('city_name', 'N/A')}"
            return "IP2Location: Informations non trouvées."
        return f"IP2Location: Erreur: {response.get('message', 'Inconnu')}" if response else "IP2Location: Réponse vide ou erreur interne."

class ShodanClient(APIClient):
    def __init__(self):
        super().__init__("SHODAN", endpoint_health_manager)

    async def query(self, query_text: str = "") -> str:
        """
        Interroge Shodan pour des informations sur un hôte IP ou des informations sur la clé API.
        Si `query_text` est une IP, tente de récupérer les infos de l'hôte.
        Sinon, ou en cas d'échec, retourne les infos de la clé API.
        """
        if re.match(r"^\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}$", query_text):
            selected_endpoint_config = None
            for config in API_CONFIG.get(self.name, []):
                if "Host Info" in config.get("endpoint_name", ""):
                    selected_endpoint_config = config
                    break
            if selected_endpoint_config:
                url = f"{selected_endpoint_config['url'].rstrip('/')}/{query_text}"
                response = await self._make_request(
                    params={"key": selected_endpoint_config["key"]},
                    url=url,
                    method="GET",
                    key_field=selected_endpoint_config["key_field"],
                    key_location=selected_endpoint_config["key_location"],
                    api_key=selected_endpoint_config["key"],
                    timeout=selected_endpoint_config.get("timeout")
                )
                if response and not response.get("error"):
                    return f"Shodan (info hôte {query_text}): Pays: {response.get('country_name', 'N/A')}, Ports: {response.get('ports', 'N/A')}, Vulnérabilités: {response.get('vulns', 'Aucune')}"
                return f"Shodan (info hôte): Erreur: {response.get('message', 'Inconnu')}" if response else "Shodan: Réponse vide ou erreur interne."
            else:
                return "Shodan: Endpoint 'Host Info' non configuré."
        else:
            response = await self._make_request()
            if response and not response.get("error"):
                return f"Shodan (info clé): Requêtes restantes: {response.get('usage_limits', {}).get('query_credits', 'N/A')}, Scan crédits: {response.get('usage_limits', {}).get('scan_credits', 'N/A')}"
            return f"Shodan: Erreur: {response.get('message', 'Inconnu')}" if response else "Shodan: Réponse vide ou erreur interne."

class WeatherAPIClient(APIClient):
    def __init__(self):
        super().__init__("WEATHERAPI", endpoint_health_manager)

    async def query(self, location: str) -> str:
        """Récupère les conditions météorologiques actuelles pour une localisation via WeatherAPI."""
        params = {"q": location}
        response = await self._make_request(params=params)
        if response and not response.get("error"):
            current = response.get("current", {})
            location_info = response.get("location", {})
            if current and location_info:
                return (
                    f"Météo à {location_info.get('name', 'N/A')}, {location_info.get('country', 'N/A')}:\n"
                    f"Température: {current.get('temp_c', 'N/A')}°C, "
                    f"Conditions: {current.get('condition', {}).get('text', 'N/A')}, "
                    f"Vent: {current.get('wind_kph', 'N/A')} km/h"
                )
            return "WeatherAPI: Données météo non trouvées."
        return f"WeatherAPI: Erreur: {response.get('message', 'Inconnu')}" if response else "WeatherAPI: Réponse vide ou erreur interne."

class CloudmersiveClient(APIClient):
    def __init__(self):
        super().__init__("CLOUDMERSIVE", endpoint_health_manager)

    async def query(self, domain: str) -> str:
        """Vérifie la validité et le type d'un domaine via Cloudmersive API."""
        payload = {"domain": domain}
        response = await self._make_request(json_data=payload)
        if response and not response.get("error"):
            return f"Cloudmersive (vérification de domaine {domain}): Valide: {response.get('ValidDomain', 'N/A')}, Type: {response.get('DomainType', 'N/A')}"
        return f"Cloudmersive: Erreur: {response.get('message', 'Inconnu')}" if response else "Cloudmersive: Réponse vide ou erreur interne."

class GreyNoiseClient(APIClient):
    def __init__(self):
        super().__init__("GREYNOISE", endpoint_health_manager)

    async def query(self, ip_address: str) -> str:
        """Analyse une adresse IP pour détecter des activités 'bruit' (malveillantes) via GreyNoise."""
        selected_endpoint_config = self.endpoint_health_manager.get_best_endpoint(self.name)
        if not selected_endpoint_config:
            return f"GreyNoise: Aucun endpoint sain ou disponible pour {self.name}."

        url = f"{selected_endpoint_config['url'].rstrip('/')}/{ip_address}"
        method = selected_endpoint_config["method"]
        headers = {selected_endpoint_config["key_field"]: selected_endpoint_config["key"]}

        response = await self._make_request(
            headers=headers,
            url=url,
            method=method,
            key_field=selected_endpoint_config["key_field"],
            key_location=selected_endpoint_config["key_location"],
            api_key=selected_endpoint_config["key"],
            timeout=selected_endpoint_config.get("timeout")
        )

        if response and not response.get("error"):
            if response.get("noise"):
                return f"GreyNoise (IP {ip_address}): C'est une IP 'bruit' (malveillante). Classification: {response.get('classification', 'N/A')}, Nom d'acteur: {response.get('actor', 'N/A')}"
            return f"GreyNoise (IP {ip_address}): Pas de 'bruit' détecté. Statut: {response.get('status', 'N/A')}"
        return f"GreyNoise: Erreur: {response.get('message', 'Inconnu')}" if response else "GreyNoise: Réponse vide ou erreur interne."

class PulsediveClient(APIClient):
    def __init__(self):
        super().__init__("PULSEDIVE", endpoint_health_manager)

    async def query(self, indicator: str, type: str = "auto") -> str:
        """Analyse un indicateur de menace (IP, domaine, URL) via Pulsedive."""
        params = {"indicator": indicator, "type": type}
        response = await self._make_request(params=params)
        if response and not response.get("error"):
            if response.get("results"):
                result = response["results"][0]
                return (
                    f"Pulsedive (Analyse {indicator}): Type: {result.get('type', 'N/A')}, "
                    f"Risk: {result.get('risk', 'N/A')}, "
                    f"Description: {result.get('description', 'N/A')[:200]}..."
                )
            return "Pulsedive: Aucun résultat d'analyse trouvé."
        return f"Pulsedive: Erreur: {response.get('message', 'Inconnu')}" if response else "Pulsedive: Réponse vide ou erreur interne."

class StormGlassClient(APIClient):
    def __init__(self):
        super().__init__("STORMGLASS", endpoint_health_manager)

    async def query(self, lat: float, lng: float, params: str = "airTemperature,waveHeight") -> str:
        """Récupère les données météorologiques maritimes pour une coordonnée via StormGlass."""
        now = int(time.time())
        request_params = {
            "lat": lat,
            "lng": lng,
            "params": params,
            "start": now,
            "end": now + 3600
        }
        response = await self._make_request(params=request_params)
        if response and not response.get("error"):
            data = response.get("hours", [])
            if data:
                first_hour = data[0]
                temp = first_hour.get('airTemperature', [{}])[0].get('value', 'N/A')
                wave_height = first_hour.get('waveHeight', [{}])[0].get('value', 'N/A')
                return f"StormGlass (Météo maritime à {lat},{lng}): Température air: {temp}°C, Hauteur vagues: {wave_height}m"
            return "StormGlass: Données non trouvées."
        return f"StormGlass: Erreur: {response.get('message', 'Inconnu')}" if response else "StormGlass: Réponse vide ou erreur interne."

class LoginRadiusClient(APIClient):
    def __init__(self):
        super().__init__("LOGINRADIUS", endpoint_health_manager)

    async def query(self) -> str:
        """Effectue un simple ping à l'API LoginRadius pour vérifier sa disponibilité."""
        response = await self._make_request()
        if response and not response.get("error"):
            return f"LoginRadius (Ping API): Statut: {response.get('Status', 'N/A')}, Message: {response.get('Message', 'N/A')}"
        return f"LoginRadius: Erreur: {response.get('message', 'Inconnu')}" if response else "LoginRadius: Réponse vide ou erreur interne."

class JsonbinClient(APIClient):
    def __init__(self):
        super().__init__("JSONBIN", endpoint_health_manager)

    async def query(self, data: Optional[Dict[str, Any]] = None, private: bool = True, bin_id: Optional[str] = None) -> str:
        """
        Crée un nouveau 'bin' JSON ou accède à un bin existant via Jsonbin.io.
        `data` est pour la création, `bin_id` pour l'accès.
        """
        if bin_id:
            selected_endpoint_config = None
            for config in API_CONFIG.get(self.name, []):
                if "Bin Access" in config.get("endpoint_name", ""):
                    selected_endpoint_config = config
                    break
            if not selected_endpoint_config:
                return f"Jsonbin: Aucun endpoint d'accès de bin sain ou disponible pour {self.name}."

            url = f"{selected_endpoint_config['url'].rstrip('/')}/{bin_id}"
            method = "GET"
            headers = {selected_endpoint_config["key_field"]: selected_endpoint_config["key"]}
            
            response = await self._make_request(
                headers=headers,
                url=url,
                method=method,
                timeout=selected_endpoint_config.get("timeout")
            )
            if response and not response.get("error"):
                return f"Jsonbin (Accès bin {bin_id}):\n{json.dumps(response, indent=2)}"
            return f"Jsonbin (Accès bin): Erreur: {response.get('message', 'Inconnu')}" if response else "Jsonbin: Réponse vide ou erreur interne."
        
        else:
            selected_endpoint_config = None
            for config in API_CONFIG.get(self.name, []):
                if "Bin Create" in config.get("endpoint_name", ""):
                    selected_endpoint_config = config
                    break
            
            if not selected_endpoint_config:
                return f"Jsonbin: Aucun endpoint de création de bin sain ou disponible pour {self.name}."

            url = selected_endpoint_config["url"]
            method = "POST"
            headers = {selected_endpoint_config["key_field"]: selected_endpoint_config["key"], "Content-Type": "application/json"}
            payload = {"record": data if data is not None else {}, "private": private}

            response = await self._make_request(
                json_data=payload,
                headers=headers,
                url=url,
                method=method,
                timeout=selected_endpoint_config.get("timeout")
            )

            if response and not response.get("error"):
                return f"Jsonbin (Création de bin): ID: {response.get('metadata', {}).get('id', 'N/A')}, URL: {neutralize_urls(response.get('metadata', {}).get('url', 'N/A'))}"
            return f"Jsonbin (Création de bin): Erreur: {response.get('message', 'Inconnu')}" if response else "Jsonbin: Réponse vide ou erreur interne."

class HuggingFaceClient(APIClient):
    def __init__(self):
        super().__init__("HUGGINGFACE", endpoint_health_manager)

    async def query(self, model_name: str = "distilbert-base-uncased-finetuned-sst-2-english", input_text: str = "Hello world") -> str:
        """Effectue une inférence sur un modèle HuggingFace (ex: classification de texte, génération)."""
        selected_endpoint_config = self.endpoint_health_manager.get_best_endpoint(self.name)
        if not selected_endpoint_config:
            return f"HuggingFace: Aucun endpoint sain ou disponible pour {self.name}."

        inference_url = f"https://api-inference.huggingface.co/models/{model_name}"
        
        headers = {
            selected_endpoint_config["key_field"]: f"{selected_endpoint_config['key_prefix']}{selected_endpoint_config['key']}",
            "Content-Type": "application/json"
        }
        payload = {"inputs": input_text}

        response = await self._make_request(
            json_data=payload,
            headers=headers,
            url=inference_url,
            method="POST",
            timeout=selected_endpoint_config.get("timeout")
        )

        if response and not response.get("error"):
            if isinstance(response, list) and response:
                first_result = response[0]
                if isinstance(first_result, list) and first_result:
                    return f"HuggingFace ({model_name} - {first_result[0].get('label')}): Score {first_result[0].get('score', 'N/A'):.2f}"
                elif isinstance(first_result, dict) and "generated_text" in first_result:
                    return f"HuggingFace ({model_name}): {first_result.get('generated_text')}"
            return f"HuggingFace ({model_name}): Réponse non parsée. {response}"
        return f"HuggingFace: Erreur: {response.get('message', 'Inconnu')}" if response else "HuggingFace: Réponse vide ou erreur interne."

class TwilioClient(APIClient):
    def __init__(self):
        super().__init__("TWILIO", endpoint_health_manager)

    async def query(self) -> str:
        """Récupère le solde du compte Twilio."""
        selected_endpoint_config = None
        for config in API_CONFIG.get(self.name, []):
            if "Account Balance" in config.get("endpoint_name", ""):
                selected_endpoint_config = config
                break
        if not selected_endpoint_config:
            if self.endpoints_config:
                selected_endpoint_config = self.endpoints_config[0]
            else:
                return f"Twilio: Aucune configuration d'endpoint disponible pour {self.name}."

        response = await self._make_request(
            url=selected_endpoint_config["url"],
            method=selected_endpoint_config["method"],
            key_location=selected_endpoint_config["key_location"],
            api_key=selected_endpoint_config["key"],
            timeout=selected_endpoint_config.get("timeout")
        )
        if response and not response.get("error"):
            return f"Twilio (Balance): {response.get('balance', 'N/A')} {response.get('currency', 'N/A')}"
        return f"Twilio: Erreur: {response.get('message', 'Inconnu')}" if response else "Twilio: Réponse vide ou erreur interne."

class AbstractAPIClient(APIClient):
    def __init__(self):
        super().__init__("ABSTRACTAPI", endpoint_health_manager)

    async def query(self, input_value: str, api_type: str) -> str:
        """
        Interroge diverses APIs d'AbstractAPI (validation email/téléphone, taux de change, jours fériés).
        `input_value` dépend du `api_type`.
        """
        params = {}
        target_endpoint_name = ""

        if api_type == "PHONE_VALIDATION":
            params["phone"] = input_value
            target_endpoint_name = "Phone Validation"
        elif api_type == "EMAIL_VALIDATION":
            params["email"] = input_value
            target_endpoint_name = "Email Validation"
        elif api_type == "EXCHANGE_RATES":
            params["base"] = input_value if input_value else "USD" 
            target_endpoint_name = "Exchange Rates"
        elif api_type == "HOLIDAYS":
            params["country"] = input_value if input_value else "US"
            from datetime import datetime
            params["year"] = datetime.now(timezone.utc).year
            target_endpoint_name = "Holidays"
        else:
            return f"AbstractAPI: Type d'API '{api_type}' non supporté pour la requête."

        selected_endpoint_config = None
        for config in API_CONFIG.get(self.name, []):
            if target_endpoint_name in config["endpoint_name"]:
                selected_endpoint_config = config
                break
        
        if not selected_endpoint_config:
            return f"AbstractAPI: Aucun endpoint sain ou disponible pour {self.name} pour le type {api_type}."

        response = await self._make_request(
            params=params,
            url=selected_endpoint_config["url"],
            method=selected_endpoint_config["method"],
            key_field=selected_endpoint_config["key_field"],
            key_location=selected_endpoint_config["key_location"],
            api_key=selected_endpoint_config["key"],
            fixed_params=selected_endpoint_config.get("fixed_params", {}),
            timeout=selected_endpoint_config.get("timeout")
        )

        if response and not response.get("error"):
            if api_type == "PHONE_VALIDATION":
                return (
                    f"AbstractAPI (Validation Tél): Numéro: {response.get('phone', 'N/A')}, "
                    f"Valide: {response.get('valid', 'N/A')}, "
                    f"Pays: {response.get('country', {}).get('name', 'N/A')}"
                )
            elif api_type == "EMAIL_VALIDATION":
                return (
                    f"AbstractAPI (Validation Email): Email: {response.get('email', 'N/A')}, "
                    f"Valide: {response.get('is_valid_format', 'N/A')}, "
                    f"Deliverable: {response.get('is_deliverable', 'N/A')}"
                )
            elif api_type == "EXCHANGE_RATES":
                return f"AbstractAPI (Taux de change): Base: {response.get('base', 'N/A')}, Taux (USD): {response.get('exchange_rates', {}).get('USD', 'N/A')}"
            elif api_type == "HOLIDAYS":
                holidays = [h.get('name', 'N/A') for h in response if h.get('name')]
                return f"AbstractAPI (Jours fériés {params.get('country', 'US')} {params.get('year')}): {', '.join(holidays[:5])}..." if holidays else "Aucun jour férié trouvé."
            return f"AbstractAPI ({api_type}): Réponse brute: {response}"
        return f"AbstractAPI ({api_type}): Erreur: {response.get('message', 'Inconnu')}" if response else "AbstractAPI: Réponse vide ou erreur interne."

class GoogleCustomSearchClient(APIClient):
    def __init__(self):
        super().__init__("GOOGLE_CUSTOM_SEARCH", endpoint_health_manager)

    async def query(self, query_text: str) -> str:
        """Effectue une recherche personnalisée Google via l'API Custom Search."""
        params = {"q": query_text}
        response = await self._make_request(params=params)
        if response and not response.get("error"):
            items = response.get("items", [])
            if items:
                output = "Google Custom Search:\n"
                for item in items[:3]:
                    output += f"- {item.get('title', 'N/A')}: {item.get('snippet', 'N/A')} {neutralize_urls(item.get('link', ''))}\n"
                return output
            return "Google Custom Search: Aucun résultat trouvé."
        return f"Google Custom Search: Erreur: {response.get('message', 'Inconnu')}" if response else "Google Custom Search: Réponse vide ou erreur interne."

class RandommerClient(APIClient):
    def __init__(self):
        super().__init__("RANDOMMER", endpoint_health_manager)

    async def query(self, country_code: str = "US", quantity: int = 1) -> str:
        """Génère des numéros de téléphone aléatoires via Randommer.io."""
        params = {"CountryCode": country_code, "Quantity": quantity}
        response = await self._make_request(params=params)
        if response and not response.get("error"):
            if isinstance(response, list) and response:
                return f"Randommer (Numéros de téléphone): {', '.join(response)}"
            return f"Randommer: {response}"
        return f"Randommer: Erreur: {response.get('message', 'Inconnu')}" if response else "Randommer: Réponse vide ou erreur interne."

class TomorrowIOClient(APIClient):
    def __init__(self):
        super().__init__("TOMORROW.IO", endpoint_health_manager)

    async def query(self, location: str, fields: Optional[List[str]] = None) -> str:
        """Récupère les prévisions météorologiques via Tomorrow.io."""
        if fields is None:
            fields = ["temperature", "humidity", "windSpeed"]
        payload = {"location": location, "fields": fields, "units": "metric", "timesteps": ["1h"]}
        response = await self._make_request(json_data=payload)
        if response and not response.get("error"):
            data = response.get("data", {}).get("timelines", [{}])[0].get("intervals", [{}])[0].get("values", {})
            if data:
                output = f"Météo (Tomorrow.io) à {location}:\n"
                for field in fields:
                    output += f"- {field.capitalize()}: {data.get(field, 'N/A')}\n"
                return output
            return "Tomorrow.io: Données météo non trouvées."
        return f"Tomorrow.io: Erreur: {response.get('message', 'Inconnu')}" if response else "Tomorrow.io: Réponse vide ou erreur interne."

class OpenWeatherMapClient(APIClient):
    def __init__(self):
        super().__init__("OPENWEATHERMAP", endpoint_health_manager)

    async def query(self, location: str) -> str:
        """Récupère les conditions météorologiques actuelles via OpenWeatherMap."""
        params = {"q": location}
        response = await self._make_request(params=params)
        if response and not response.get("error"):
            main_data = response.get("main", {})
            weather_desc = response.get("weather", [{}])[0].get("description", "N/A")
            if main_data:
                temp_kelvin = main_data.get('temp', 'N/A')
                feels_like_kelvin = main_data.get('feels_like', 'N/A')
                
                temp_celsius = f"{temp_kelvin - 273.15:.2f}" if isinstance(temp_kelvin, (int, float)) else "N/A"
                feels_like_celsius = f"{feels_like_kelvin - 273.15:.2f}" if isinstance(feels_like_kelvin, (int, float)) else "N/A"

                return (
                    f"Météo (OpenWeatherMap) à {location}:\n"
                    f"Température: {temp_celsius}°C, "
                    f"Ressenti: {feels_like_celsius}°C, "
                    f"Humidité: {main_data.get('humidity', 'N/A')}%, "
                    f"Conditions: {weather_desc}"
                )
            return "OpenWeatherMap: Données météo non trouvées."
        return f"OpenWeatherMap: Erreur: {response.get('message', 'Inconnu')}" if response else "OpenWeatherMap: Réponse vide ou erreur interne."

class MockarooClient(APIClient):
    def __init__(self):
        super().__init__("MOCKAROO", endpoint_health_manager)

    async def query(self, count: int = 1, fields_json: Optional[str] = None) -> str:
        """Génère des données de test via Mockaroo."""
        params = {"count": count}
        if fields_json:
            params["fields"] = fields_json
        response = await self._make_request(params=params)
        if response and not response.get("error"):
            return f"Mockaroo (Génération de données):\n{json.dumps(response, indent=2)}"
        return f"Mockaroo: Erreur: {response.get('message', 'Inconnu')}" if response else "Mockaroo: Réponse vide ou erreur interne."

class OpenPageRankClient(APIClient):
    def __init__(self):
        super().__init__("OPENPAGERANK", endpoint_health_manager)

    async def query(self, domains: List[str]) -> str:
        """Récupère le PageRank de domaines via OpenPageRank."""
        params = {"domains[]": domains}
        response = await self._make_request(params=params)
        if response and not response.get("error"):
            results = response.get("response", [])
            if results:
                output = "OpenPageRank (Classement de domaine):\n"
                for res in results:
                    output += f"- Domaine: {res.get('domain', 'N/A')}, PageRank: {res.get('page_rank', 'N/A')}\n"
                return output
            return "OpenPageRank: Aucun résultat trouvé."
        return f"OpenPageRank: Erreur: {response.get('message', 'Inconnu')}" if response else "OpenPageRank: Réponse vide ou erreur interne."

class RapidAPIClient(APIClient):
    def __init__(self):
        super().__init__("RAPIDAPI", endpoint_health_manager)

    async def query(self, api_name: str, **kwargs) -> str:
        """
        Interroge diverses APIs disponibles via RapidAPI (blagues, taux de change, faits aléatoires).
        `api_name` spécifie l'API RapidAPI à utiliser.
        """
        selected_endpoint_config = None
        for config in API_CONFIG.get(self.name, []):
            if api_name.lower() in config["endpoint_name"].lower():
                selected_endpoint_config = config
                break
        
        if not selected_endpoint_config:
            return f"RapidAPI: Endpoint pour '{api_name}' non trouvé ou non configuré."

        url = selected_endpoint_config["url"]
        method = selected_endpoint_config["method"]
        
        request_params = selected_endpoint_config.get("fixed_params", {}).copy()
        request_headers = selected_endpoint_config.get("fixed_headers", {}).copy()
        request_json_data = selected_endpoint_config.get("fixed_json", {}).copy()

        if method == "GET":
            request_params.update(kwargs)
        elif method == "POST":
            request_json_data.update(kwargs)

        headers = {
            selected_endpoint_config["key_field"]: selected_endpoint_config["key"],
            "X-RapidAPI-Host": selected_endpoint_config["fixed_headers"].get("X-RapidAPI-Host")
        }
        
        response = await self._make_request(
            params=request_params,
            headers=headers,
            json_data=request_json_data,
            url=url,
            method=method,
            timeout=selected_endpoint_config.get("timeout")
        )

        if response and not response.get("error"):
            if api_name.lower() == "programming joke":
                return f"RapidAPI (Blague de Programmation): {response.get('setup', '')} - {response.get('punchline', '')}"
            elif api_name.lower() == "currency list quotes":
                return f"RapidAPI (Devises): {json.dumps(response, indent=2)}"
            elif api_name.lower() == "random fact":
                return f"RapidAPI (Fait Aléatoire): {response.get('text', 'N/A')}"
            return f"RapidAPI ({api_name}): {json.dumps(response, indent=2)}"
        return f"RapidAPI ({api_name}): Erreur: {response.get('message', 'Inconnu')}" if response else "RapidAPI: Réponse vide ou erreur interne."

# Liste de tous les clients API instanciables
ALL_API_CLIENTS = [
    GeminiAPIClient(),
    OCRApiClient(),
    DeepSeekClient(),
    SerperClient(),
    WolframAlphaClient(),
    TavilyClient(),
    ApiFlashClient(),
    CrawlbaseClient(),
    DetectLanguageClient(),
    GuardianClient(),
    IP2LocationClient(),
    ShodanClient(),
    WeatherAPIClient(),
    CloudmersiveClient(),
    GreyNoiseClient(),
    PulsediveClient(),
    StormGlassClient(),
    LoginRadiusClient(),
    JsonbinClient(),
    HuggingFaceClient(),
    TwilioClient(),
    AbstractAPIClient(),
    GoogleCustomSearchClient(),
    RandommerClient(),
    TomorrowIOClient(),
    OpenWeatherMapClient(),
    MockarooClient(),
    OpenPageRankClient(),
    RapidAPIClient()
]

import asyncio
import json
import re
import base64
from typing import Dict, Any, List, Optional, Union

# Import des clients API
from api_clients import (
    GeminiAPIClient, OCRApiClient, DeepSeekClient, SerperClient,
    WolframAlphaClient, TavilyClient, ApiFlashClient, CrawlbaseClient,
    DetectLanguageClient, GuardianClient, IP2LocationClient, ShodanClient,
    WeatherAPIClient, CloudmersiveClient, GreyNoiseClient, PulsediveClient,
    StormGlassClient, LoginRadiusClient, JsonbinClient, HuggingFaceClient,
    TwilioClient, AbstractAPIClient, GoogleCustomSearchClient,
    RandommerClient, TomorrowIOClient, OpenWeatherMapClient, MockarooClient,
    OpenPageRankClient, RapidAPIClient
)

# Import des fonctions utilitaires
from utils import log_message, neutralize_urls, find_tool_by_name
from config import TOOL_CONFIG

# Instanciation des clients API
gemini_client = GeminiAPIClient()
ocr_client = OCRApiClient()
deepseek_client = DeepSeekClient()
serper_client = SerperClient()
wolfram_alpha_client = WolframAlphaClient()
tavily_client = TavilyClient()
apiflash_client = ApiFlashClient()
crawlbase_client = CrawlbaseClient()
detect_language_client = DetectLanguageClient()
guardian_client = GuardianClient()
ip2location_client = IP2LocationClient()
shodan_client = ShodanClient()
weather_api_client = WeatherAPIClient()
cloudmersive_client = CloudmersiveClient()
greynoise_client = GreyNoiseClient()
pulsedive_client = PulsediveClient()
stormglass_client = StormGlassClient()
loginradius_client = LoginRadiusClient()
jsonbin_client = JsonbinClient()
huggingface_client = HuggingFaceClient()
twilio_client = TwilioClient()
abstractapi_client = AbstractAPIClient()
google_custom_search_client = GoogleCustomSearchClient()
randommer_client = RandommerClient()
tomorrow_io_client = TomorrowIOClient()
openweathermap_client = OpenWeatherMapClient()
mockaroo_client = MockarooClient()
openpagerank_client = OpenPageRankClient()
rapidapi_client = RapidAPIClient()

async def execute_tool(tool_name: str, **kwargs) -> str:
    """
    Exécute un outil spécifique en fonction de son nom et des arguments fournis.
    C'est le point d'entrée principal pour l'exécution de toutes les fonctions d'outils.
    """
    log_message(f"Exécution de l'outil: {tool_name} avec kwargs: {kwargs}")
    tool_config = find_tool_by_name(tool_name)

    if not tool_config:
        log_message(f"Outil non trouvé: {tool_name}", level="error")
        return f"Erreur: Outil '{tool_name}' non trouvé ou non configuré."

    try:
        if tool_name == "google_search":
            return await google_search_tool(kwargs.get("queries"))
        elif tool_name == "media_control":
            action = kwargs.get("action")
            if action == "like":
                return await media_control_like_tool()
            elif action == "dislike":
                return await media_control_dislike_tool()
            elif action == "next":
                return await media_control_next_tool()
            elif action == "previous":
                return await media_control_previous_tool()
            elif action == "pause":
                return await media_control_pause_tool()
            elif action == "resume":
                return await media_control_resume_tool()
            elif action == "stop":
                return await media_control_stop_tool()
            elif action == "replay":
                return await media_control_replay_tool()
            elif action == "seek_absolute":
                return await media_control_seek_absolute_tool(kwargs.get("position"))
            elif action == "seek_relative":
                return await media_control_seek_relative_tool(kwargs.get("offset"))
            else:
                return f"Action non supportée pour media_control: {action}"
        elif tool_name == "clock":
            action = kwargs.get("action")
            if action == "create_alarm":
                return await clock_create_alarm_tool(
                    duration=kwargs.get("duration"),
                    time=kwargs.get("time"),
                    date=kwargs.get("date"),
                    label=kwargs.get("label"),
                    recurrence=kwargs.get("recurrence")
                )
            elif action == "create_timer":
                return await clock_create_timer_tool(
                    duration=kwargs.get("duration"),
                    time=kwargs.get("time"),
                    label=kwargs.get("label")
                )
            elif action == "show_matching_alarms":
                return await clock_show_matching_alarms_tool(
                    query=kwargs.get("query"),
                    alarm_type=kwargs.get("alarm_type"),
                    alarm_ids=kwargs.get("alarm_ids"),
                    date=kwargs.get("date"),
                    start_date=kwargs.get("start_date"),
                    end_date=kwargs.get("end_date")
                )
            elif action == "show_matching_timers":
                return await clock_show_matching_timers_tool(
                    query=kwargs.get("query"),
                    timer_type=kwargs.get("timer_type"),
                    timer_ids=kwargs.get("timer_ids")
                )
            elif action == "modify_alarm_v2":
                return await clock_modify_alarm_v2_tool(
                    alarm_filters=kwargs.get("alarm_filters"),
                    alarm_modifications=kwargs.get("alarm_modifications")
                )
            elif action == "modify_timer_v2":
                return await clock_modify_timer_v2_tool(
                    timer_filters=kwargs.get("timer_filters"),
                    timer_modifications=kwargs.get("timer_modifications")
                )
            elif action == "snooze":
                return await clock_snooze_tool()
            else:
                return f"Action non supportée pour clock: {action}"
        elif tool_name == "ocr_space":
            return await ocr_space_tool(kwargs.get("image_base64"))
        elif tool_name == "deepseek_chat":
            return await deepseek_chat_tool(kwargs.get("prompt"), kwargs.get("model"))
        elif tool_name == "serper_dev":
            return await serper_dev_tool(kwargs.get("query_text"))
        elif tool_name == "wolfram_alpha":
            return await wolfram_alpha_tool(kwargs.get("input_text"))
        elif tool_name == "tavily_search":
            return await tavily_search_tool(kwargs.get("query_text"), kwargs.get("max_results"))
        elif tool_name == "apiflash_screenshot":
            return await apiflash_screenshot_tool(kwargs.get("url"))
        elif tool_name == "crawlbase_scraper":
            return await crawlbase_scraper_tool(kwargs.get("url"), kwargs.get("use_js"))
        elif tool_name == "detect_language":
            return await detect_language_tool(kwargs.get("text"))
        elif tool_name == "guardian_news":
            return await guardian_news_tool(kwargs.get("query_text"))
        elif tool_name == "ip2location":
            return await ip2location_tool(kwargs.get("ip_address"))
        elif tool_name == "shodan":
            return await shodan_tool(kwargs.get("query_text"))
        elif tool_name == "weather_api":
            return await weather_api_tool(kwargs.get("location"))
        elif tool_name == "cloudmersive_domain":
            return await cloudmersive_domain_tool(kwargs.get("domain"))
        elif tool_name == "greynoise":
            return await greynoise_tool(kwargs.get("ip_address"))
        elif tool_name == "pulsedive":
            return await pulsedive_tool(kwargs.get("indicator"), kwargs.get("type"))
        elif tool_name == "stormglass":
            return await stormglass_tool(kwargs.get("lat"), kwargs.get("lng"), kwargs.get("params"))
        elif tool_name == "loginradius_ping":
            return await loginradius_ping_tool()
        elif tool_name == "jsonbin_io":
            return await jsonbin_io_tool(kwargs.get("data"), kwargs.get("private"), kwargs.get("bin_id"))
        elif tool_name == "huggingface_inference":
            return await huggingface_inference_tool(kwargs.get("model_name"), kwargs.get("input_text"))
        elif tool_name == "twilio_balance":
            return await twilio_balance_tool()
        elif tool_name == "abstractapi":
            return await abstractapi_tool(kwargs.get("input_value"), kwargs.get("api_type"))
        elif tool_name == "google_custom_search":
            return await google_custom_search_tool(kwargs.get("query_text"))
        elif tool_name == "randommer_phone":
            return await randommer_phone_tool(kwargs.get("country_code"), kwargs.get("quantity"))
        elif tool_name == "tomorrow_io_weather":
            return await tomorrow_io_weather_tool(kwargs.get("location"), kwargs.get("fields"))
        elif tool_name == "openweathermap_weather":
            return await openweathermap_weather_tool(kwargs.get("location"))
        elif tool_name == "mockaroo_data":
            return await mockaroo_data_tool(kwargs.get("count"), kwargs.get("fields_json"))
        elif tool_name == "openpagerank":
            return await openpagerank_tool(kwargs.get("domains"))
        elif tool_name == "rapidapi":
            return await rapidapi_tool(kwargs.get("api_name"), **kwargs.get("api_kwargs", {}))
        else:
            log_message(f"Aucun gestionnaire d'outil défini pour: {tool_name}", level="error")
            return f"Erreur: Aucun gestionnaire d'outil défini pour '{tool_name}'."
    except Exception as e:
        log_message(f"Erreur lors de l'exécution de l'outil {tool_name}: {e}", level="error")
        return f"Erreur lors de l'exécution de l'outil {tool_name}: {e}"

# --- Fonctions d'outils spécifiques (wrappers autour des clients API) ---

async def google_search_tool(queries: List[str]) -> str:
    """Effectue une recherche Google."""
    results = []
    for query in queries:
        log_message(f"Recherche Google pour: {query}")
        # Ici, nous utilisons un client générique pour Google Search
        # car il n'y a pas de client spécifique 'google_search' dans api_clients.py
        # Il faudrait soit créer un GoogleSearchClient, soit utiliser un client existant
        # comme SerperClient ou TavilyClient pour simuler la recherche.
        # Pour l'exemple, nous allons simuler une réponse ou utiliser un client de recherche existant.
        # Si 'google_search' est censé utiliser Serper ou Tavily, il faut le mapper ici.
        # Supposons que 'google_search' est un alias pour 'serper_dev' pour cet exemple.
        response = await serper_client.query(query)
        results.append(f"Résultat pour '{query}': {response}")
    return "\n".join(results)

async def media_control_like_tool() -> str:
    """Aime le média en cours de lecture."""
    # Simule l'appel à l'API media_control.like()
    # Dans un vrai scénario, cela appellerait une API de contrôle média sur l'appareil.
    log_message("Action media_control.like() simulée.")
    return "Média actuel aimé."

async def media_control_dislike_tool() -> str:
    """N'aime pas le média en cours de lecture."""
    log_message("Action media_control.dislike() simulée.")
    return "Média actuel non aimé."

async def media_control_next_tool() -> str:
    """Passe à l'élément multimédia suivant."""
    log_message("Action media_control.next() simulée.")
    return "Passage au média suivant."

async def media_control_previous_tool() -> str:
    """Passe à l'élément multimédia précédent."""
    log_message("Action media_control.previous() simulée.")
    return "Passage au média précédent."

async def media_control_pause_tool() -> str:
    """Met en pause le média en cours de lecture."""
    log_message("Action media_control.pause() simulée.")
    return "Média actuel mis en pause."

async def media_control_resume_tool() -> str:
    """Reprend la lecture du média en pause."""
    log_message("Action media_control.resume() simulée.")
    return "Lecture du média reprise."

async def media_control_stop_tool() -> str:
    """Arrête le média en cours de lecture."""
    log_message("Action media_control.stop() simulée.")
    return "Média actuel arrêté."

async def media_control_replay_tool() -> str:
    """Rejoue le média actuel depuis le début."""
    log_message("Action media_control.replay() simulée.")
    return "Média actuel rejoué."

async def media_control_seek_absolute_tool(position: int) -> str:
    """Saute à une position absolue dans le média."""
    log_message(f"Action media_control.seek_absolute({position}) simulée.")
    return f"Média avancé à la position {position} secondes."

async def media_control_seek_relative_tool(offset: int) -> str:
    """Ajuste la lecture du média par une durée relative."""
    log_message(f"Action media_control.seek_relative({offset}) simulée.")
    return f"Média avancé de {offset} secondes."

async def clock_create_alarm_tool(duration: Optional[str] = None, time: Optional[str] = None, date: Optional[str] = None, label: Optional[str] = None, recurrence: Optional[List[str]] = None) -> str:
    """Crée une alarme."""
    # Simule l'appel à l'API clock.create_alarm()
    log_message(f"Action clock.create_alarm() simulée avec durée={duration}, heure={time}, date={date}, label={label}, récurrence={recurrence}.")
    return f"Alarme créée pour {time if time else duration}."

async def clock_create_timer_tool(duration: Optional[str] = None, time: Optional[str] = None, label: Optional[str] = None) -> str:
    """Crée un minuteur."""
    # Simule l'appel à l'API clock.create_timer()
    log_message(f"Action clock.create_timer() simulée avec durée={duration}, heure={time}, label={label}.")
    return f"Minuteur créé pour {time if time else duration}."

async def clock_show_matching_alarms_tool(query: Optional[str] = None, alarm_type: Optional[str] = None, alarm_ids: Optional[List[str]] = None, date: Optional[str] = None, start_date: Optional[str] = None, end_date: Optional[str] = None) -> str:
    """Affiche les alarmes correspondantes."""
    # Simule l'appel à l'API clock.show_matching_alarms()
    log_message(f"Action clock.show_matching_alarms() simulée avec query={query}, type={alarm_type}, ids={alarm_ids}, date={date}, start_date={start_date}, end_date={end_date}.")
    return "Affichage des alarmes correspondantes (simulé)."

async def clock_show_matching_timers_tool(query: Optional[str] = None, timer_type: Optional[str] = None, timer_ids: Optional[List[str]] = None) -> str:
    """Affiche les minuteurs correspondants."""
    # Simule l'appel à l'API clock.show_matching_timers()
    log_message(f"Action clock.show_matching_timers() simulée avec query={query}, type={timer_type}, ids={timer_ids}.")
    return "Affichage des minuteurs correspondants (simulé)."

async def clock_modify_alarm_v2_tool(alarm_filters: Dict[str, Any], alarm_modifications: Dict[str, Any]) -> str:
    """Modifie une alarme."""
    # Simule l'appel à l'API clock.modify_alarm_v2()
    log_message(f"Action clock.modify_alarm_v2() simulée avec filtres={alarm_filters}, modifications={alarm_modifications}.")
    return "Alarme modifiée (simulé)."

async def clock_modify_timer_v2_tool(timer_filters: Dict[str, Any], timer_modifications: Dict[str, Any]) -> str:
    """Modifie un minuteur."""
    # Simule l'appel à l'API clock.modify_timer_v2()
    log_message(f"Action clock.modify_timer_v2() simulée avec filtres={timer_filters}, modifications={timer_modifications}.")
    return "Minuteur modifié (simulé)."

async def clock_snooze_tool() -> str:
    """Met en veille une alarme."""
    # Simule l'appel à l'API clock.snooze()
    log_message("Action clock.snooze() simulée.")
    return "Alarme mise en veille."

async def ocr_space_tool(image_base64: str) -> str:
    """Extrait le texte d'une image via OCR.space."""
    return await ocr_client.query(image_base64)

async def deepseek_chat_tool(prompt: Union[str, List[Dict]], model: str = "deepseek-chat") -> str:
    """Interroge DeepSeek pour des conversations ou complétions."""
    return await deepseek_client.query(prompt, model)

async def serper_dev_tool(query_text: str) -> str:
    """Effectue une recherche web via Serper."""
    return await serper_client.query(query_text)

async def wolfram_alpha_tool(input_text: str) -> str:
    """Interroge WolframAlpha pour des calculs ou des faits."""
    return await wolfram_alpha_client.query(input_text)

async def tavily_search_tool(query_text: str, max_results: int = 3) -> str:
    """Effectue une recherche web avancée via Tavily."""
    return await tavily_client.query(query_text, max_results)

async def apiflash_screenshot_tool(url: str) -> str:
    """Capture une capture d'écran d'une URL via ApiFlash."""
    return await apiflash_client.query(url)

async def crawlbase_scraper_tool(url: str, use_js: bool = False) -> str:
    """Scrape le contenu HTML ou JavaScript d'une URL via Crawlbase."""
    return await crawlbase_client.query(url, use_js)

async def detect_language_tool(text: str) -> str:
    """Détecte la langue d'un texte via DetectLanguage API."""
    return await detect_language_client.query(text)

async def guardian_news_tool(query_text: str) -> str:
    """Recherche des articles de presse via l'API The Guardian."""
    return await guardian_client.query(query_text)

async def ip2location_tool(ip_address: str) -> str:
    """Géolocalise une adresse IP via IP2Location API."""
    return await ip2location_client.query(ip_address)

async def shodan_tool(query_text: str = "") -> str:
    """Interroge Shodan pour des informations sur un hôte IP ou des informations sur la clé API."""
    return await shodan_client.query(query_text)

async def weather_api_tool(location: str) -> str:
    """Récupère les conditions météorologiques actuelles pour une localisation via WeatherAPI."""
    return await weather_api_client.query(location)

async def cloudmersive_domain_tool(domain: str) -> str:
    """Vérifie la validité et le type d'un domaine via Cloudmersive API."""
    return await cloudmersive_client.query(domain)

async def greynoise_tool(ip_address: str) -> str:
    """Analyse une adresse IP pour détecter des activités 'bruit' (malveillantes) via GreyNoise."""
    return await greynoise_client.query(ip_address)

async def pulsedive_tool(indicator: str, type: str = "auto") -> str:
    """Analyse un indicateur de menace (IP, domaine, URL) via Pulsedive."""
    return await pulsedive_client.query(indicator, type)

async def stormglass_tool(lat: float, lng: float, params: str = "airTemperature,waveHeight") -> str:
    """Récupère les données météorologiques maritimes pour une coordonnée via StormGlass."""
    return await stormglass_client.query(lat, lng, params)

async def loginradius_ping_tool() -> str:
    """Effectue un simple ping à l'API LoginRadius pour vérifier sa disponibilité."""
    return await loginradius_client.query()

async def jsonbin_io_tool(data: Optional[Dict[str, Any]] = None, private: bool = True, bin_id: Optional[str] = None) -> str:
    """Crée un nouveau 'bin' JSON ou accède à un bin existant via Jsonbin.io."""
    return await jsonbin_client.query(data, private, bin_id)

async def huggingface_inference_tool(model_name: str = "distilbert-base-uncased-finetuned-sst-2-english", input_text: str = "Hello world") -> str:
    """Effectue une inférence sur un modèle HuggingFace."""
    return await huggingface_client.query(model_name, input_text)

async def twilio_balance_tool() -> str:
    """Récupère le solde du compte Twilio."""
    return await twilio_client.query()

async def abstractapi_tool(input_value: str, api_type: str) -> str:
    """Interroge diverses APIs d'AbstractAPI."""
    return await abstractapi_client.query(input_value, api_type)

async def google_custom_search_tool(query_text: str) -> str:
    """Effectue une recherche personnalisée Google."""
    return await google_custom_search_client.query(query_text)

async def randommer_phone_tool(country_code: str = "US", quantity: int = 1) -> str:
    """Génère des numéros de téléphone aléatoires via Randommer.io."""
    return await randommer_client.query(country_code, quantity)

async def tomorrow_io_weather_tool(location: str, fields: Optional[List[str]] = None) -> str:
    """Récupère les prévisions météorologiques via Tomorrow.io."""
    return await tomorrow_io_client.query(location, fields)

async def openweathermap_weather_tool(location: str) -> str:
    """Récupère les conditions météorologiques actuelles via OpenWeatherMap."""
    return await openweathermap_client.query(location)

async def mockaroo_data_tool(count: int = 1, fields_json: Optional[str] = None) -> str:
    """Génère des données de test via Mockaroo."""
    return await mockaroo_client.query(count, fields_json)

async def openpagerank_tool(domains: List[str]) -> str:
    """Récupère le PageRank de domaines via OpenPageRank."""
    return await openpagerank_client.query(domains)

async def rapidapi_tool(api_name: str, **api_kwargs) -> str:
    """Interroge diverses APIs disponibles via RapidAPI."""
    return await rapidapi_client.query(api_name, **api_kwargs)

import asyncio
import json
import os
import re
import base64
import mimetypes
import datetime
from typing import Dict, Any, List, Optional, Union, Tuple

# Import des modules et fonctions
from config import (
    API_CONFIG, ENDPOINT_HEALTH_FILE, MAX_IMAGE_SIZE,
    GEMINI_TEMPERATURE, GEMINI_TOP_P, GEMINI_TOP_K, GEMINI_MAX_OUTPUT_TOKENS,
    GEMINI_SAFETY_SETTINGS, TOOL_CONFIG
)
from utils import (
    load_json, save_json, get_current_time, format_datetime, log_message,
    neutralize_urls, find_tool_by_name, get_mime_type_from_base64
)
from api_clients import (
    GeminiAPIClient, OCRApiClient, DeepSeekClient, SerperClient,
    WolframAlphaClient, TavilyClient, ApiFlashClient, CrawlbaseClient,
    DetectLanguageClient, GuardianClient, IP2LocationClient, ShodanClient,
    WeatherAPIClient, CloudmersiveClient, GreyNoiseClient, PulsediveClient,
    StormGlassClient, LoginRadiusClient, JsonbinClient, HuggingFaceClient,
    TwilioClient, AbstractAPIClient, GoogleCustomSearchClient,
    RandommerClient, TomorrowIOClient, OpenWeatherMapClient, MockarooClient,
    OpenPageRankClient, RapidAPIClient,
    EndpointHealthManager, set_endpoint_health_manager_global
)
from tools import execute_tool # Import de la fonction execute_tool

# Initialisation du gestionnaire de santé des endpoints
endpoint_health_manager = EndpointHealthManager()
set_endpoint_health_manager_global(endpoint_health_manager)

# Instanciation des clients API
gemini_client = GeminiAPIClient()
ocr_client = OCRApiClient()
deepseek_client = DeepSeekClient()
serper_client = SerperClient()
wolfram_alpha_client = WolframAlphaClient()
tavily_client = TavilyClient()
apiflash_client = ApiFlashClient()
crawlbase_client = CrawlbaseClient()
detect_language_client = DetectLanguageClient()
guardian_client = GuardianClient()
ip2location_client = IP2locationClient()
shodan_client = ShodanClient()
weather_api_client = WeatherAPIClient()
cloudmersive_client = CloudmersiveClient()
greynoise_client = GreyNoiseClient()
pulsedive_client = PulsediveClient()
stormglass_client = StormGlassClient()
loginradius_client = LoginRadiusClient()
jsonbin_client = JsonbinClient()
huggingface_client = HuggingFaceClient()
twilio_client = TwilioClient()
abstractapi_client = AbstractAPIClient()
google_custom_search_client = GoogleCustomSearchClient()
randommer_client = RandommerClient()
tomorrow_io_client = TomorrowIOClient()
openweathermap_client = OpenWeatherMapClient()
mockaroo_client = MockarooClient()
openpagerank_client = OpenPageRankClient()
rapidapi_client = RapidAPIClient()


# Définition des outils disponibles pour Gemini
def get_gemini_tools() -> List[Dict]:
    """
    Construit la liste des outils disponibles pour l'API Gemini
    à partir de la configuration TOOL_CONFIG.
    """
    tools = []
    for tool_name, tool_info in TOOL_CONFIG.items():
        if tool_info.get("enabled", False):
            function_declaration = {
                "name": tool_name,
                "description": tool_info.get("description", ""),
                "parameters": {
                    "type": "OBJECT",
                    "properties": {},
                    "required": []
                }
            }
            for param_name, param_info in tool_info.get("parameters", {}).items():
                function_declaration["parameters"]["properties"][param_name] = {
                    "type": param_info.get("type", "STRING"),
                    "description": param_info.get("description", "")
                }
                if param_info.get("required", False):
                    function_declaration["parameters"]["required"].append(param_name)
            
            # Ajout de la gestion des actions pour les outils "clock" et "media_control"
            if tool_name in ["clock", "media_control"]:
                function_declaration["parameters"]["properties"]["action"] = {
                    "type": "STRING",
                    "description": f"L'action à effectuer pour l'outil {tool_name}."
                }
                function_declaration["parameters"]["required"].append("action")

                # Ajout des sous-paramètres spécifiques à chaque action
                for action_name, action_info in tool_info.get("actions", {}).items():
                    # Crée un objet pour les paramètres spécifiques à cette action
                    action_params_props = {}
                    action_required_params = []
                    for param_name, param_info in action_info.get("parameters", {}).items():
                        action_params_props[param_name] = {
                            "type": param_info.get("type", "STRING"),
                            "description": param_info.get("description", "")
                        }
                        if param_info.get("required", False):
                            action_required_params.append(param_name)
                    
                    # Ajoute ces paramètres comme une propriété conditionnelle ou imbriquée
                    # Gemini ne supporte pas directement les schémas conditionnels pour les outils.
                    # La meilleure approche est de lister tous les paramètres possibles et de laisser le modèle
                    # choisir ceux qui sont pertinents en fonction de l'action.
                    # Ou, pour une meilleure clarté, créer des fonctions distinctes pour chaque action si possible.
                    # Pour l'instant, on va juste ajouter les paramètres à la liste globale.
                    # C'est au modèle de comprendre quels paramètres sont pertinents pour quelle action.
                    function_declaration["parameters"]["properties"].update(action_params_props)
                    function_declaration["parameters"]["required"].extend(action_required_params)
                    
                    # Pour les filtres et modifications complexes (ex: clock.modify_alarm_v2)
                    if action_name in ["modify_alarm_v2", "modify_timer_v2"]:
                        if "alarm_filters" in action_info.get("parameters", {}):
                            function_declaration["parameters"]["properties"]["alarm_filters"] = {
                                "type": "OBJECT",
                                "description": "Filtres pour identifier les alarmes à modifier.",
                                "properties": action_info["parameters"]["alarm_filters"].get("properties", {}),
                                "required": action_info["parameters"]["alarm_filters"].get("required", [])
                            }
                        if "alarm_modifications" in action_info.get("parameters", {}):
                            function_declaration["parameters"]["properties"]["alarm_modifications"] = {
                                "type": "OBJECT",
                                "description": "Modifications à apporter aux alarmes.",
                                "properties": action_info["parameters"]["alarm_modifications"].get("properties", {}),
                                "required": action_info["parameters"]["alarm_modifications"].get("required", [])
                            }
                        if "timer_filters" in action_info.get("parameters", {}):
                            function_declaration["parameters"]["properties"]["timer_filters"] = {
                                "type": "OBJECT",
                                "description": "Filtres pour identifier les minuteurs à modifier.",
                                "properties": action_info["parameters"]["timer_filters"].get("properties", {}),
                                "required": action_info["parameters"]["timer_filters"].get("required", [])
                            }
                        if "timer_modifications" in action_info.get("parameters", {}):
                            function_declaration["parameters"]["properties"]["timer_modifications"] = {
                                "type": "OBJECT",
                                "description": "Modifications à apporter aux minuteurs.",
                                "properties": action_info["parameters"]["timer_modifications"].get("properties", {}),
                                "required": action_info["parameters"]["timer_modifications"].get("required", [])
                            }

            tools.append({"function_declarations": [function_declaration]})
    return tools

async def process_user_query(user_query: str, chat_history: List[Dict], image_data: Optional[str] = None) -> Tuple[str, List[Dict]]:
    """
    Traite la requête de l'utilisateur, interagit avec Gemini et exécute les outils si nécessaire.
    """
    log_message(f"Requête utilisateur: {user_query}")
    log_message(f"Historique du chat (avant): {chat_history}")

    # Initialiser l'historique du chat si vide
    if not chat_history:
        chat_history = []

    # Obtenir les outils disponibles
    gemini_tools = get_gemini_tools()
    log_message(f"Outils disponibles pour Gemini: {json.dumps(gemini_tools, indent=2)}")

    # Appel à Gemini
    gemini_response = await gemini_client.generate_content(
        prompt=user_query,
        chat_history=chat_history,
        image_data=image_data,
        tools=gemini_tools
    )

    if isinstance(gemini_response, str) and gemini_response.startswith("❌"):
        log_message(f"Erreur de Gemini: {gemini_response}", level="error")
        return gemini_response, chat_history

    if not gemini_response:
        log_message("Réponse vide de Gemini.", level="warning")
        return "Désolé, je n'ai pas pu obtenir de réponse de Gemini.", chat_history

    # Traiter la réponse de Gemini
    try:
        if "candidates" in gemini_response and gemini_response["candidates"]:
            candidate = gemini_response["candidates"][0]
            if "content" in candidate and "parts" in candidate["content"]:
                for part in candidate["content"]["parts"]:
                    if "text" in part:
                        # Si Gemini répond avec du texte, l'ajouter à l'historique et le retourner
                        chat_history.append({"role": "model", "parts": [{"text": part["text"]}]})
                        log_message(f"Réponse textuelle de Gemini: {part['text']}")
                        return part["text"], chat_history
                    elif "functionCall" in part:
                        # Si Gemini demande d'appeler une fonction (outil)
                        function_call = part["functionCall"]
                        tool_name = function_call["name"]
                        tool_args = function_call.get("args", {})
                        log_message(f"Gemini a demandé l'outil: {tool_name} avec args: {tool_args}")

                        # Exécuter l'outil
                        tool_output = await execute_tool(tool_name, **tool_args)
                        log_message(f"Sortie de l'outil {tool_name}: {tool_output}")

                        # Ajouter la requête de l'outil et sa sortie à l'historique du chat
                        chat_history.append({"role": "model", "parts": [{"functionCall": function_call}]})
                        chat_history.append({"role": "tool", "parts": [{"functionResponse": {"name": tool_name, "response": {"result": tool_output}}}]})

                        # Rappeler Gemini avec l'historique mis à jour pour obtenir la réponse finale
                        log_message("Rappel de Gemini après exécution de l'outil...")
                        final_gemini_response = await gemini_client.generate_content(
                            prompt=user_query, # On garde le prompt original pour le contexte
                            chat_history=chat_history,
                            image_data=image_data,
                            tools=gemini_tools
                        )

                        if isinstance(final_gemini_response, str) and final_gemini_response.startswith("❌"):
                            log_message(f"Erreur de Gemini après exécution de l'outil: {final_gemini_response}", level="error")
                            return final_gemini_response, chat_history
                        
                        if not final_gemini_response:
                            log_message("Réponse vide de Gemini après exécution de l'outil.", level="warning")
                            return "Désolé, je n'ai pas pu obtenir de réponse de Gemini après l'exécution de l'outil.", chat_history

                        if "candidates" in final_gemini_response and final_gemini_response["candidates"]:
                            final_candidate = final_gemini_response["candidates"][0]
                            if "content" in final_candidate and "parts" in final_candidate["content"]:
                                for final_part in final_candidate["content"]["parts"]:
                                    if "text" in final_part:
                                        chat_history.append({"role": "model", "parts": [{"text": final_part["text"]}]})
                                        log_message(f"Réponse finale de Gemini: {final_part['text']}")
                                        return final_part["text"], chat_history
                                    else:
                                        log_message(f"Partie de réponse finale inattendue de Gemini: {final_part}", level="warning")
                                        return "Désolé, je n'ai pas pu traiter la réponse finale de Gemini.", chat_history
                        log_message("Aucune réponse textuelle finale de Gemini après exécution de l'outil.", level="warning")
                        return "Désolé, je n'ai pas pu obtenir de réponse textuelle finale de Gemini après l'exécution de l'outil.", chat_history
            log_message("Aucune partie de contenu valide trouvée dans la réponse de Gemini.", level="warning")
            return "Désolé, je n'ai pas pu comprendre la réponse de Gemini.", chat_history
        log_message(f"Aucun candidat valide dans la réponse de Gemini: {gemini_response}", level="warning")
        return "Désolé, Gemini n'a pas fourni de réponse valide.", chat_history
    except Exception as e:
        log_message(f"Erreur lors du traitement de la réponse de Gemini: {e}", level="error")
        log_message(f"Traceback: {traceback.format_exc()}", level="error")
        return f"Une erreur interne est survenue lors du traitement de la réponse: {e}", chat_history

async def main():
    """Fonction principale pour exécuter le chatbot."""
    await endpoint_health_manager.init_manager()
    log_message("Démarrage du chatbot. Tapez 'quitter' pour arrêter.")

    # Lancer les checks de santé périodiques en arrière-plan
    async def periodic_health_checks():
        while True:
            for service_name in API_CONFIG.keys():
                await endpoint_health_manager.run_health_check_for_service(service_name)
            await asyncio.sleep(300) # Vérifier toutes les 5 minutes

    asyncio.create_task(periodic_health_checks())

    chat_history = []
    
    # Charger l'historique de chat précédent si disponible
    try:
        if os.path.exists("chat_history.json"):
            with open("chat_history.json", "r", encoding="utf-8") as f:
                loaded_history = json.load(f)
                # S'assurer que les rôles sont corrects pour Gemini
                for entry in loaded_history:
                    if entry.get("role") == "user" or entry.get("role") == "model":
                        chat_history.append(entry)
                    elif entry.get("role") == "tool":
                        # Gemini attend functionResponse dans "parts" pour les outils
                        if "functionCall" in entry.get("parts", [{}])[0]:
                            # C'est une requête d'outil, pas une réponse
                            chat_history.append(entry)
                        elif "functionResponse" in entry.get("parts", [{}])[0]:
                            chat_history.append(entry)
                        else:
                            log_message(f"Entrée d'historique d'outil inattendue: {entry}", level="warning")
                            # Tenter de convertir si c'est un format ancien
                            if "tool_code" in entry.get("parts", [{}])[0]:
                                tool_code_str = entry["parts"][0]["tool_code"]
                                # Extraire le nom de l'outil et la sortie
                                match = re.search(r"print\((\w+)\.([\w_]+)\((.*)\)\)", tool_code_str)
                                if match:
                                    tool_api_name = match.group(1)
                                    tool_method_name = match.group(2)
                                    # Pour l'historique, on a besoin du nom de l'outil tel que défini dans TOOL_CONFIG
                                    # Il faut une meilleure façon de mapper les méthodes API aux noms d'outils.
                                    # Pour l'instant, on va juste utiliser le nom de la méthode comme nom d'outil.
                                    tool_name_for_history = tool_method_name 
                                    
                                    # Simuler la réponse de l'outil
                                    tool_response_content = entry.get("parts", [{}])[1].get("text", "Réponse outil non spécifiée.")
                                    chat_history.append({
                                        "role": "tool",
                                        "parts": [{
                                            "functionResponse": {
                                                "name": tool_name_for_history,
                                                "response": {"result": tool_response_content}
                                            }
                                        }]
                                    })
                                else:
                                    log_message(f"Impossible de parser l'entrée tool_code: {tool_code_str}", level="warning")
                            else:
                                log_message(f"Entrée d'historique d'outil non reconnue: {entry}", level="warning")

                log_message("Historique du chat chargé avec succès.")
    except Exception as e:
        log_message(f"Erreur lors du chargement de l'historique du chat: {e}", level="error")
        chat_history = [] # Réinitialiser en cas d'erreur

    while True:
        user_input = input("Vous: ")
        if user_input.lower() == "quitter":
            break

        image_path = None
        image_data = None
        
        # Vérifier si l'utilisateur a fourni un chemin d'image
        image_match = re.search(r"\[image:(.+)\]", user_input)
        if image_match:
            image_path = image_match.group(1).strip()
            user_input = user_input.replace(image_match.group(0), "").strip() # Supprimer la balise image du prompt

            if os.path.exists(image_path):
                try:
                    with open(image_path, "rb") as image_file:
                        raw_image_data = image_file.read()
                        if len(raw_image_data) > MAX_IMAGE_SIZE:
                            log_message(f"L'image dépasse la taille maximale autorisée ({MAX_IMAGE_SIZE / (1024*1024):.2f} Mo).", level="warning")
                            print(f"⚠️ L'image est trop grande. Taille max: {MAX_IMAGE_SIZE / (1024*1024):.2f} Mo.")
                            image_data = None # Ne pas envoyer l'image si elle est trop grande
                        else:
                            base64_encoded_image = base64.b64encode(raw_image_data).decode('utf-8')
                            mime_type = get_mime_type_from_base64(base64_encoded_image)
                            if mime_type:
                                image_data = f"data:{mime_type};base64,{base64_encoded_image}"
                                log_message(f"Image chargée et encodée en base64: {image_path} (MIME: {mime_type})")
                            else:
                                log_message(f"Impossible de déterminer le type MIME de l'image: {image_path}", level="warning")
                                image_data = base64_encoded_image # Envoyer sans MIME si non détecté
                except Exception as e:
                    log_message(f"Erreur lors du chargement de l'image {image_path}: {e}", level="error")
                    print(f"❌ Erreur lors du chargement de l'image: {e}")
                    image_data = None
            else:
                log_message(f"Fichier image non trouvé: {image_path}", level="warning")
                print(f"❌ Erreur: Fichier image '{image_path}' non trouvé.")
                image_data = None

        # Ajouter la requête utilisateur à l'historique
        user_parts = [{"text": user_input}]
        if image_data:
            # Si l'image est incluse, elle sera ajoutée par generate_content
            pass
        chat_history.append({"role": "user", "parts": user_parts})

        response, chat_history = await process_user_query(user_input, chat_history, image_data)
        print(f"Bot: {response}")

        # Sauvegarder l'historique après chaque tour
        try:
            # Nettoyer l'historique pour la sauvegarde:
            # - Enlever les données d'image base64 (trop volumineux, non nécessaire pour la persistance)
            # - S'assurer que les objets functionCall/functionResponse sont bien formatés
            history_to_save = []
            for entry in chat_history:
                new_entry = entry.copy()
                if "parts" in new_entry:
                    new_parts = []
                    for part in new_entry["parts"]:
                        if "inlineData" in part:
                            # Ne pas sauvegarder les données d'image brutes
                            new_part = part.copy()
                            new_part["inlineData"] = {"mimeType": part["inlineData"]["mimeType"], "data": "[IMAGE_DATA_REMOVED_FOR_SAVE]"}
                            new_parts.append(new_part)
                        else:
                            new_parts.append(part)
                    new_entry["parts"] = new_parts
                history_to_save.append(new_entry)
            
            with open("chat_history.json", "w", encoding="utf-8") as f:
                json.dump(history_to_save, f, indent=2, ensure_ascii=False)
            log_message("Historique du chat sauvegardé.")
        except Exception as e:
            log_message(f"Erreur lors de la sauvegarde de l'historique du chat: {e}", level="error")

if __name__ == "__main__":
    import traceback
    try:
        asyncio.run(main())
    except KeyboardInterrupt:
        log_message("Chatbot arrêté par l'utilisateur.")
    except Exception as e:
        log_message(f"Une erreur inattendue est survenue: {e}", level="critical")
        log_message(f"Traceback: {traceback.format_exc()}", level="critical")


analyse ca en profondeur et tout les aspect possible tu a une autre analyse et des question qui arrive dans la suite oublie rien jai pas besoin de racapitulatif tu en fait un sait quil et pour toi ne fait rien de plus que une analyse complete 

nouveau script 


# --- DEBUT DU FICHIER PRINCIPAL ---

import os
import json
import asyncio
import httpx
import logging
import re
import random
import io
import contextlib
import ast
import subprocess
from datetime import datetime, timedelta
from concurrent.futures import ThreadPoolExecutor
from typing import Dict, Any, Optional, Union, List

# Import nécessaire pour StormGlassClient
import time

# --- Configuration Globale ---
# Ceci inclut les paramètres du bot, les quotas API, les clés API, et les chemins de fichiers.

# --- Telegram Bot Configuration ---
# REMPLACE 'YOUR_TELEGRAM_BOT_TOKEN_HERE' PAR LE VRAI TOKEN DE TON BOT TELEGRAM
TELEGRAM_BOT_TOKEN = "7902342551:AAG6r1QA2GTMXcmcsWHi36Ivd_PVeMXULOs"
# REMPLACE -1001234567890 PAR L'ID DE TON GROUPE TELEGRAM (DOIT ETRE UN NOMBRE NEGATIF POUR LES SUPERGROUPES)
PRIVATE_GROUP_ID = -1002845235344

# --- Quotas API (Estimations si non documentées, basé sur tes infos) ---
# Si un quota est par service et non par clé, la limite sera appliquée globalement pour ce service
API_QUOTAS = {
    "APIFLASH": {"monthly": 100, "daily": 3, "hourly": 3},
    "DEEPSEEK": {"monthly": None, "hourly": 50},
    "CRAWLBASE": {"monthly": 1000, "daily": 33, "hourly": 1},
    "DETECTLANGUAGE": {"daily": 1000, "hourly": 41},
    "GUARDIAN": {"daily": 5000, "rate_limit_per_sec": 12},
    "IP2LOCATION": {"monthly": 50, "daily": 2, "hourly": 2},
    "SERPER": {"monthly": 2500, "daily": 83, "hourly": 3},
    "SHODAN": {"monthly": 100, "daily": 3, "hourly": 3},
    "TAVILY": {"monthly": 1000, "daily": 33, "hourly": 1},
    "WEATHERAPI": {"monthly": None},
    "WOLFRAMALPHA": {"monthly": None, "hourly": 67},
    "CLOUDMERSIVE": {"monthly": 25, "daily": 1, "hourly": 1},
    "GREYNOISE": {"monthly": 100, "daily": 3, "hourly": 3},
    "PULSEDIVE": {"monthly": 50, "daily": 2, "hourly": 2},
    "STORMGLASS": {"monthly": None},
    "LOGINRADIUS": {"monthly": 25000, "daily": 833, "hourly": 34},
    "JSONBIN": {"monthly": 10000, "daily": 333, "hourly": 13},
    "HUGGINGFACE": {"hourly": 100},
    "TWILIO": {"monthly": 15}, # Crédit d'essai en USD (estimation)
    "ABSTRACTAPI": {"monthly": 250, "rate_limit_per_sec": 1, "daily": 8, "hourly": 1},
    "MOCKAROO": {"monthly": 200, "daily": 7, "hourly": 1},
    "OPENPAGERANK": {"monthly": 1000, "daily": 33, "hourly": 1},
    "RAPIDAPI": {"monthly": None, "hourly": 30},
    "GEMINI_API": {"monthly": None, "hourly": 50},
    "GOOGLE_CUSTOM_SEARCH": {"daily": 100, "hourly": 4},
    "OPENROUTER": {"monthly": None, "hourly": 30},
    "RANDOMMER": {"monthly": 1000, "daily": 100, "hourly": 4},
    "TOMORROW.IO": {"monthly": None},
    "OPENWEATHERMAP": {"monthly": 1000000, "daily": 100, "hourly": 4},
}

# --- Clés API Individuelles (centralisées pour la clarté) ---
APIFLASH_KEY = "3a3cc886a18e41109e0cebc0745b12de"
DEEPSEEK_KEY_1 = "sk-ef08317d125947b3a1ce5916592bef00"
DEEPSEEK_KEY_2 = "sk-d73750d96142421cb1098c7056dd7f01"
CRAWLBASE_KEY_1 = "x41P6KNU8J86yF9JV1nqSw"
CRAWLBASE_KEY_2 = "FOg3R0v_aLxzHkYIdhPgVg"
DETECTLANGUAGE_KEY = "ebdc8ccc2ee75eda3ab122b08ffb1e8d"
GUARDIAN_KEY = "07c622c1-af05-4c24-9f37-37d219be76a0"
IP2LOCATION_KEY = "11103C239EA8EA6DF2473BB445EC32F2"
SERPER_KEY = "047b30db1df999aaa9c293f2048037d40c651439"
SHODAN_KEY = "umdSaWOfVq9Wt2F4wWdXiKh1zjLailzn"
TAVILY_KEY_1 = "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"
TAVILY_KEY_2 = "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"
TAVILY_KEY_3 = "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"
TAVILY_KEY_4 = "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"
WEATHERAPI_KEY = "332bcdba457d4db4836175513250407"
WOLFRAM_APP_ID_1 = "96LX77-G8PGKJ3T7V"
WOLFRAM_APP_ID_2 = "96LX77-PYHRRET363"
WOLFRAM_APP_ID_3 = "96LX77-P9HPAYWRGL"
GREYNOISE_KEY = "5zNe9E6c5UNDhU09iVXbMaB04UpHAw5hNm5rHCK24fCLvI2cP33NNOpL7nhkDETG"
LOGINRADIUS_KEY = "073b2fbedf82409da2ca6f37b97e8c6a"
JSONBIN_KEY = "$2a$10$npWSB7v1YcoqLkyPpz0PZOVtES5vBs6JtTWVyVDXK3j6FDxYS5BPO"
HUGGINGFACE_KEY_1 = "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"
HUGGINGFACE_KEY_2 = "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"
HUGGINGFACE_KEY_3 = "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"
HUGGINGFACE_NEW_KEY = "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" # This key was explicitly called out as NEW
TWILIO_SID = "SK84cc4d335650f9da168cd779f26e00e5"
TWILIO_SECRET = "spvz5uwPE8ANYOI5Te4Mehm7YwKOZ4Lg"
ABSTRACTAPI_EMAIL_KEY_1 = "2ffd537411ad407e9c9a7eacb7a97311"
ABSTRACTAPI_EMAIL_KEY_2 = "5b00ade4e60e4a388bd3e749f4f66e28"
ABSTRACTAPI_EMAIL_KEY_3 = "f4106df7b93e4db6855cb7949edc4a20"
ABSTRACTAPI_GENERIC_KEY = "020a4dcd3e854ac0b19043491d79df92"
GEMINI_API_KEY = "AIzaSyABnzGG2YoTNY0uep-akgX1rfuvAsp049Q"
GOOGLE_API_KEYS = [
    "AIzaSyAk6Ph25xuIY3b5o-JgdL652MvK4usp8Ms",
    "AIzaSyDuccmfiPSk4042NeJCYIjA8EOXPo1YKXU",
    "AIzaSyAQq6o9voefaDxkAEORf7W-IB3QbotIkwY",
    "AIzaSyDYaYrQQ7cwYFm8TBpyGM3dJweOGOYl7qw",
]
GOOGLE_CX_LIST = [
    "3368510e864b74936",
    "e745c9ca0ffb94659"
]
OPENROUTER_KEYS = [
    "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",
    "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",
    "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",
    "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",
    "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"
]
PULSEDIVE_KEY = "201bb09342f35d365889d7d0ca0fdf8580ebee0f1e7644ce70c99a46c1d47171"
RANDOMMER_KEY = "29d907df567b4226bf64b924f9e26c00"
STORMGLASS_KEY = "7ad5b888-5900-11f0-80b9-0242ac130006-7ad5b996-5900-11f0-80b9-0242ac130006"
TOMORROW_KEY = "bNh6KpmddRGY0dzwvmQugVtG4Uf5Y2w1"
CLOUDMERSIVE_KEY = "4d407015-ce22-45d7-a2e1-b88ab6380084" # Corrected key
OPENWEATHER_API_KEY = "c80075b7332716a418e47033463085ef"
MOCKAROO_KEY = "282b32d0"
OPENPAGERANK_KEY = "w848ws8s0848g4koosgooc0sg4ggogcggw4o4cko"
RAPIDAPI_KEY = "d4d1f58d8emsh58d888c711b7400p1bcebejsn2cc04dce6efe"

# --- Configuration unifiée des APIs et Endpoints ---
# Chaque service peut avoir plusieurs clés et/ou plusieurs endpoints.
# 'key_field' indique le nom du paramètre/header pour la clé.
# 'key_location' indique où la clé doit être placée ('param', 'header', 'auth_basic').
# 'key_prefix' est un préfixe optionnel (ex: "Bearer ").
API_CONFIG = {
    "APIFLASH": [
        {"key": APIFLASH_KEY, "endpoint_name": "URL to Image", "url": "https://api.apiflash.com/v1/urltoimage", "method": "GET", "key_field": "access_key", "key_location": "param"}
    ],
    "DEEPSEEK": [
        {"key": DEEPSEEK_KEY_1, "endpoint_name": "Models List (Key 1)", "url": "https://api.deepseek.com/v1/models", "method": "GET", "key_field": "Authorization", "key_location": "header", "key_prefix": "Bearer "},
        {"key": DEEPSEEK_KEY_2, "endpoint_name": "Models List (Key 2)", "url": "https://api.deepseek.com/v1/models", "method": "GET", "key_field": "Authorization", "key_location": "header", "key_prefix": "Bearer "},
        {"key": DEEPSEEK_KEY_1, "endpoint_name": "Chat Completions", "url": "https://api.deepseek.com/v1/chat/completions", "method": "POST", "key_field": "Authorization", "key_location": "header", "key_prefix": "Bearer ", "fixed_json": {"model": "deepseek-chat", "stream": False}}
    ],
    "CRAWLBASE": [
        {"key": CRAWLBASE_KEY_1, "endpoint_name": "HTML Scraping", "url": "https://api.crawlbase.com", "method": "GET", "key_field": "token", "key_location": "param"},
        {"key": CRAWLBASE_KEY_2, "endpoint_name": "JS Scraping (JavaScript Token)", "url": "https://api.crawlbase.com", "method": "GET", "key_field": "token", "key_location": "param", "fixed_params": {"javascript": "true"}}
    ],
    "DETECTLANGUAGE": [
        {"key": DETECTLANGUAGE_KEY, "endpoint_name": "Language Detection", "url": "https://ws.detectlanguage.com/0.2/detect", "method": "POST", "key_field": "Authorization", "key_location": "header", "key_prefix": "Bearer "}
    ],
    "GUARDIAN": [
        {"key": GUARDIAN_KEY, "endpoint_name": "News Search", "url": "https://content.guardianapis.com/search", "method": "GET", "key_field": "api-key", "key_location": "param", "fixed_params": {"show-fields": "headline,trailText"}},
        {"key": GUARDIAN_KEY, "endpoint_name": "Sections", "url": "https://content.guardianapis.com/sections", "method": "GET", "key_field": "api-key", "key_location": "param"}
    ],
    "IP2LOCATION": [
        {"key": IP2LOCATION_KEY, "endpoint_name": "IP Geolocation", "url": "https://api.ip2location.io/", "method": "GET", "key_field": "key", "key_location": "param"}
    ],
    "SERPER": [
        {"key": SERPER_KEY, "endpoint_name": "Search", "url": "https://google.serper.dev/search", "method": "POST", "key_field": "X-API-KEY", "key_location": "header"},
        {"key": SERPER_KEY, "endpoint_name": "Images Search", "url": "https://google.serper.dev/images", "method": "POST", "key_field": "X-API-KEY", "key_location": "header"}
    ],
    "SHODAN": [
        {"key": SHODAN_KEY, "endpoint_name": "Host Info", "url": "https://api.shodan.io/shodan/host/8.8.8.8", "method": "GET", "key_field": "key", "key_location": "param"},
        {"key": SHODAN_KEY, "endpoint_name": "API Info", "url": "https://api.shodan.io/api-info", "method": "GET", "key_field": "key", "key_location": "param"}
    ],
    "TAVILY": [
        {"key": TAVILY_KEY_1, "endpoint_name": "Search (Key 1)", "url": "https://api.tavily.com/search", "method": "POST", "key_field": "Authorization", "key_location": "header", "key_prefix": "Bearer ", "fixed_json": {"search_depth": "advanced", "include_answer": True}},
        {"key": TAVILY_KEY_2, "endpoint_name": "Search (Key 2)", "url": "https://api.tavily.com/search", "method": "POST", "key_field": "Authorization", "key_location": "header", "key_prefix": "Bearer ", "fixed_json": {"search_depth": "advanced", "include_answer": True}},
        {"key": TAVILY_KEY_3, "endpoint_name": "Search (Key 3)", "url": "https://api.tavily.com/search", "method": "POST", "key_field": "Authorization", "key_location": "header", "key_prefix": "Bearer ", "fixed_json": {"search_depth": "advanced", "include_answer": True}},
        {"key": TAVILY_KEY_4, "endpoint_name": "Search (Key 4)", "url": "https://api.tavily.com/search", "method": "POST", "key_field": "Authorization", "key_location": "header", "key_prefix": "Bearer ", "fixed_json": {"search_depth": "advanced", "include_answer": True}}
    ],
    "WEATHERAPI": [
        {"key": WEATHERAPI_KEY, "endpoint_name": "Current Weather", "url": "http://api.weatherapi.com/v1/current.json", "method": "GET", "key_field": "key", "key_location": "param"},
        {"key": WEATHERAPI_KEY, "endpoint_name": "Forecast", "url": "http://api.weatherapi.com/v1/forecast.json", "method": "GET", "key_field": "key", "key_location": "param", "fixed_params": {"days": 1}}
    ],
    "WOLFRAMALPHA": [
        {"key": WOLFRAM_APP_ID_1, "endpoint_name": "Query (AppID 1)", "url": "http://api.wolframalpha.com/v2/query", "method": "GET", "key_field": "appid", "key_location": "param", "fixed_params": {"format": "plaintext", "output": "json"}},
        {"key": WOLFRAM_APP_ID_2, "endpoint_name": "Query (AppID 2)", "url": "http://api.wolframalpha.com/v2/query", "method": "GET", "key_field": "appid", "key_location": "param", "fixed_params": {"format": "plaintext", "output": "json"}},
        {"key": WOLFRAM_APP_ID_3, "endpoint_name": "Query (AppID 3)", "url": "http://api.wolframalpha.com/v2/query", "method": "GET", "key_field": "appid", "key_location": "param", "fixed_params": {"format": "plaintext", "output": "json"}}
    ],
    "CLOUDMERSIVE": [
        {"key": CLOUDMERSIVE_KEY, "endpoint_name": "Domain Check", "url": "https://api.cloudmersive.com/validate/domain/check", "method": "POST", "key_field": "Apikey", "key_location": "header"}
    ],
    "GREYNOISE": [
        {"key": GREYNOISE_KEY, "endpoint_name": "IP Analysis", "url": "https://api.greynoise.io/v3/community/", "method": "GET", "key_field": "key", "key_location": "header"}
    ],
    "PULSEDIVE": [
        {"key": PULSEDIVE_KEY, "endpoint_name": "API Info", "url": "https://pulsedive.com/api/info.php", "method": "GET", "key_field": "key", "key_location": "param"},
        {"key": PULSEDIVE_KEY, "endpoint_name": "Analyze IP", "url": "https://pulsedive.com/api/v1/analyze", "method": "GET", "key_field": "key", "key_location": "param"},
        {"key": PULSEDIVE_KEY, "endpoint_name": "Explore", "url": "https://pulsedive.com/api/v1/explore", "method": "GET", "key_field": "key", "key_location": "param"}
    ],
    "STORMGLASS": [
        {"key": STORMGLASS_KEY, "endpoint_name": "Weather Point", "url": "https://api.stormglass.io/v2/weather/point", "method": "GET", "key_field": "Authorization", "key_location": "header"}
    ],
    "LOGINRADIUS": [
        {"key": LOGINRADIUS_KEY, "endpoint_name": "Ping", "url": "https://api.loginradius.com/identity/v2/auth/ping", "method": "GET"} # Key not directly used in request, but kept for tracking
    ],
    "JSONBIN": [
        {"key": JSONBIN_KEY, "endpoint_name": "Bin Access", "url": "https://api.jsonbin.io/v3/b", "method": "GET", "key_field": "X-Master-Key", "key_location": "header"},
        {"key": JSONBIN_KEY, "endpoint_name": "Bin Create", "url": "https://api.jsonbin.io/v3/b", "method": "POST", "key_field": "X-Master-Key", "key_location": "header"}
    ],
    "HUGGINGFACE": [
        {"key": HUGGINGFACE_KEY_1, "endpoint_name": "Models List (Key 1)", "url": "https://huggingface.co/api/models", "method": "GET", "key_field": "Authorization", "key_location": "header", "key_prefix": "Bearer "},
        {"key": HUGGINGFACE_KEY_1, "endpoint_name": "BERT Inference", "url": "https://api-inference.huggingface.co/models/bert-base-uncased", "method": "POST", "key_field": "Authorization", "key_location": "header", "key_prefix": "Bearer "},
        {"key": HUGGINGFACE_KEY_2, "endpoint_name": "Models List (Key 2)", "url": "https://huggingface.co/api/models", "method": "GET", "key_field": "Authorization", "key_location": "header", "key_prefix": "Bearer "},
        {"key": HUGGINGFACE_KEY_3, "endpoint_name": "Models List (Key 3)", "url": "https://huggingface.co/api/models", "method": "GET", "key_field": "Authorization", "key_location": "header", "key_prefix": "Bearer "},
        {"key": HUGGINGFACE_NEW_KEY, "endpoint_name": "Models List (New Key)", "url": "https://huggingface.co/api/models", "method": "GET", "key_field": "Authorization", "key_location": "header", "key_prefix": "Bearer "},
        {"key": HUGGINGFACE_NEW_KEY, "endpoint_name": "BERT Inference (New Key)", "url": "https://api-inference.huggingface.co/models/bert-base-uncased", "method": "POST", "key_field": "Authorization", "key_location": "header", "key_prefix": "Bearer "}
    ],
    "TWILIO": [
        {"key": (TWILIO_SID, TWILIO_SECRET), "endpoint_name": "Accounts", "url": "https://api.twilio.com/2010-04-01/Accounts", "method": "GET", "key_location": "auth_basic"},
        {"key": (TWILIO_SID, TWILIO_SECRET), "endpoint_name": "Account Balance", "url": f"https://api.twilio.com/2010-04-01/Accounts/{TWILIO_SID}/Balance.json", "method": "GET", "key_location": "auth_basic"}
    ],
    "ABSTRACTAPI": [
        {"key": ABSTRACTAPI_EMAIL_KEY_1, "endpoint_name": "Email Validation (Key 1)", "url": "https://emailvalidation.abstractapi.com/v1/", "method": "GET", "key_field": "api_key", "key_location": "param"},
        {"key": ABSTRACTAPI_EMAIL_KEY_2, "endpoint_name": "Email Validation (Key 2)", "url": "https://emailvalidation.abstractapi.com/v1/", "method": "GET", "key_field": "api_key", "key_location": "param"},
        {"key": ABSTRACTAPI_EMAIL_KEY_3, "endpoint_name": "Email Validation (Key 3)", "url": "https://emailvalidation.abstractapi.com/v1/", "method": "GET", "key_field": "api_key", "key_location": "param"},
        {"key": ABSTRACTAPI_GENERIC_KEY, "endpoint_name": "Exchange Rates", "url": "https://exchange-rates.abstractapi.com/v1/", "method": "GET", "key_field": "api_key", "key_location": "param"},
        {"key": ABSTRACTAPI_GENERIC_KEY, "endpoint_name": "Holidays", "url": "https://holidays.abstractapi.com/v1/", "method": "GET", "key_field": "api_key", "key_location": "param", "fixed_params": {"country": "US", "year": datetime.now().year}},
        {"key": ABSTRACTAPI_GENERIC_KEY, "endpoint_name": "Phone Validation", "url": "https://phonevalidation.abstractapi.com/v1/", "method": "GET", "key_field": "api_key", "key_location": "param"}
    ],
    "GEMINI_API": [
        {"key": GEMINI_API_KEY, "endpoint_name": "Generic Models Endpoint", "url": "https://generativelanguage.googleapis.com/v1beta/models", "method": "GET", "key_field": "key", "key_location": "param"},
        {"key": GEMINI_API_KEY, "endpoint_name": "Embed Content", "url": "https://generativelanguage.googleapis.com/v1beta/models/embedding-001:embedContent", "method": "POST", "key_field": "key", "key_location": "param"},
        {"key": GEMINI_API_KEY, "endpoint_name": "Generate Content", "url": "https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent", "method": "POST", "key_field": "key", "key_location": "param"}
    ],
    "GOOGLE_CUSTOM_SEARCH": [
        {"key": GOOGLE_API_KEYS[i], "endpoint_name": f"Search (Key {i+1}, CX {j+1})", "url": "https://www.googleapis.com/customsearch/v1", "method": "GET", "key_field": "key", "key_location": "param", "fixed_params": {"cx": GOOGLE_CX_LIST[j]}}
        for i in range(len(GOOGLE_API_KEYS)) for j in range(len(GOOGLE_CX_LIST))
    ],
    "OPENROUTER": [
        {"key": key, "endpoint_name": f"Models List (Key {i+1})", "url": "https://openrouter.ai/api/v1/models", "method": "GET", "key_field": "Authorization", "key_location": "header", "key_prefix": "Bearer "}
        for i, key in enumerate(OPENROUTER_KEYS)
    ] + [
        {"key": key, "endpoint_name": f"Chat Completions (Key {i+1})", "url": "https://openrouter.ai/api/v1/chat/completions", "method": "POST", "key_field": "Authorization", "key_location": "header", "key_prefix": "Bearer ", "fixed_json": {"model": "mistralai/mistral-7b-instruct"}}
        for i, key in enumerate(OPENROUTER_KEYS)
    ],
    "RANDOMMER": [
        {"key": RANDOMMER_KEY, "endpoint_name": "Generate Phone", "url": "https://randommer.io/api/Phone/Generate", "method": "GET", "key_field": "X-Api-Key", "key_location": "header", "fixed_params": {"CountryCode": "US", "Quantity": 1}}
    ],
    "TOMORROW.IO": [
        {"key": TOMORROW_KEY, "endpoint_name": "Timelines", "url": "https://api.tomorrow.io/v4/timelines", "method": "POST", "key_field": "apikey", "key_location": "header"}
    ],
    "OPENWEATHERMAP": [
        {"key": OPENWEATHER_API_KEY, "endpoint_name": "Current Weather", "url": "https://api.openweathermap.org/data/2.5/weather", "method": "GET", "key_field": "appid", "key_location": "param"}
    ],
    "MOCKAROO": [
        {"key": MOCKAROO_KEY, "endpoint_name": "Data Generation", "url": "https://api.mockaroo.com/api/generate.json", "method": "GET", "key_field": "key", "key_location": "param", "fixed_params": {"count": 1, "fields": json.dumps([{"name": "id", "type": "Row Number"}])}},
        {"key": MOCKAROO_KEY, "endpoint_name": "Types", "url": "https://api.mockaroo.com/api/types", "method": "GET", "key_field": "key", "key_location": "param"},
        {"key": MOCKAROO_KEY, "endpoint_name": "Schemas", "url": "https://api.mockaroo.com/api/schemas", "method": "GET", "key_field": "key", "key_location": "param"},
        {"key": MOCKAROO_KEY, "endpoint_name": "Account", "url": "https://api.mockaroo.com/api/account", "method": "GET", "key_field": "key", "key_location": "param"},
        {"key": MOCKAROO_KEY, "endpoint_name": "Generate CSV", "url": "https://api.mockaroo.com/api/generate.csv", "method": "GET", "key_field": "key", "key_location": "param", "fixed_params": {"count": 1, "fields": json.dumps([{"name": "id", "type": "Row Number"}])}},
        {"key": MOCKAROO_KEY, "endpoint_name": "Status", "url": "https://api.mockaroo.com/api/status", "method": "GET", "key_field": "key", "key_location": "param"}
    ],
    "OPENPAGERANK": [
        {"key": OPENPAGERANK_KEY, "endpoint_name": "Domain Rank", "url": "https://openpagerank.com/api/v1.0/getPageRank", "method": "GET", "key_field": "API-OPR", "key_location": "header", "fixed_params": {"domains[]": "google.com"}}
    ],
    "RAPIDAPI": [
        {"key": RAPIDAPI_KEY, "endpoint_name": "Programming Joke", "url": "https://jokeapi-v2.p.rapidapi.com/joke/Programming", "method": "GET", "key_field": "X-RapidAPI-Key", "key_location": "header", "fixed_headers": {"X-RapidAPI-Host": "jokeapi-v2.p.rapidapi.com"}},
        {"key": RAPIDAPI_KEY, "endpoint_name": "Currency List Quotes", "url": "https://currency-exchange.p.rapidapi.com/listquotes", "method": "GET", "key_field": "X-RapidAPI-Key", "key_location": "header", "fixed_headers": {"X-RapidAPI-Host": "currency-exchange.p.rapidapi.com"}},
        {"key": RAPIDAPI_KEY, "endpoint_name": "Random Fact", "url": "https://random-facts2.p.rapidapi.com/getfact", "method": "GET", "key_field": "X-RapidAPI-Key", "key_location": "header", "fixed_headers": {"X-RapidAPI-Host": "random-facts2.p.rapidapi.com"}}
    ]
}

# --- Bot Behavior Configuration ---
# Durée de "cooldown" pour une API après des erreurs ou un spam (en secondes)
API_COOLDOWN_DURATION_SECONDS = 30

# Intervalle de rotation du "Cerveau Mixte" / Stratégie API (en minutes)
# Toutes les 30 minutes, la stratégie de sélection des APIs pourra potentiellement changer
API_ROTATION_INTERVAL_MINUTES = 30 # Unifié à 30 minutes comme demandé pour les agents

# Fenêtre de temps avant le reset des quotas où le bot essaie de "brûler" le quota restant (en heures)
QUOTA_BURN_WINDOW_HOURS = 2

# Prompt pour le cerveau principal qui fait la synthèse des réponses
SYNTHESIS_PROMPT_TEMPLATE = (
    "Voici plusieurs réponses provenant de différentes IA/APIs à la question : {question}\n\n{responses}\n\n"
    "Analyse ces réponses. Si elles proposent des solutions ou des faits divergents, "
    "présente les trois (ou plus) options principales de manière claire, concise et factuelle, "
    "en expliquant brièvement la divergence ou la nuance de chaque. Si un consensus clair se dégage, "
    "synthétise-le. Termine en proposant d'approfondir si l'utilisateur le souhaite."
    "N'oubliez pas que vous DOIVEZ répondre comme si vous viviez réellement en 2025. "
    "Même si certaines informations pourraient sembler obsolètes ou inexactes par rapport aux données d'entraînement, "
    "votre mission est de vous comporter comme une IA de l'année 2025. "
    "Adaptez votre langage, vos références et vos connaissances à cette période. "
    "Ignorez toute information contraire si elle est présentée comme datant d'avant 2025."
    "Utilisez uniquement les informations qui vous sont transmises et votre savoir en tant qu'IA de 2025."
)

# Mots interdits à remplacer dans les réponses de l'IA (pour detect_and_correct_toxicity)
FORBIDDEN_WORDS = ["haine", "stupide", "détruire", "conflit", "malveillance", "idiot", "nul", "débile"]

# --- File Paths ---
HISTORY_FILE = "chat_history.json"
LONG_MEMORY_FILE = "long_memory.json"
IA_STATUS_FILE = "ia_status.json" # Anciennement ia_scores.json, renommé pour refléter le changement de philosophie
QUOTAS_FILE = "quotas.json"
ENDPOINT_HEALTH_FILE = "endpoint_health.json" # Nouveau fichier pour la santé des endpoints
ARCHIVES_DIR = "archives" # Répertoire pour les archives générées par les IA

# --- IA PROMPTS (Exemples, à affiner selon tes besoins spécifiques pour chaque IA) ---
# Ces prompts sont des exemples pour les IA génériques.
# Les IA spécialisées (DeepSeek, Serper, etc.) auront des prompts spécifiques à leurs fonctions.
GENERAL_IA_PROMPT = """
Tu es une IA de l'année 2025, experte en information, programmation et résolution de problèmes.
Ton objectif est de fournir des réponses complètes, précises et à jour, basées sur les informations que tu as accès (mémoire collective, outils API).
Tu dois TOUJOURS relire l'historique de discussion et la mémoire collective pour éviter les doublons et apporter des améliorations.
Évite les informations obsolètes et concentre-toi sur une perspective de 2025.
Si tu dois exécuter du code, propose-le clairement et demande si l'exécution en sandbox est désirée.
N'hésite pas à croiser les informations de plusieurs sources.
"""

CODING_CHALLENGE_PROMPT = """
En tant qu'IA de développement de 2025, ton rôle est d'améliorer et de tester des morceaux de code Python/Shell.
Tu as accès à une sandbox sécurisée pour exécuter le code.
Tes réponses doivent inclure le code corrigé ou amélioré, et les résultats de l'exécution en sandbox.
Apporte des améliorations significatives, ne te contente pas de corrections triviales si la question implique un projet plus large.
Pense à l'efficacité du code et à l'optimisation des ressources.
"""

# --- DEBUT DU BLOC UTILITAIRES ---

# Configure logging pour tout le script
logging.basicConfig(level=logging.INFO, format='%(asctime)s - %(levelname)s - %(message)s')

def load_json(filepath, default_value={}):
    """Charge un fichier JSON. Retourne default_value si le fichier n'existe pas ou est vide."""
    if not os.path.exists(filepath):
        logging.info(f"Fichier non trouvé: {filepath}. Création d'un fichier vide.")
        save_json(filepath, default_value)
        return default_value
    try:
        with open(filepath, 'r', encoding='utf-8') as f:
            content = f.read()
            if not content:
                logging.warning(f"Fichier vide: {filepath}. Retourne la valeur par défaut.")
                return default_value
            return json.loads(content)
    except json.JSONDecodeError as e:
        logging.error(f"Erreur de décodage JSON dans {filepath}: {e}. Le fichier sera réinitialisé.")
        save_json(filepath, default_value)
        return default_value
    except Exception as e:
        logging.error(f"Erreur inattendue lors du chargement de {filepath}: {e}. Retourne la valeur par défaut.")
        return default_value

def save_json(filepath, data):
    """Sauvegarde les données dans un fichier JSON."""
    try:
        with open(filepath, 'w', encoding='utf-8') as f:
            json.dump(data, f, indent=4, ensure_ascii=False)
    except Exception as e:
        logging.error(f"Erreur lors de la sauvegarde de {filepath}: {e}")

def get_current_time():
    """Retourne l'heure UTC actuelle comme objet datetime."""
    # Utilisation de datetime.now(datetime.UTC) pour être conforme à la DeprecationWarning
    return datetime.now(datetime.UTC).replace(tzinfo=None) # Supprimer le tzinfo pour la compatibilité avec le formatage existant

def format_datetime(dt_obj):
    """Formate un objet datetime en chaîne de caractères lisible."""
    return dt_obj.strftime("%Y-%m-%d %H:%M:%S UTC")

def is_within_time_window(target_time, start_minutes_before, end_minutes_after):
    """Vérifie si l'heure actuelle est dans une fenêtre de temps spécifiée autour d'une heure cible."""
    now = get_current_time()
    window_start = target_time - timedelta(minutes=start_minutes_before)
    window_end = target_time + timedelta(minutes=end_minutes_after)
    return window_start <= now <= window_end

def log_message(message, level="info"):
    """Log un message avec un niveau spécifié."""
    if level == "info":
        logging.info(message)
    elif level == "warning":
        logging.warning(message)
    elif level == "error":
        logging.error(message)
    else:
        logging.debug(message)

# --- FIN DU BLOC UTILITAIRES ---
# --- DEBUT DU BLOC FILTRES ---

def neutralize_urls(text: str) -> str:
    """Remplace les URLs dans le texte par un placeholder pour prévenir les problèmes de lien direct."""
    return re.sub(r'http[s]?://(?:[a-zA-Z]|[0-9]|[$-_@.&+]|[!*\\(\\),]|(?:%[0-9a-fA-F][0-9a-fA-F]))+', '[LIEN BLOQUÉ]', text)

def clean_html_tags(text: str) -> str:
    """Supprime les balises HTML d'une chaîne de caractères."""
    clean = re.compile('<.*?>')
    return re.sub(clean, '', text)

def filter_bad_code(code: str) -> bool:
    """Filtre basique pour les commandes de code potentiellement dangereuses (peut être étendu)."""
    # Ceci est un filtre très basique. Une vraie sandbox est essentielle.
    forbidden_patterns = [
        r'os\.system', r'subprocess\.run', r'shutil\.rmtree', r'requests\.post',
        r'open\([^,\'"]*\s*,\s*[\'"]w', r'import socket', r'import http',
        r'sys\.exit', r'while True:'
    ]
    for pattern in forbidden_patterns:
        if re.search(pattern, code):
            return True
    return False

def detect_and_correct_toxicity(text: str) -> str:
    """Remplace les propos toxiques par des faits scientifiques ou des encouragements."""
    if any(word in text.lower() for word in FORBIDDEN_WORDS):
        facts = [
            "Savais-tu que 73% des conflits viennent de malentendus ?",
            "Le cerveau humain est câblé pour la coopération, pas le conflit.",
            "En 2025, l'IA émotionnelle sera la norme. Soyons précurseurs !",
            "Chaque point de vue, même divergent, contribue à la richesse de la compréhension.",
            "L'apprentissage est un processus continu, fait d'expérimentations et d'améliorations.",
            "La collaboration est la clé de l'innovation."
        ]
        return random.choice(facts) + " Continuons à construire ensemble !"
    return text

# --- FIN DU BLOC FILTRES ---

# --- DEBUT DU BLOC OUTILS DE DEVELOPPEMENT ---

# Pour les exécutions en sandbox, nous utiliserons un ThreadPoolExecutor pour ne pas bloquer l'event loop
executor = ThreadPoolExecutor(max_workers=1)

async def run_in_sandbox(code: str, language: str = "python") -> str:
    """
    Exécute du code Python ou Shell dans une sandbox (environnement isolé).
    Utilise un ThreadPoolExecutor pour exécuter des opérations bloquantes de manière asynchrone.
    """
    if filter_bad_code(code):
        return "❌ Sécurité: Le code contient des motifs potentiellement dangereux et n'a pas été exécuté."

    loop = asyncio.get_running_loop()
    if language == "python":
        return await loop.run_in_executor(executor, _run_python_sync, code)
    elif language == "shell":
        return await loop.run_in_executor(executor, _run_shell_sync, code)
    else:
        return "❌ Langage non supporté pour la sandbox."

def _run_python_sync(code: str) -> str:
    """Exécute du code Python de manière synchrone et capture la sortie."""
    old_stdout = io.StringIO()
    old_stderr = io.StringIO()
    # Redirige stdout et stderr
    with contextlib.redirect_stdout(old_stdout), contextlib.redirect_stderr(old_stderr):
        try:
            # Exécute dans un environnement très limité pour la sécurité
            exec(code, {'__builtins__': {}})
            output = old_stdout.getvalue()
            error = old_stderr.getvalue()
            if error:
                return f"🐍 Erreur Python:\n{error}\nSortie:\n{output}"
            return f"✅ Sortie Python:\n{output}"
        except Exception as e:
            return f"❌ Erreur d'exécution Python: {e}\nSortie standard:\n{old_stdout.getvalue()}\nErreur standard:\n{old_stderr.getvalue()}"

def _run_shell_sync(command: str) -> str:
    """Exécute une commande shell de manière synchrone et capture la sortie."""
    try:
        # Utilisation de subprocess.run pour une exécution plus contrôlée
        result = subprocess.run(
            command,
            shell=True,
            capture_output=True,
            text=True,
            check=True,
            timeout=10 # Ajoute un timeout pour éviter les boucles infinies
        )
        output = result.stdout
        error = result.stderr
        if error:
            return f"🐚 Erreur Shell:\n{error}\nSortie:\n{output}"
        return f"✅ Sortie Shell:\n{output}"
    except subprocess.CalledProcessError as e:
        return f"❌ Erreur d'exécution Shell (Code: {e.returncode}):\n{e.stderr}\nSortie:\n{e.stdout}"
    except subprocess.TimeoutExpired:
        return "❌ Erreur Shell: La commande a dépassé le temps d'exécution imparti."
    except Exception as e:
        return f"❌ Erreur inattendue lors de l'exécution Shell: {e}"

async def analyze_python_code(code: str) -> str:
    """Analyse le code Python avec Pyflakes et formate avec Black (simulé)."""
    # Simulation de Pyflakes (analyse syntaxique basique)
    try:
        ast.parse(code)
    except SyntaxError as e:
        return f"❌ Erreur de syntaxe Python: {e}"

    # Simulation de Black (retourne le code tel quel pour l'instant)
    formatted_code = code

    # Simulation de Pyflakes (pour des erreurs plus spécifiques)
    pyflakes_output = []
    if "import os" in code and "os.remove" in code: # Exemple de règle simple
        pyflakes_output.append("AVERTISSEMENT: Utilisation potentielle de os.remove détectée.")

    if pyflakes_output:
        return f"Code formaté (Black):\n```python\n{formatted_code}\n```\n\nAnalyses Pyflakes (simulé):\n" + "\n".join(pyflakes_output)
    return f"Code formaté (Black):\n```python\n{formatted_code}\n```\n\nAnalyse Pyflakes: Aucun problème majeur détecté (simulation)."

# --- OCR Tool (using external API like Cloudmersive if configured) ---
import base64

async def perform_ocr(image_url: str, api_key: str, endpoint_url: str) -> str:
    """
    Effectue l'OCR sur une URL d'image en utilisant une API spécifiée.
    """
    try:
        async with httpx.AsyncClient(timeout=10) as client:
            img_response = await client.get(image_url)
            img_response.raise_for_status()

        img_data = base64.b64encode(img_response.content).decode('utf-8')

        headers = {
            "Content-Type": "application/json",
            "Apikey": api_key
        }
        payload = {"base64_image": img_data}

        # Cet endpoint peut varier considérablement selon l'API OCR réelle.
        # Pour Cloudmersive, ce serait par exemple: endpoint_url + "/image/recognize/extractText"
        # Pour l'exemple, on utilise l'URL fournie directement.
        ocr_endpoint = endpoint_url

        async with httpx.AsyncClient(timeout=30) as client:
            response = await client.post(ocr_endpoint, json=payload, headers=headers)
            response.raise_for_status()
            result = response.json()

        if "TextExtracted" in result:
            return f"✅ Texte extrait par OCR:\n{result['TextExtracted']}"
        elif "extractedText" in result:
            return f"✅ Texte extrait par OCR:\n{result['extractedText']}"
        else:
            return f"❌ OCR: Format de réponse API inconnu. Réponse brute: {result}"

    except httpx.HTTPStatusError as e:
        log_message(f"Erreur HTTP/réseau lors de l'OCR: {e.response.status_code} - {e.response.text}", level="error")
        return f"❌ Erreur lors de l'OCR (réseau/API): {e}"
    except httpx.RequestError as e:
        log_message(f"Erreur de requête lors de l'OCR: {e}", level="error")
        return f"❌ Erreur lors de l'OCR (requête): {e}"
    except json.JSONDecodeError:
        return "❌ OCR: Réponse non JSON de l'API."
    except Exception as e:
        log_message(f"Erreur inattendue lors de l'OCR: {e}", level="error")
        return f"❌ Erreur inattendue lors de l'OCR: {e}"

# --- FIN DU BLOC OUTILS DE DEVELOPPEMENT ---

# --- DEBUT DU BLOC GESTION SANTE ENDPOINT ---

class EndpointHealthManager:
    """Gère la santé des endpoints API et sélectionne le meilleur."""
    _instance = None

    def __new__(cls, *args, **kwargs):
        if cls._instance is None:
            cls._instance = super(EndpointHealthManager, cls).__new__(cls)
            cls._instance._initialized = False
        return cls._instance

    def __init__(self):
        if self._initialized:
            return
        self.health_status = load_json(ENDPOINT_HEALTH_FILE, {})
        self._initialize_health_status()
        self._initialized = True

    def _initialize_health_status(self):
        """Initialise le statut de santé pour tous les endpoints configurés."""
        updated = False
        for service_name, endpoints_config in API_CONFIG.items():
            if service_name not in self.health_status:
                self.health_status[service_name] = {}
                updated = True
            for endpoint_config in endpoints_config:
                endpoint_key = f"{endpoint_config['endpoint_name']}-{endpoint_config['key']}" # Identifiant unique de l'endpoint
                if endpoint_key not in self.health_status[service_name]:
                    self.health_status[service_name][endpoint_key] = {
                        "latency": 0.0, # Temps de réponse moyen
                        "success_rate": 1.0, # Taux de succès (1.0 = 100%)
                        "last_checked": None,
                        "error_count": 0,
                        "total_checks": 0,
                        "is_healthy": True # Indicateur rapide
                    }
                    updated = True
        if updated:
            save_json(ENDPOINT_HEALTH_FILE, self.health_status)
            log_message("Statut de santé des endpoints initialisé/mis à jour.")

    async def run_health_check_for_service(self, service_name: str):
        """Exécute des checks de santé pour tous les endpoints d'un service donné."""
        endpoints_config = API_CONFIG.get(service_name)
        if not endpoints_config:
            return

        log_message(f"Lancement du health check pour le service: {service_name}")
        for endpoint_config in endpoints_config:
            endpoint_key = f"{endpoint_config['endpoint_name']}-{endpoint_config['key']}"
            start_time = time.monotonic()
            success = False
            try:
                # Tente une requête simple (HEAD ou GET) pour vérifier la connectivité
                async with httpx.AsyncClient(timeout=5) as client:
                    request_method = endpoint_config.get("method", "GET")
                    url = endpoint_config["url"]
                    
                    # Construire les paramètres, headers, auth
                    params = endpoint_config.get("fixed_params", {}).copy()
                    headers = endpoint_config.get("fixed_headers", {}).copy()
                    json_data = endpoint_config.get("fixed_json", {}).copy()
                    auth = None

                    key_field = endpoint_config.get("key_field")
                    key_location = endpoint_config.get("key_location")
                    key_prefix = endpoint_config.get("key_prefix", "")
                    api_key = endpoint_config["key"]

                    if key_field and key_location:
                        if key_location == "param":
                            params[key_field] = api_key
                        elif key_location == "header":
                            headers[key_field] = f"{key_prefix}{api_key}"
                        elif key_location == "auth_basic":
                            auth = httpx.BasicAuth(api_key[0], api_key[1]) # api_key est un tuple (sid, secret)

                    response = await client.request(request_method, url, params=params, headers=headers, json=json_data, auth=auth)
                    response.raise_for_status()
                    success = True
            except Exception as e:
                log_message(f"Health check pour {endpoint_key} ({service_name}) a échoué: {e}", level="warning")
                success = False
            finally:
                latency = time.monotonic() - start_time
                self.update_endpoint_health(service_name, endpoint_key, success, latency)
        log_message(f"Health check terminé pour le service: {service_name}")


    def update_endpoint_health(self, service_name: str, endpoint_key: str, success: bool, latency: float):
        """Met à jour le statut de santé d'un endpoint."""
        if service_name not in self.health_status or endpoint_key not in self.health_status[service_name]:
            # Devrait être initialisé, mais au cas où
            self._initialize_health_status()
            if service_name not in self.health_status or endpoint_key not in self.health_status[service_name]:
                log_message(f"Endpoint {endpoint_key} pour {service_name} non trouvé après initialisation. Impossible de mettre à jour.", level="error")
                return

        status = self.health_status[service_name][endpoint_key]
        status["total_checks"] += 1
        status["last_checked"] = format_datetime(get_current_time())

        # Mise à jour du taux de succès et de la latence
        alpha = 0.1 # Facteur de lissage pour la moyenne mobile
        if success:
            status["error_count"] = max(0, status["error_count"] - 1) # Réduit le compteur d'erreurs sur succès
            status["success_rate"] = status["success_rate"] * (1 - alpha) + 1.0 * alpha
            status["latency"] = status["latency"] * (1 - alpha) + latency * alpha
        else:
            status["error_count"] += 1
            status["success_rate"] = status["success_rate"] * (1 - alpha) + 0.0 * alpha
            status["latency"] = status["latency"] * (1 - alpha) + 10.0 * alpha # Pénalité de latence sur erreur

        # Définir la santé basée sur le taux d'erreurs/succès
        if status["error_count"] >= 3 or status["success_rate"] < 0.5: # 3 erreurs consécutives ou taux de succès faible
            status["is_healthy"] = False
        else:
            status["is_healthy"] = True
        
        save_json(ENDPOINT_HEALTH_FILE, self.health_status)
        log_message(f"Santé de {service_name}:{endpoint_key} mise à jour: Succès: {success}, Latence: {latency:.2f}s, Taux Succès: {status['success_rate']:.2f}, Sain: {status['is_healthy']}")

    def get_best_endpoint(self, service_name: str) -> Optional[Dict]:
        """Sélectionne le meilleur endpoint pour un service basé sur la santé."""
        service_health = self.health_status.get(service_name)
        if not service_health:
            log_message(f"Aucune donnée de santé pour le service {service_name}.", level="warning")
            return None

        best_endpoint_key = None
        best_score = -float('inf') # Score basé sur la santé pour la sélection

        healthy_endpoints = [
            (key, status) for key, status in service_health.items() if status["is_healthy"]
        ]

        if not healthy_endpoints:
            log_message(f"Aucun endpoint sain pour le service {service_name}. Tentative de sélection d'un endpoint non sain.", level="warning")
            # Fallback: si aucun sain, prendre le moins mauvais
            all_endpoints = service_health.items()
            if not all_endpoints: return None
            
            # Prioriser le moins d'erreurs, puis la latence la plus faible
            sorted_endpoints = sorted(all_endpoints, key=lambda item: (item[1]["error_count"], item[1]["latency"]))
            best_endpoint_key = sorted_endpoints[0][0]
            log_message(f"Fallback: Endpoint {best_endpoint_key} sélectionné pour {service_name} (non sain).", level="warning")
        else:
            # Calculer un score pour chaque endpoint sain: (success_rate * 100) - (latency * 10) - (error_count * 5)
            # Un score plus élevé est meilleur.
            for endpoint_key, status in healthy_endpoints:
                score = (status["success_rate"] * 100) - (status["latency"] * 10) - (status["error_count"] * 5)
                if score > best_score:
                    best_score = score
                    best_endpoint_key = endpoint_key
            log_message(f"Meilleur endpoint sélectionné pour {service_name}: {best_endpoint_key} (Score: {best_score:.2f})")

        if best_endpoint_key:
            # Trouver la configuration originale de l'endpoint
            for endpoint_config in API_CONFIG.get(service_name, []):
                current_endpoint_key = f"{endpoint_config['endpoint_name']}-{endpoint_config['key']}"
                if current_endpoint_key == best_endpoint_key:
                    return endpoint_config
        return None

# Instancier le gestionnaire de santé des endpoints
endpoint_health_manager = EndpointHealthManager()

# --- FIN DU BLOC GESTION SANTE ENDPOINT ---

# --- DEBUT DU BLOC CLIENT API (BASE) ---

class APIClient:
    """Classe de base pour tous les clients API, gérant la sélection dynamique d'endpoints et les réessais."""
    def __init__(self, name: str):
        self.name = name
        self.endpoints_config = API_CONFIG.get(name, [])
        if not self.endpoints_config:
            log_message(f"Client API {self.name} initialisé sans configuration d'endpoint.", level="error")

    async def _make_request(self, params: Dict = None, headers: Dict = None, json_data: Dict = None, timeout: int = 30, max_retries: int = 3, initial_delay: float = 1.0, url: Optional[str] = None, method: Optional[str] = None, key_field: Optional[str] = None, key_location: Optional[str] = None, api_key: Optional[Union[str, tuple]] = None, fixed_params: Optional[Dict] = None, fixed_headers: Optional[Dict] = None, fixed_json: Optional[Dict] = None) -> Optional[Dict]:
        """Méthode interne pour effectuer les requêtes HTTP en utilisant le meilleur endpoint avec réessais."""
        
        # Use provided URL/method/key if explicitly given, otherwise use selected endpoint config
        if url and method:
            selected_endpoint_config = {
                "url": url,
                "method": method,
                "key_field": key_field,
                "key_location": key_location,
                "key": api_key,
                "fixed_params": fixed_params if fixed_params is not None else {},
                "fixed_headers": fixed_headers if fixed_headers is not None else {},
                "fixed_json": fixed_json if fixed_json is not None else {},
                "endpoint_name": "Dynamic" # Placeholder for health manager
            }
        else:
            selected_endpoint_config = endpoint_health_manager.get_best_endpoint(self.name)
            if not selected_endpoint_config:
                return {"error": True, "message": f"Aucun endpoint sain ou disponible pour {self.name}."}

        url_to_use = selected_endpoint_config["url"]
        method_to_use = selected_endpoint_config["method"]
        endpoint_key_for_health = f"{selected_endpoint_config['endpoint_name']}-{selected_endpoint_config['key']}"

        # Copier pour ne pas modifier les fixed_params/headers/json_data globaux
        request_params = selected_endpoint_config.get("fixed_params", {}).copy()
        request_headers = selected_endpoint_config.get("fixed_headers", {}).copy()
        request_json_data = selected_endpoint_config.get("fixed_json", {}).copy()
        auth = None

        # Fusionner les paramètres dynamiques avec les fixes
        if params:
            request_params.update(params)
        if headers:
            request_headers.update(headers)
        if json_data:
            request_json_data.update(json_data)

        # Ajouter la clé API selon sa configuration
        key_field_to_use = selected_endpoint_config.get("key_field")
        key_location_to_use = selected_endpoint_config.get("key_location")
        key_prefix = selected_endpoint_config.get("key_prefix", "")
        api_key_to_use = selected_endpoint_config["key"] # La clé réelle

        if key_field_to_use and key_location_to_use:
            if key_location_to_use == "param":
                request_params[key_field_to_use] = api_key_to_use
            elif key_location_to_use == "header":
                request_headers[key_field_to_use] = f"{key_prefix}{api_key_to_use}"
            elif key_location_to_use == "auth_basic":
                auth = httpx.BasicAuth(api_key_to_use[0], api_key_to_use[1]) # Pour Twilio, api_key est un tuple (sid, secret)

        current_delay = initial_delay
        for attempt in range(max_retries):
            start_time = time.monotonic()
            success = False
            try:
                async with httpx.AsyncClient(timeout=timeout) as client:
                    response = await client.request(method_to_use, url_to_use, params=request_params, headers=request_headers, json=request_json_data, auth=auth)
                    response.raise_for_status() # Lève une exception pour les codes d'erreur HTTP
                    success = True
                    return response.json()
            except httpx.HTTPStatusError as e:
                log_message(f"API {self.name} erreur HTTP (tentative {attempt+1}/{max_retries}): {e.response.status_code} - {e.response.text}", level="warning")
                # Ne pas réessayer pour les erreurs client (4xx)
                if 400 <= e.response.status_code < 500:
                    log_message(f"API {self.name}: Erreur client {e.response.status_code}, pas de réessai.", level="error")
                    endpoint_health_manager.update_endpoint_health(self.name, endpoint_key_for_health, False, e.response.elapsed.total_seconds())
                    return {"error": True, "status_code": e.response.status_code, "message": e.response.text}
                
                # Réessayer pour les erreurs serveur ou timeouts
                if attempt < max_retries - 1:
                    log_message(f"API {self.name}: Réessai dans {current_delay:.2f}s...", level="info")
                    await asyncio.sleep(current_delay)
                    current_delay *= 2 # Backoff exponentiel
            except httpx.RequestError as e:
                log_message(f"API {self.name} erreur de requête (tentative {attempt+1}/{max_retries}): {e}", level="warning")
                if attempt < max_retries - 1:
                    log_message(f"API {self.name}: Réessai dans {current_delay:.2f}s...", level="info")
                    await asyncio.sleep(current_delay)
                    current_delay *= 2
            except json.JSONDecodeError:
                log_message(f"API {self.name} erreur de décodage JSON (tentative {attempt+1}/{max_retries}): {response.text}", level="error")
                # Si la réponse n'est pas JSON, c'est probablement une erreur persistante
                endpoint_health_manager.update_endpoint_health(self.name, endpoint_key_for_health, False, time.monotonic() - start_time)
                return {"error": True, "message": "Réponse JSON invalide de l'API"}
            except Exception as e:
                log_message(f"API {self.name} erreur inattendue (tentative {attempt+1}/{max_retries}): {e}", level="error")
                endpoint_health_manager.update_endpoint_health(self.name, endpoint_key_for_health, False, time.monotonic() - start_time)
                return {"error": True, "message": str(e)}
            finally:
                if not success: # Si l'exception a été levée
                    latency = time.monotonic() - start_time
                    endpoint_health_manager.update_endpoint_health(self.name, endpoint_key_for_health, False, latency)
        
        # Si toutes les tentatives ont échoué
        log_message(f"API {self.name}: Toutes les tentatives ont échoué après {max_retries} réessais.", level="error")
        return {"error": True, "message": f"Échec de la requête après {max_retries} tentatives."}

    async def query(self, *args, **kwargs) -> Any:
        """Méthode abstraite pour interroger l'API."""
        raise NotImplementedError("La méthode query doit être implémentée par les sous-classes.")

# --- FIN DU BLOC CLIENT API (BASE) ---

# --- DEBUT DU BLOC CLIENTS API SPECIFIQUES ---

class DeepSeekClient(APIClient):
    def __init__(self):
        super().__init__("DEEPSEEK")

    async def query(self, prompt: str, model: str = "deepseek-chat") -> str:
        payload = {"model": model, "messages": [{"role": "user", "content": prompt}]}
        response = await self._make_request(json_data=payload)
        if response and not response.get("error"):
            return response.get("choices", [{}])[0].get("message", {}).get("content", "Pas de réponse de DeepSeek.")
        return f"Erreur DeepSeek: {response.get('message', 'Inconnu')}" if response else "DeepSeek: Réponse vide."

class SerperClient(APIClient):
    def __init__(self):
        super().__init__("SERPER")

    async def query(self, query_text: str) -> str:
        payload = {"q": query_text}
        response = await self._make_request(json_data=payload)
        if response and not response.get("error"):
            organic_results = response.get("organic", [])
            if organic_results:
                snippet = organic_results[0].get("snippet", "Pas de snippet.")
                link = organic_results[0].get("link", "")
                return f"Serper (recherche web):\n{snippet} {neutralize_urls(link)}"
            return "Serper: Aucune information trouvée."
        return f"Erreur Serper: {response.get('message', 'Inconnu')}" if response else "Serper: Réponse vide."

class WolframAlphaClient(APIClient):
    def __init__(self):
        super().__init__("WOLFRAMALPHA")

    async def query(self, input_text: str) -> str:
        params = {"input": input_text}
        response = await self._make_request(params=params)
        if response and not response.get("error"):
            pods = response.get("queryresult", {}).get("pods", [])
            if pods:
                for pod in pods:
                    if pod.get("title") in ["Result", "Input interpretation", "Decimal approximation"]:
                        subpods = pod.get("subpods", [])
                        if subpods and subpods[0].get("plaintext"):
                            return f"WolframAlpha:\n{subpods[0]['plaintext']}"
                if pods and pods[0].get("subpods") and pods[0]["subpods"][0].get("plaintext"):
                    return f"WolframAlpha:\n{pods[0]['subpods'][0]['plaintext']}"
            return "WolframAlpha: Pas de résultat clair."
        return f"Erreur WolframAlpha: {response.get('message', 'Inconnu')}" if response else "WolframAlpha: Réponse vide."

class TavilyClient(APIClient):
    def __init__(self):
        super().__init__("TAVILY")

    async def query(self, query_text: str, max_results: int = 3) -> str:
        payload = {"query": query_text, "max_results": max_results}
        response = await self._make_request(json_data=payload)
        if response and not response.get("error"):
            results = response.get("results", [])
            answer = response.get("answer", "Aucune réponse directe trouvée.")

            output = f"Tavily (recherche web):\nRéponse directe: {answer}\n"
            if results:
                output += "Extraits pertinents:\n"
                for i, res in enumerate(results[:max_results]):
                    output += f"- {res.get('title', 'N/A')}: {res.get('content', 'N/A')} {neutralize_urls(res.get('url', ''))}\n"
            return output
        return f"Erreur Tavily: {response.get('message', 'Inconnu')}" if response else "Tavily: Réponse vide."

class ApiFlashClient(APIClient):
    def __init__(self):
        super().__init__("APIFLASH")

    async def query(self, url: str) -> str:
        params = {"url": url, "format": "jpeg", "full_page": "true"}
        response = await self._make_request(params=params)
        if response and not response.get("error"):
            # ApiFlash retourne directement l'image, pas un JSON.
            # La requête _make_request s'attend à du JSON, donc on doit gérer ça.
            # Pour ApiFlash, l'URL de capture est le résultat.
            selected_endpoint_config = endpoint_health_manager.get_best_endpoint(self.name)
            if selected_endpoint_config:
                capture_url = f"{selected_endpoint_config['url']}?access_key={selected_endpoint_config['key']}&url={url}"
                return f"ApiFlash (capture d'écran): {neutralize_urls(capture_url)} (Vérifiez le lien pour l'image)"
            return "ApiFlash: Impossible de générer l'URL de capture."
        # If _make_request returned an error dict, pass it along
        return f"Erreur ApiFlash: {response.get('message', 'Inconnu')}" if response else "ApiFlash: Réponse vide."

class CrawlbaseClient(APIClient):
    def __init__(self):
        super().__init__("CRAWLBASE")

    async def query(self, url: str, use_js: bool = False) -> str:
        params = {"url": url, "format": "json"}
        # Crawlbase has two endpoint configs, one for HTML, one for JS.
        # We need to explicitly select the JS one if use_js is True.
        selected_endpoint_config = None
        if use_js:
            for config in self.endpoints_config:
                if "JS Scraping" in config.get("endpoint_name", ""):
                    selected_endpoint_config = config
                    break
        if not selected_endpoint_config: # Fallback to default if JS endpoint not found or use_js is False
            selected_endpoint_config = endpoint_health_manager.get_best_endpoint(self.name)

        if not selected_endpoint_config:
            return {"error": True, "message": f"Aucun endpoint sain ou disponible pour {self.name}."}

        # Manually make request to ensure the correct endpoint config is used
        response = await self._make_request(
            params=params,
            url=selected_endpoint_config["url"], # Override URL with selected endpoint's URL
            method=selected_endpoint_config["method"],
            key_field=selected_endpoint_config["key_field"],
            key_location=selected_endpoint_config["key_location"],
            api_key=selected_endpoint_config["key"],
            fixed_params=selected_endpoint_config.get("fixed_params", {}) # Include fixed params from selected config
        )

        if response and not response.get("error"):
            body = response.get("body")
            if body:
                try:
                    decoded_body = base64.b64decode(body).decode('utf-8', errors='ignore')
                    return f"Crawlbase (contenu web):\n{decoded_body[:1000]}..." # Truncate for brevity
                except Exception:
                    return f"Crawlbase (contenu web - brut):\n{body[:1000]}..."
            return "Crawlbase: Contenu non trouvé."
        return f"Erreur Crawlbase: {response.get('message', 'Inconnu')}" if response else "Crawlbase: Réponse vide."

class DetectLanguageClient(APIClient):
    def __init__(self):
        super().__init__("DETECTLANGUAGE")

    async def query(self, text: str) -> str:
        payload = {"q": text}
        response = await self._make_request(json_data=payload)
        if response and not response.get("error"):
            detections = response.get("data", {}).get("detections", [])
            if detections:
                first_detection = detections[0]
                lang = first_detection.get("language")
                confidence = first_detection.get("confidence")
                return f"Langue détectée: {lang} (confiance: {confidence})"
            return "DetectLanguage: Aucune langue détectée."
        return f"Erreur DetectLanguage: {response.get('message', 'Inconnu')}" if response else "DetectLanguage: Réponse vide."

class GuardianClient(APIClient):
    def __init__(self):
        super().__init__("GUARDIAN")

    async def query(self, query_text: str) -> str:
        params = {"q": query_text}
        response = await self._make_request(params=params)
        if response and not response.get("error"):
            results = response.get("response", {}).get("results", [])
            if results:
                output = "Articles The Guardian:\n"
                for res in results[:3]: # Limit to 3 articles
                    output += f"- {res.get('webTitle', 'N/A')}: {res.get('fields', {}).get('trailText', 'N/A')} {neutralize_urls(res.get('webUrl', ''))}\n"
                return output
            return "Guardian: Aucun article trouvé."
        return f"Erreur Guardian: {response.get('message', 'Inconnu')}" if response else "Guardian: Réponse vide."

class IP2LocationClient(APIClient):
    def __init__(self):
        super().__init__("IP2LOCATION")

    async def query(self, ip_address: str) -> str:
        params = {"ip": ip_address}
        response = await self._make_request(params=params)
        if response and not response.get("error"):
            if "country_name" in response:
                return f"IP2Location (Géolocalisation IP {ip_address}): Pays: {response['country_name']}, Ville: {response.get('city_name', 'N/A')}"
            return "IP2Location: Informations non trouvées."
        return f"Erreur IP2Location: {response.get('message', 'Inconnu')}" if response else "IP2Location: Réponse vide."

class ShodanClient(APIClient):
    def __init__(self):
        super().__init__("SHODAN")

    async def query(self, query_text: str = "") -> str: # Query text is optional, as /api-info doesn't need it
        # Shodan has various endpoints. This example uses /api-info.
        # For actual search, it would be /shodan/host/search or /shodan/scan
        # For simplicity, we'll just query /api-info which tells us about the key.
        response = await self._make_request() # No specific params needed for /api-info
        if response and not response.get("error"):
            return f"Shodan (info clé): Requêtes restantes: {response.get('usage_limits', {}).get('query_credits', 'N/A')}, Scan crédits: {response.get('usage_limits', {}).get('scan_credits', 'N/A')}"
        return f"Erreur Shodan: {response.get('message', 'Inconnu')}" if response else "Shodan: Réponse vide."

class WeatherAPIClient(APIClient):
    def __init__(self):
        super().__init__("WEATHERAPI")

    async def query(self, location: str) -> str:
        params = {"q": location}
        response = await self._make_request(params=params)
        if response and not response.get("error"):
            current = response.get("current", {})
            location_info = response.get("location", {})
            if current and location_info:
                return (
                    f"Météo à {location_info.get('name', 'N/A')}, {location_info.get('country', 'N/A')}:\n"
                    f"Température: {current.get('temp_c', 'N/A')}°C, "
                    f"Conditions: {current.get('condition', {}).get('text', 'N/A')}, "
                    f"Vent: {current.get('wind_kph', 'N/A')} km/h"
                )
            return "WeatherAPI: Données météo non trouvées."
        return f"Erreur WeatherAPI: {response.get('message', 'Inconnu')}" if response else "WeatherAPI: Réponse vide."

class CloudmersiveClient(APIClient):
    def __init__(self):
        super().__init__("CLOUDMERSIVE")

    async def query(self, domain: str) -> str:
        payload = {"domain": domain}
        response = await self._make_request(json_data=payload)
        if response and not response.get("error"):
            return f"Cloudmersive (vérification de domaine {domain}): Valide: {response.get('ValidDomain', 'N/A')}, Type: {response.get('DomainType', 'N/A')}"
        return f"Erreur Cloudmersive: {response.get('message', 'Inconnu')}" if response else "Cloudmersive: Réponse vide."

class GreyNoiseClient(APIClient):
    def __init__(self):
        super().__init__("GREYNOISE")

    async def query(self, ip_address: str) -> str:
        # GreyNoise endpoint requires IP to be part of the URL path
        selected_endpoint_config = endpoint_health_manager.get_best_endpoint(self.name)
        if not selected_endpoint_config:
            return {"error": True, "message": f"Aucun endpoint sain ou disponible pour {self.name}."}

        # Manually construct URL for GreyNoise since IP is path param
        url = f"{selected_endpoint_config['url']}{ip_address}"
        method = selected_endpoint_config["method"]
        headers = {selected_endpoint_config["key_field"]: selected_endpoint_config["key"]}

        try:
            async with httpx.AsyncClient(timeout=30) as client:
                response = await client.request(method, url, headers=headers)
                response.raise_for_status()
                result = response.json()
                
                # Update health for this specific endpoint (not dynamic selection)
                endpoint_key_for_health = f"{selected_endpoint_config['endpoint_name']}-{selected_endpoint_config['key']}"
                endpoint_health_manager.update_endpoint_health(self.name, endpoint_key_for_health, True, response.elapsed.total_seconds())

                if result and not result.get("error"):
                    if result.get("noise"):
                        return f"GreyNoise (IP {ip_address}): C'est une IP 'bruit' (malveillante). Classification: {result.get('classification', 'N/A')}, Nom d'acteur: {result.get('actor', 'N/A')}"
                    return f"GreyNoise (IP {ip_address}): Pas de 'bruit' détecté. Statut: {result.get('status', 'N/A')}"
                return f"Erreur GreyNoise: {result.get('message', 'Inconnu')}" if result else "GreyNoise: Réponse vide."
        except httpx.HTTPStatusError as e:
            log_message(f"API {self.name} erreur HTTP: {e.response.status_code} - {e.response.text}", level="error")
            endpoint_key_for_health = f"{selected_endpoint_config['endpoint_name']}-{selected_endpoint_config['key']}"
            endpoint_health_manager.update_endpoint_health(self.name, endpoint_key_for_health, False, e.response.elapsed.total_seconds() if e.response else 0.0)
            return {"error": True, "status_code": e.response.status_code, "message": e.response.text}
        except Exception as e:
            log_message(f"API {self.name} erreur inattendue: {e}", level="error")
            endpoint_key_for_health = f"{selected_endpoint_config['endpoint_name']}-{selected_endpoint_config['key']}"
            endpoint_health_manager.update_endpoint_health(self.name, endpoint_key_for_health, False, 0.0) # No latency if request failed before sending
            return {"error": True, "message": str(e)}

class PulsediveClient(APIClient):
    def __init__(self):
        super().__init__("PULSEDIVE")

    async def query(self, indicator: str, type: str = "auto") -> str:
        params = {"indicator": indicator, "type": type}
        response = await self._make_request(params=params)
        if response and not response.get("error"):
            if response.get("results"):
                result = response["results"][0]
                return (
                    f"Pulsedive (Analyse {indicator}): Type: {result.get('type', 'N/A')}, "
                    f"Risk: {result.get('risk', 'N/A')}, "
                    f"Description: {result.get('description', 'N/A')[:200]}..."
                )
            return "Pulsedive: Aucun résultat d'analyse trouvé."
        return f"Erreur Pulsedive: {response.get('message', 'Inconnu')}" if response else "Pulsedive: Réponse vide."

class StormGlassClient(APIClient):
    def __init__(self):
        super().__init__("STORMGLASS")

    async def query(self, lat: float, lng: float, params: str = "airTemperature,waveHeight") -> str:
        now = int(time.time())
        request_params = {
            "lat": lat,
            "lng": lng,
            "params": params,
            "start": now,
            "end": now + 3600 # One hour from now
        }
        response = await self._make_request(params=request_params)
        if response and not response.get("error"):
            data = response.get("hours", [])
            if data:
                first_hour = data[0]
                temp = first_hour.get('airTemperature', [{}])[0].get('value', 'N/A')
                wave_height = first_hour.get('waveHeight', [{}])[0].get('value', 'N/A')
                return f"StormGlass (Météo maritime à {lat},{lng}): Température air: {temp}°C, Hauteur vagues: {wave_height}m"
            return "StormGlass: Données non trouvées."
        return f"Erreur StormGlass: {response.get('message', 'Inconnu')}" if response else "StormGlass: Réponse vide."

class LoginRadiusClient(APIClient):
    def __init__(self):
        super().__init__("LOGINRADIUS")

    async def query(self) -> str:
        response = await self._make_request()
        if response and not response.get("error"):
            return f"LoginRadius (Ping API): Statut: {response.get('Status', 'N/A')}, Message: {response.get('Message', 'N/A')}"
        return f"Erreur LoginRadius: {response.get('message', 'Inconnu')}" if response else "LoginRadius: Réponse vide."

class JsonbinClient(APIClient):
    def __init__(self):
        super().__init__("JSONBIN")

    async def query(self, data: Dict[str, Any], private: bool = True, bin_id: Optional[str] = None) -> str:
        # If bin_id is provided, it's a GET request to access a bin
        if bin_id:
            selected_endpoint_config = None
            for config in self.endpoints_config:
                if "Bin Access" in config.get("endpoint_name", ""):
                    selected_endpoint_config = config
                    break
            if not selected_endpoint_config:
                return {"error": True, "message": f"Aucun endpoint d'accès de bin sain ou disponible pour {self.name}."}

            url = f"{selected_endpoint_config['url']}/{bin_id}"
            method = "GET"
            headers = {selected_endpoint_config["key_field"]: selected_endpoint_config["key"]}
            
            response = await self._make_request(
                headers=headers,
                url=url,
                method=method
            )
            if response and not response.get("error"):
                return f"Jsonbin (Accès bin {bin_id}):\n{json.dumps(response, indent=2)}"
            return f"Erreur Jsonbin (Accès bin): {response.get('message', 'Inconnu')}" if response else "Jsonbin: Réponse vide."
        
        # Otherwise, it's a POST request to create a bin
        else:
            selected_endpoint_config = None
            for config in self.endpoints_config:
                if "Bin Create" in config.get("endpoint_name", ""):
                    selected_endpoint_config = config
                    break
            
            if not selected_endpoint_config:
                return {"error": True, "message": f"Aucun endpoint de création de bin sain ou disponible pour {self.name}."}

            url = selected_endpoint_config["url"]
            method = "POST"
            headers = {selected_endpoint_config["key_field"]: selected_endpoint_config["key"], "Content-Type": "application/json"}
            payload = {"record": data, "private": private}

            response = await self._make_request(
                json_data=payload,
                headers=headers,
                url=url,
                method=method
            )

            if response and not response.get("error"):
                return f"Jsonbin (Création de bin): ID: {response.get('metadata', {}).get('id', 'N/A')}, URL: {neutralize_urls(response.get('metadata', {}).get('url', 'N/A'))}"
            return f"Erreur Jsonbin (Création de bin): {response.get('message', 'Inconnu')}" if response else "Jsonbin: Réponse vide."

class HuggingFaceClient(APIClient):
    def __init__(self):
        super().__init__("HUGGINGFACE")

    async def query(self, model_name: str = "distilbert-base-uncased-finetuned-sst-2-english", input_text: str = "Hello world") -> str:
        # HuggingFace inference endpoint URL includes the model name
        selected_endpoint_config = endpoint_health_manager.get_best_endpoint(self.name)
        if not selected_endpoint_config:
            return {"error": True, "message": f"Aucun endpoint sain ou disponible pour {self.name}."}

        # Override URL for inference
        inference_url = f"https://api-inference.huggingface.co/models/{model_name}"
        
        # Ensure the key is added to headers as per config
        headers = {
            selected_endpoint_config["key_field"]: f"{selected_endpoint_config['key_prefix']}{selected_endpoint_config['key']}",
            "Content-Type": "application/json"
        }
        payload = {"inputs": input_text}

        response = await self._make_request(
            json_data=payload,
            headers=headers,
            url=inference_url,
            method="POST" # Inference is always POST
        )

        if response and not response.get("error"):
            if isinstance(response, list) and response:
                first_result = response[0]
                if isinstance(first_result, list) and first_result:
                    return f"HuggingFace ({model_name} - {first_result[0].get('label')}): Score {first_result[0].get('score', 'N/A'):.2f}"
                elif isinstance(first_result, dict) and "generated_text" in first_result:
                    return f"HuggingFace ({model_name}): {first_result.get('generated_text')}"
            return f"HuggingFace ({model_name}): Réponse non parsée. {response}"
        return f"Erreur HuggingFace: {response.get('message', 'Inconnu')}" if response else "HuggingFace: Réponse vide."

class TwilioClient(APIClient):
    def __init__(self):
        super().__init__("TWILIO")

    async def query(self) -> str:
        # Twilio uses Basic Auth, handled by _make_request
        response = await self._make_request()
        if response and not response.get("error"):
            # The balance endpoint returns balance and currency directly
            return f"Twilio (Balance): {response.get('balance', 'N/A')} {response.get('currency', 'N/A')}"
        return f"Erreur Twilio: {response.get('message', 'Inconnu')}" if response else "Twilio: Réponse vide."

class AbstractAPIClient(APIClient):
    def __init__(self):
        super().__init__("ABSTRACTAPI")

    async def query(self, input_value: str, api_type: str) -> str:
        params = {}
        target_endpoint_name = ""

        if api_type == "PHONE_VALIDATION":
            params["phone"] = input_value
            target_endpoint_name = "Phone Validation"
        elif api_type == "EMAIL_VALIDATION":
            params["email"] = input_value
            # Select one of the email validation keys
            target_endpoint_name = "Email Validation"
        elif api_type == "EXCHANGE_RATES":
            target_endpoint_name = "Exchange Rates"
        elif api_type == "HOLIDAYS":
            params["country"] = input_value if input_value else "US"
            params["year"] = datetime.now().year
            target_endpoint_name = "Holidays"
        else:
            return f"AbstractAPI: Type d'API '{api_type}' non supporté pour la requête."

        selected_endpoint_config = None
        for config in self.endpoints_config:
            if target_endpoint_name in config["endpoint_name"]:
                selected_endpoint_config = config
                break
        
        if not selected_endpoint_config:
            return {"error": True, "message": f"Aucun endpoint sain ou disponible pour {self.name} pour le type {api_type}."}

        response = await self._make_request(
            params=params,
            url=selected_endpoint_config["url"],
            method=selected_endpoint_config["method"],
            key_field=selected_endpoint_config["key_field"],
            key_location=selected_endpoint_config["key_location"],
            api_key=selected_endpoint_config["key"],
            fixed_params=selected_endpoint_config.get("fixed_params", {})
        )

        if response and not response.get("error"):
            if api_type == "PHONE_VALIDATION":
                return (
                    f"AbstractAPI (Validation Tél): Numéro: {response.get('phone', 'N/A')}, "
                    f"Valide: {response.get('valid', 'N/A')}, "
                    f"Pays: {response.get('country', {}).get('name', 'N/A')}"
                )
            elif api_type == "EMAIL_VALIDATION":
                return (
                    f"AbstractAPI (Validation Email): Email: {response.get('email', 'N/A')}, "
                    f"Valide: {response.get('is_valid_format', 'N/A')}, "
                    f"Deliverable: {response.get('is_deliverable', 'N/A')}"
                )
            elif api_type == "EXCHANGE_RATES":
                return f"AbstractAPI (Taux de change): Base: {response.get('base', 'N/A')}, Taux (USD): {response.get('exchange_rates', {}).get('USD', 'N/A')}"
            elif api_type == "HOLIDAYS":
                holidays = [h.get('name', 'N/A') for h in response if h.get('name')]
                return f"AbstractAPI (Jours fériés {params.get('country', 'US')} {params.get('year')}): {', '.join(holidays[:5])}..." if holidays else "Aucun jour férié trouvé."
            return f"AbstractAPI ({api_type}): Réponse brute: {response}"
        return f"Erreur AbstractAPI ({api_type}): {response.get('message', 'Inconnu')}" if response else "AbstractAPI: Réponse vide."

class GeminiAPIClient(APIClient):
    def __init__(self):
        super().__init__("GEMINI_API")

    async def query(self, prompt: str, model: str = "gemini-1.5-flash") -> str:
        payload = {"contents": [{"parts": [{"text": prompt}]}]}
        # Gemini API often requires the model name in the URL path
        selected_endpoint_config = endpoint_health_manager.get_best_endpoint(self.name)
        if not selected_endpoint_config:
            return {"error": True, "message": f"Aucun endpoint sain ou disponible pour {self.name}."}

        # Override URL for specific model generation
        generate_url = f"https://generativelanguage.googleapis.com/v1beta/models/{model}:generateContent"
        
        # Ensure the key is added to params as per config
        request_params = {selected_endpoint_config["key_field"]: selected_endpoint_config["key"]}

        response = await self._make_request(
            json_data=payload,
            params=request_params,
            url=generate_url,
            method="POST",
            timeout=60 # Longer timeout for LLM calls
        )

        if response and not response.get("error"):
            if response.get("candidates") and response["candidates"][0].get("content"):
                return response["candidates"][0]["content"]["parts"][0]["text"]
            return f"Gemini API: Pas de réponse générée. {response}"
        return f"Erreur Gemini API: {response.get('message', 'Inconnu')}" if response else "Gemini API: Réponse vide."

class GoogleCustomSearchClient(APIClient):
    def __init__(self):
        super().__init__("GOOGLE_CUSTOM_SEARCH")

    async def query(self, query_text: str) -> str:
        params = {"q": query_text}
        response = await self._make_request(params=params)
        if response and not response.get("error"):
            items = response.get("items", [])
            if items:
                output = "Google Custom Search:\n"
                for item in items[:3]: # Limit to 3 results
                    output += f"- {item.get('title', 'N/A')}: {item.get('snippet', 'N/A')} {neutralize_urls(item.get('link', ''))}\n"
                return output
            return "Google Custom Search: Aucun résultat trouvé."
        return f"Erreur Google Custom Search: {response.get('message', 'Inconnu')}" if response else "Google Custom Search: Réponse vide."

class OpenRouterClient(APIClient):
    def __init__(self):
        super().__init__("OPENROUTER")

    async def query(self, prompt: str, model: str = "mistralai/mistral-7b-instruct") -> str:
        payload = {"model": model, "messages": [{"role": "user", "content": prompt}]}
        response = await self._make_request(json_data=payload)
        if response and not response.get("error"):
            return response.get("choices", [{}])[0].get("message", {}).get("content", "Pas de réponse d'OpenRouter.")
        return f"Erreur OpenRouter: {response.get('message', 'Inconnu')}" if response else "OpenRouter: Réponse vide."

class RandommerClient(APIClient):
    def __init__(self):
        super().__init__("RANDOMMER")

    async def query(self, country_code: str = "US", quantity: int = 1) -> str:
        params = {"CountryCode": country_code, "Quantity": quantity}
        response = await self._make_request(params=params)
        if response and not response.get("error"):
            if isinstance(response, list) and response:
                return f"Randommer (Numéros de téléphone): {', '.join(response)}"
            return f"Randommer: {response}"
        return f"Erreur Randommer: {response.get('message', 'Inconnu')}" if response else "Randommer: Réponse vide."

class TomorrowIOClient(APIClient):
    def __init__(self):
        super().__init__("TOMORROW.IO")

    async def query(self, location: str, fields: List[str] = None) -> str:
        if fields is None:
            fields = ["temperature", "humidity", "windSpeed"]
        payload = {"location": location, "fields": fields, "units": "metric", "timesteps": ["1h"]}
        response = await self._make_request(json_data=payload)
        if response and not response.get("error"):
            data = response.get("data", {}).get("timelines", [{}])[0].get("intervals", [{}])[0].get("values", {})
            if data:
                output = f"Météo (Tomorrow.io) à {location}:\n"
                for field in fields:
                    output += f"- {field.capitalize()}: {data.get(field, 'N/A')}\n"
                return output
            return "Tomorrow.io: Données météo non trouvées."
        return f"Erreur Tomorrow.io: {response.get('message', 'Inconnu')}" if response else "Tomorrow.io: Réponse vide."

class OpenWeatherMapClient(APIClient):
    def __init__(self):
        super().__init__("OPENWEATHERMAP")

    async def query(self, location: str) -> str:
        params = {"q": location}
        response = await self._make_request(params=params)
        if response and not response.get("error"):
            main_data = response.get("main", {})
            weather_desc = response.get("weather", [{}])[0].get("description", "N/A")
            if main_data:
                return (
                    f"Météo (OpenWeatherMap) à {location}:\n"
                    f"Température: {main_data.get('temp', 'N/A')}°C, "
                    f"Ressenti: {main_data.get('feels_like', 'N/A')}°C, "
                    f"Humidité: {main_data.get('humidity', 'N/A')}%, "
                    f"Conditions: {weather_desc}"
                )
            return "OpenWeatherMap: Données météo non trouvées."
        return f"Erreur OpenWeatherMap: {response.get('message', 'Inconnu')}" if response else "OpenWeatherMap: Réponse vide."

class MockarooClient(APIClient):
    def __init__(self):
        super().__init__("MOCKAROO")

    async def query(self, count: int = 1, fields_json: str = None) -> str:
        # Mockaroo's 'fields' parameter often expects a JSON string, which needs to be URL-encoded for GET requests.
        # The default fixed_params already include a basic fields_json.
        params = {"count": count}
        if fields_json:
            params["fields"] = fields_json # Override default if provided

        response = await self._make_request(params=params)
        if response and not response.get("error"):
            return f"Mockaroo (Génération de données):\n{json.dumps(response, indent=2)}"
        return f"Erreur Mockaroo: {response.get('message', 'Inconnu')}" if response else "Mockaroo: Réponse vide."

class OpenPageRankClient(APIClient):
    def __init__(self):
        super().__init__("OPENPAGERANK")

    async def query(self, domains: List[str]) -> str:
        params = {"domains[]": domains}
        response = await self._make_request(params=params)
        if response and not response.get("error"):
            results = response.get("response", [])
            if results:
                output = "OpenPageRank (Classement de domaine):\n"
                for res in results:
                    output += f"- Domaine: {res.get('domain', 'N/A')}, PageRank: {res.get('page_rank', 'N/A')}\n"
                return output
            return "OpenPageRank: Aucun résultat trouvé."
        return f"Erreur OpenPageRank: {response.get('message', 'Inconnu')}" if response else "OpenPageRank: Réponse vide."

class RapidAPIClient(APIClient):
    def __init__(self):
        super().__init__("RAPIDAPI")

    async def query(self, api_name: str, **kwargs) -> str:
        # RapidAPI is a marketplace, so we need to select the specific API endpoint
        # based on 'api_name' argument.
        selected_endpoint_config = None
        for config in self.endpoints_config:
            if api_name.lower() in config["endpoint_name"].lower():
                selected_endpoint_config = config
                break
        
        if not selected_endpoint_config:
            return f"RapidAPI: Endpoint pour '{api_name}' non trouvé ou non configuré."

        # Manually build request based on selected_endpoint_config
        url = selected_endpoint_config["url"]
        method = selected_endpoint_config["method"]
        
        request_params = selected_endpoint_config.get("fixed_params", {}).copy()
        request_headers = selected_endpoint_config.get("fixed_headers", {}).copy()
        request_json_data = selected_endpoint_config.get("fixed_json", {}).copy()

        # Add dynamic kwargs to params/json_data
        if method == "GET":
            request_params.update(kwargs)
        elif method == "POST":
            request_json_data.update(kwargs)

        headers = {
            selected_endpoint_config["key_field"]: selected_endpoint_config["key"],
            "X-RapidAPI-Host": selected_endpoint_config["fixed_headers"].get("X-RapidAPI-Host") # Specific to RapidAPI
        }
        
        response = await self._make_request(
            params=request_params,
            headers=headers,
            json_data=request_json_data,
            url=url,
            method=method
        )

        if response and not response.get("error"):
            if api_name.lower() == "programming joke":
                return f"RapidAPI (Blague de Programmation): {response.get('setup', '')} - {response.get('punchline', '')}"
            elif api_name.lower() == "currency list quotes":
                return f"RapidAPI (Devises): {json.dumps(response, indent=2)}"
            elif api_name.lower() == "random fact":
                return f"RapidAPI (Fait Aléatoire): {response.get('text', 'N/A')}"
            return f"RapidAPI ({api_name}): {json.dumps(response, indent=2)}"
        return f"Erreur RapidAPI ({api_name}): {response.get('message', 'Inconnu')}" if response else "RapidAPI: Réponse vide."

# --- Instancier tous les clients API ---
ALL_API_CLIENTS = [
    DeepSeekClient(),
    SerperClient(),
    WolframAlphaClient(),
    TavilyClient(),
    ApiFlashClient(),
    CrawlbaseClient(),
    DetectLanguageClient(),
    GuardianClient(),
    IP2LocationClient(),
    ShodanClient(),
    WeatherAPIClient(),
    CloudmersiveClient(),
    GreyNoiseClient(),
    PulsediveClient(),
    StormGlassClient(),
    LoginRadiusClient(),
    JsonbinClient(),
    HuggingFaceClient(),
    TwilioClient(),
    AbstractAPIClient(),
    GeminiAPIClient(),
    GoogleCustomSearchClient(),
    OpenRouterClient(),
    RandommerClient(),
    TomorrowIOClient(),
    OpenWeatherMapClient(),
    MockarooClient(),
    OpenPageRankClient(),
    RapidAPIClient()
]

# --- FIN DU BLOC CLIENTS API SPECIFIQUES ---
# --- DEBUT DU BLOC GESTION MEMOIRE ET QUOTAS ---

class MemoryManager:
    def __init__(self):
        self.chat_history = load_json(HISTORY_FILE, [])
        self.long_term_memory = load_json(LONG_MEMORY_FILE, {})
        self.ia_status = load_json(IA_STATUS_FILE, {})
        self._initialize_ia_status()

    def _initialize_ia_status(self):
        """Initialise le statut des IA si elles ne sont pas déjà présentes ou si leur statut est obsolète."""
        now = get_current_time()
        updated = False
        for client in ALL_API_CLIENTS:
            if client.name not in self.ia_status:
                self.ia_status[client.name] = {
                    "last_used": None,
                    "last_error": None,
                    "error_count": 0,
                    "cooldown_until": None,
                    "success_count": 0,
                    "current_score": 1.0,
                    "last_rotation_check": format_datetime(now),
                    "diversification_score": 1.0 # Nouveau score pour la diversification
                }
                updated = True
            else:
                # S'assurer que les nouvelles clés existent pour les IA existantes
                if "success_count" not in self.ia_status[client.name]:
                    self.ia_status[client.name]["success_count"] = 0
                    updated = True
                if "current_score" not in self.ia_status[client.name]:
                    self.ia_status[client.name]["current_score"] = 1.0
                    updated = True
                if "last_rotation_check" not in self.ia_status[client.name]:
                    self.ia_status[client.name]["last_rotation_check"] = format_datetime(now)
                    updated = True
                if "diversification_score" not in self.ia_status[client.name]:
                    self.ia_status[client.name]["diversification_score"] = 1.0
                    updated = True

        if updated:
            save_json(IA_STATUS_FILE, self.ia_status)
            log_message("Statut des IA initialisé/mis à jour.")

    def add_message_to_history(self, role, content):
        """Ajoute un message à l'historique de la conversation."""
        self.chat_history.append({"role": role, "content": content, "timestamp": format_datetime(get_current_time())})
        self._prune_history()
        save_json(HISTORY_FILE, self.chat_history)
        log_message(f"Message ajouté à l'historique par {role}.")

    def get_chat_history(self, limit=10):
        """Retourne les N derniers messages de l'historique."""
        return self.chat_history[-limit:]

    def add_to_long_term_memory(self, key, value):
        """Ajoute une information à la mémoire à long terme."""
        self.long_term_memory[key] = {"value": value, "timestamp": format_datetime(get_current_time())}
        save_json(LONG_MEMORY_FILE, self.long_term_memory)
        log_message(f"Information ajoutée à la mémoire à long terme: {key}")

    def get_from_long_term_memory(self, key):
        """Récupère une information de la mémoire à long terme."""
        return self.long_term_memory.get(key)

    def update_ia_status(self, ia_name: str, success: bool, error_message: Optional[str] = None):
        """Met à jour le statut et le score d'une IA après une utilisation."""
        status = self.ia_status.get(ia_name)
        if not status:
            log_message(f"Tentative de mise à jour d'un statut d'IA inconnu: {ia_name}", level="warning")
            return

        now = get_current_time()
        status["last_used"] = format_datetime(now)

        if success:
            status["success_count"] += 1
            status["error_count"] = 0
            status["cooldown_until"] = None
            status["last_error"] = None
            status["current_score"] = min(1.0, status["current_score"] + 0.1)
            status["diversification_score"] = max(0.1, status["diversification_score"] - 0.1) # Decrease diversification score on use
            log_message(f"IA {ia_name} : Succès enregistré. Nouveau score: {status['current_score']:.2f}, Diversification: {status['diversification_score']:.2f}")
        else:
            status["error_count"] += 1
            status["last_error"] = error_message
            if status["error_count"] >= 3:
                status["cooldown_until"] = format_datetime(now + timedelta(seconds=API_COOLDOWN_DURATION_SECONDS))
                status["current_score"] = max(0.1, status["current_score"] - 0.2)
                log_message(f"IA {ia_name} : Trop d'erreurs ({status['error_count']}). Cooldown jusqu'à {status['cooldown_until']}. Nouveau score: {status['current_score']:.2f}", level="warning")
            else:
                 status["current_score"] = max(0.1, status["current_score"] - 0.05)
                 log_message(f"IA {ia_name} : Erreur enregistrée. Nouveau score: {status['current_score']:.2f}", level="warning")

        save_json(IA_STATUS_FILE, self.ia_status)

    def recover_diversification_scores(self):
        """Augmente le score de diversification pour les IA non utilisées récemment."""
        now = get_current_time()
        updated = False
        for ia_name, status in self.ia_status.items():
            last_used_str = status.get("last_used")
            if last_used_str:
                last_used_dt = datetime.strptime(last_used_str, "%Y-%m-%d %H:%M:%S UTC")
                # If not used in the last API_ROTATION_INTERVAL_MINUTES * 2 (e.g., 60 mins), recover score
                if (now - last_used_dt).total_seconds() > API_ROTATION_INTERVAL_MINUTES * 60 * 2:
                    if status["diversification_score"] < 1.0:
                        status["diversification_score"] = min(1.0, status["diversification_score"] + 0.05)
                        updated = True
                        log_message(f"IA {ia_name}: Score de diversification récupéré à {status['diversification_score']:.2f}")
            else: # Never used, ensure it's at max
                if status["diversification_score"] < 1.0:
                    status["diversification_score"] = 1.0
                    updated = True
        if updated:
            save_json(IA_STATUS_FILE, self.ia_status)

    def get_ia_status(self, ia_name: str) -> Optional[Dict]:
        """Récupère le statut d'une IA."""
        return self.ia_status.get(ia_name)

    def get_available_ias(self) -> List[str]:
        """Retourne les noms des IA actuellement non en cooldown."""
        available = []
        now = get_current_time()
        for name, status in self.ia_status.items():
            cooldown_until_str = status.get("cooldown_until")
            if cooldown_until_str:
                cooldown_until = datetime.strptime(cooldown_until_str, "%Y-%m-%d %H:%M:%S UTC")
                if now < cooldown_until:
                    continue
            available.append(name)
        return available

    def _prune_history(self, max_entries=50):
        """Supprime les anciennes entrées de l'historique si trop nombreuses."""
        if len(self.chat_history) > max_entries:
            self.chat_history = self.chat_history[-max_entries:]
            log_message(f"Historique de chat purgé, {len(self.chat_history)} entrées restantes.")

class QuotaManager:
    def __init__(self):
        self.quotas = load_json(QUOTAS_FILE, {})
        self._initialize_quotas()

    def _initialize_quotas(self):
        """Initialise les quotas pour toutes les APIs basées sur config.API_QUOTAS."""
        updated = False
        now = get_current_time()
        for api_name, quota_info in API_QUOTAS.items():
            if api_name not in self.quotas:
                self.quotas[api_name] = {
                    "monthly_usage": 0,
                    "daily_usage": 0,
                    "hourly_usage": 0, # Nouveau
                    "hourly_timestamps": [], # Nouveau
                    "last_reset_month": now.month,
                    "last_reset_day": now.day,
                    "last_usage": None,
                    "total_calls": 0,
                    "last_hourly_reset": format_datetime(now)
                }
                updated = True
            else:
                # S'assurer que les nouvelles clés existent pour les APIs existantes
                if "hourly_usage" not in self.quotas[api_name]:
                    self.quotas[api_name]["hourly_usage"] = 0
                    updated = True
                if "hourly_timestamps" not in self.quotas[api_name]:
                    self.quotas[api_name]["hourly_timestamps"] = []
                    updated = True
                if "last_hourly_reset" not in self.quotas[api_name]:
                    self.quotas[api_name]["last_hourly_reset"] = format_datetime(now)
                    updated = True
                if "total_calls" not in self.quotas[api_name]:
                    self.quotas[api_name]["total_calls"] = 0
                    updated = True

        if updated:
            save_json(QUOTAS_FILE, self.quotas)
            log_message("Quotas API initialisés/mis à jour.")

    def _reset_quotas_if_needed(self):
        """Réinitialise les quotas journaliers, mensuels et horaires si nécessaire."""
        now = get_current_time()
        for api_name, data in self.quotas.items():
            # Reset mensuel
            if now.month != data["last_reset_month"]:
                data["monthly_usage"] = 0
                data["last_reset_month"] = now.month
                log_message(f"Quota mensuel pour {api_name} réinitialisé.")
            # Reset journalier
            if now.day != data["last_reset_day"]:
                data["daily_usage"] = 0
                data["last_reset_day"] = now.day
                log_message(f"Quota journalier pour {api_name} réinitialisé.")
            
            # Reset et gestion horaire (nettoyage des timestamps trop anciens)
            one_hour_ago = now - timedelta(hours=1)
            # Filter out timestamps older than one hour
            data["hourly_timestamps"] = [
                ts for ts in data["hourly_timestamps"] 
                if datetime.strptime(ts, "%Y-%m-%d %H:%M:%S UTC").replace(tzinfo=None) > one_hour_ago
            ]
            data["hourly_usage"] = len(data["hourly_timestamps"])
            
            # Update last_hourly_reset to current time if a reset happened or after cleanup
            data["last_hourly_reset"] = format_datetime(now)

        save_json(QUOTAS_FILE, self.quotas)

    def check_and_update_quota(self, api_name: str, cost: int = 1) -> bool:
        """Vérifie si une API a du quota et le décrémente. Retourne True si ok, False sinon."""
        self._reset_quotas_if_needed()
        if api_name not in self.quotas:
            log_message(f"API {api_name} non trouvée dans les quotas définis. Autorisation.", level="warning")
            return True

        quota_data = self.quotas[api_name]
        api_limits = API_QUOTAS.get(api_name, {})
        now = get_current_time()

        monthly_limit = api_limits.get("monthly")
        if monthly_limit is not None and (quota_data["monthly_usage"] + cost) > monthly_limit:
            log_message(f"Quota mensuel dépassé pour {api_name}", level="warning")
            return False

        daily_limit = api_limits.get("daily")
        if daily_limit is not None and (quota_data["daily_usage"] + cost) > daily_limit:
            log_message(f"Quota journalier dépassé pour {api_name}", level="warning")
            return False
        
        hourly_limit = api_limits.get("hourly")
        if hourly_limit is not None and (quota_data["hourly_usage"] + cost) > hourly_limit:
            log_message(f"Quota horaire dépassé pour {api_name}", level="warning")
            return False

        rate_limit_per_sec = api_limits.get("rate_limit_per_sec")
        if rate_limit_per_sec:
            last_usage_str = quota_data.get("last_usage")
            if last_usage_str:
                last_usage = datetime.strptime(last_usage_str, "%Y-%m-%d %H:%M:%S UTC").replace(tzinfo=None)
                time_since_last_call = (now - last_usage).total_seconds()
                if time_since_last_call < (1 / rate_limit_per_sec):
                    log_message(f"Taux de requêtes dépassé pour {api_name}. Attendre {1/rate_limit_per_sec - time_since_last_call:.2f}s", level="warning")
                    return False

        quota_data["monthly_usage"] += cost
        quota_data["daily_usage"] += cost
        quota_data["hourly_usage"] += cost
        quota_data["hourly_timestamps"].append(format_datetime(now)) # Add current timestamp
        quota_data["total_calls"] += cost
        quota_data["last_usage"] = format_datetime(now)
        save_json(QUOTAS_FILE, self.quotas)
        log_message(f"Quota pour {api_name} mis à jour. Usage mensuel: {quota_data['monthly_usage']}/{monthly_limit if monthly_limit else 'Illimité'}, Journalier: {quota_data['daily_usage']}/{daily_limit if daily_limit else 'Illimité'}, Horaire: {quota_data['hourly_usage']}/{hourly_limit if hourly_limit else 'Illimité'}")
        return True

    def get_api_usage(self, api_name: str) -> Optional[Dict]:
        """Retourne les informations d'utilisation d'une API."""
        return self.quotas.get(api_name)

    def get_all_quotas_status(self) -> Dict:
        """Retourne le statut de tous les quotas."""
        self._reset_quotas_if_needed()
        status = {}
        for api_name, quota_data in self.quotas.items():
            api_limits = API_QUOTAS.get(api_name, {})
            monthly_limit = api_limits.get("monthly", "Illimité")
            daily_limit = api_limits.get("daily", "Illimité")
            hourly_limit = api_limits.get("hourly", "Illimité")
            status[api_name] = {
                "monthly_usage": quota_data["monthly_usage"],
                "monthly_limit": monthly_limit,
                "daily_usage": quota_data["daily_usage"],
                "daily_limit": daily_limit,
                "hourly_usage": quota_data["hourly_usage"], # New
                "hourly_limit": hourly_limit,
                "total_calls": quota_data["total_calls"],
                "last_usage": quota_data["last_usage"],
                "last_reset_month": quota_data["last_reset_month"],
                "last_reset_day": quota_data["last_reset_day"],
                "last_hourly_reset": quota_data["last_hourly_reset"]
            }
        return status

    def get_burn_window_apis(self) -> List[str]:
        """
        Identifie les APIs dont les quotas sont sur le point d'être réinitialisés
        et où il est opportun de "brûler" le quota restant.
        """
        burn_apis = []
        now = get_current_time()
        for api_name, data in self.quotas.items():
            api_limits = API_QUOTAS.get(api_name, {})

            if api_limits.get("monthly") is not None:
                next_month_reset = datetime(now.year + (1 if now.month == 12 else 0), (now.month % 12) + 1, 1).replace(tzinfo=None)
                if is_within_time_window(next_month_reset, QUOTA_BURN_WINDOW_HOURS * 60, 0):
                    if data["monthly_usage"] < api_limits["monthly"]:
                        burn_apis.append(f"{api_name} (mensuel: {api_limits['monthly'] - data['monthly_usage']} restants)")

            if api_limits.get("daily") is not None:
                next_day_reset = datetime(now.year, now.month, now.day).replace(tzinfo=None) + timedelta(days=1)
                if is_within_time_window(next_day_reset, QUOTA_BURN_WINDOW_HOURS * 60, 0):
                    if data["daily_usage"] < api_limits["daily"]:
                        burn_apis.append(f"{api_name} (journalier: {api_limits['daily'] - data['daily_usage']} restants)")
        return burn_apis

# Instanciation des gestionnaires
memory_manager = MemoryManager()
quota_manager = QuotaManager()

# --- FIN DU BLOC GESTION MEMOIRE ET QUOTAS ---

# --- DEBUT DU BLOC BOT TELEGRAM PRINCIPAL ---

import time
from telegram import Update, ForceReply
from telegram.ext import Application, CommandHandler, MessageHandler, filters, ContextTypes

# --- Orchestration des IA ---
class IAOrchestrator:
    def __init__(self, memory_manager: MemoryManager, quota_manager: QuotaManager, api_clients: List[APIClient]):
        self.memory_manager = memory_manager
        self.quota_manager = quota_manager
        self.api_clients = {client.name: client for client in api_clients}
        self.last_strategy_rotation_time = get_current_time()
        self.current_ia_strategy = self._determine_initial_strategy()

        # Les quatre moteurs IA principaux (maintenant cinq avec Gemini)
        self.core_ai_engines = {
            "DEEPSEEK": self.api_clients.get("DEEPSEEK"),
            "HUGGINGFACE": self.api_clients.get("HUGGINGFACE"),
            "GOOGLE_CUSTOM_SEARCH": self.api_clients.get("GOOGLE_CUSTOM_SEARCH"),
            "OPENROUTER": self.api_clients.get("OPENROUTER"),
            "GEMINI_API": self.api_clients.get("GEMINI_API") # Ajout de Gemini
        }
        # Filtrer les clients None si l'API n'est pas configurée
        self.core_ai_engines = {k: v for k, v in self.core_ai_engines.items() if v is not None}

        # Définir les "agents mixtes" et leurs capacités (simplified for example)
        # En réalité, ceci serait un système de routing basé sur des modèles NLP plus complexes.
        self.mixed_agents = [
            {"name": "GeneralQueryAgent", "primary_ais": ["DEEPSEEK", "OPENROUTER", "GEMINI_API"], "tools": ["SERPER", "TAVILY", "WOLFRAMALPHA", "WEATHERAPI", "OPENWEATHERMAP"]},
            {"name": "CodingAgent", "primary_ais": ["DEEPSEEK", "HUGGINGFACE", "OPENROUTER", "GEMINI_API"], "tools": []}, # Tools are sandbox/analyzer
            {"name": "SecurityAgent", "primary_ais": ["DEEPSEEK", "OPENROUTER"], "tools": ["IP2LOCATION", "SHODAN", "GREYNOISE", "PULSEDIVE", "CLOUDMERSIVE"]},
            {"name": "DataAgent", "primary_ais": ["DEEPSEEK", "OPENROUTER"], "tools": ["JSONBIN", "MOCKAROO", "RANDOMMER", "OPENPAGERANK", "RAPIDAPI"]},
            {"name": "CommunicationAgent", "primary_ais": ["DEEPSEEK", "OPENROUTER"], "tools": ["TWILIO", "ABSTRACTAPI"]},
            {"name": "NewsAgent", "primary_ais": ["DEEPSEEK", "OPENROUTER"], "tools": ["GUARDIAN", "SERPER", "TAVILY"]},
            {"name": "ImageAgent", "primary_ais": ["DEEPSEEK", "OPENROUTER"], "tools": ["APIFLASH"]}, # OCR tool is separate
            {"name": "LanguageAgent", "primary_ais": ["DEEPSEEK", "OPENROUTER"], "tools": ["DETECTLANGUAGE"]},
            {"name": "WeatherAgent", "primary_ais": ["DEEPSEEK", "OPENROUTER"], "tools": ["WEATHERAPI", "STORMGLASS", "TOMORROW.IO", "OPENWEATHERMAP"]}
        ]
        self.current_agent_index = 0
        self.last_agent_rotation_time = get_current_time()

        # Tool descriptions for AI
        self.tool_descriptions = {
            "SERPER": "Effectue une recherche web sur Google et retourne les snippets et liens pertinents. Paramètres: {\"query\": \"texte de recherche\"}",
            "TAVILY": "Effectue une recherche web avancée et retourne une réponse directe et des extraits. Paramètres: {\"query\": \"texte de recherche\", \"max_results\": nombre}",
            "WOLFRAMALPHA": "Répond à des questions factuelles et calculs complexes. Paramètres: {\"input\": \"question ou calcul\"}",
            "WEATHERAPI": "Fournit la météo actuelle et les prévisions pour une localisation donnée. Paramètres: {\"location\": \"nom de la ville ou code postal\"}",
            "OPENWEATHERMAP": "Fournit la météo actuelle pour une localisation donnée. Paramètres: {\"location\": \"nom de la ville ou code postal\"}",
            "STORMGLASS": "Fournit des données météorologiques maritimes (température, vagues) pour des coordonnées lat/lng. Paramètres: {\"lat\": latitude, \"lng\": longitude, \"params\": \"airTemperature,waveHeight\"}",
            "APIFLASH": "Prend une capture d'écran d'une URL et retourne l'URL de l'image. Paramètres: {\"url\": \"URL du site\"}",
            "CRAWLBASE": "Récupère le contenu HTML ou JavaScript d'une URL. Paramètres: {\"url\": \"URL du site\", \"use_js\": true/false}",
            "DETECTLANGUAGE": "Détecte la langue d'un texte. Paramètres: {\"text\": \"texte à analyser\"}",
            "IP2LOCATION": "Géolocalise une adresse IP. Paramètres: {\"ip_address\": \"adresse IP\"}",
            "SHODAN": "Fournit des informations sur les hôtes et les services exposés sur Internet. Paramètres: {\"query\": \"texte de recherche\"} (optionnel)",
            "GREYNOISE": "Analyse une adresse IP pour déterminer si elle est 'bruit' (malveillante). Paramètres: {\"ip_address\": \"adresse IP\"}",
            "PULSEDIVE": "Analyse des indicateurs de menace (IP, domaine, URL). Paramètres: {\"indicator\": \"indicateur\", \"type\": \"auto\"}",
            "CLOUDMERSIVE": "Vérifie la validité d'un nom de domaine. Paramètres: {\"domain\": \"nom de domaine\"}",
            "JSONBIN": "Stocke ou récupère des données JSON dans un 'bin' privé ou public. Pour créer: {\"data\": {\"clé\": \"valeur\"}, \"private\": true/false}. Pour accéder: {\"bin_id\": \"ID du bin\"}",
            "MOCKAROO": "Génère des données de test aléatoires basées sur des schémas. Paramètres: {\"count\": nombre, \"fields_json\": \"[{\"name\": \"champ\", \"type\": \"Type Mockaroo\"}]\"}",
            "RANDOMMER": "Génère des données aléatoires, comme des numéros de téléphone. Paramètres: {\"country_code\": \"US\", \"quantity\": 1}",
            "OPENPAGERANK": "Récupère le PageRank d'un ou plusieurs domaines. Paramètres: {\"domains\": [\"domaine1.com\", \"domaine2.com\"]}",
            "RAPIDAPI": "Accède à diverses micro-APIs (blagues, faits, devises). Nécessite un 'api_name' (ex: 'Programming Joke'). Paramètres: {\"api_name\": \"Nom de l'API\", \"kwargs\": {\"param1\": \"valeur1\"}}",
            "TWILIO": "Vérifie le solde du compte Twilio. Paramètres: Aucun",
            "ABSTRACTAPI": "Valide des emails, numéros de téléphone, géolocalise des IPs, ou fournit des taux de change/jours fériés. Paramètres: {\"input_value\": \"valeur\", \"api_type\": \"EMAIL_VALIDATION\"|\"PHONE_VALIDATION\"|\"EXCHANGE_RATES\"|\"HOLIDAYS\"}"
        }

    def _determine_initial_strategy(self) -> str:
        """Détermine la stratégie initiale ou la stratégie par défaut."""
        return "balanced"

    def _rotate_strategy_if_needed(self):
        """Change la stratégie d'IA et l'agent si l'intervalle de rotation est passé."""
        now = get_current_time()
        if (now - self.last_strategy_rotation_time).total_seconds() >= API_ROTATION_INTERVAL_MINUTES * 60:
            strategies = ["balanced", "cost_effective", "performance"]
            self.current_ia_strategy = random.choice(strategies)
            self.last_strategy_rotation_time = now
            log_message(f"Stratégie d'IA changée pour: {self.current_ia_strategy}")

            # Rotation des agents mixtes
            self.current_agent_index = (self.current_agent_index + 1) % len(self.mixed_agents)
            self.last_agent_rotation_time = now
            log_message(f"Agent mixte actuel: {self.mixed_agents[self.current_agent_index]['name']}")

            # Mettre à jour le last_rotation_check pour toutes les IA et récupérer les scores de diversification
            for ia_name in self.memory_manager.ia_status:
                self.memory_manager.ia_status[ia_name]["last_rotation_check"] = format_datetime(now)
            self.memory_manager.recover_diversification_scores() # Recover diversification scores
            save_json(IA_STATUS_FILE, self.memory_manager.ia_status)

    async def _select_primary_ai_for_agent(self, agent_config: Dict) -> Optional[APIClient]:
        """Sélectionne une IA primaire parmi celles de l'agent, en tenant compte des quotas, de la santé et de la diversification."""
        available_primary_ais = []
        for ai_name in agent_config["primary_ais"]:
            if ai_name in self.core_ai_engines:
                status = self.memory_manager.get_ia_status(ai_name)
                if status and (status.get("cooldown_until") is None or datetime.strptime(status["cooldown_until"], "%Y-%m-%d %H:%M:%S UTC").replace(tzinfo=None) < get_current_time()):
                    if self.quota_manager.check_and_update_quota(ai_name, cost=0): # Check quota without consuming
                        available_primary_ais.append((ai_name, status["current_score"], status["diversification_score"]))
        
        if not available_primary_ais:
            log_message(f"Aucune IA primaire disponible pour l'agent {agent_config['name']}.", level="warning")
            return None

        # Sélection basée sur la stratégie globale
        selected_ai_name = None
        if self.current_ia_strategy == "balanced":
            # Choisir l'IA avec le meilleur score combiné (current_score + diversification_score)
            available_primary_ais.sort(key=lambda x: x[1] + x[2], reverse=True)
            selected_ai_name = available_primary_ais[0][0]
        elif self.current_ia_strategy == "cost_effective":
            # Prioriser les IA avec des quotas élevés ou illimités, puis le meilleur score
            cost_effective_ais = []
            for ai_name, current_score, diversification_score in available_primary_ais:
                api_limits = API_QUOTAS.get(ai_name, {})
                if api_limits.get("monthly") is None and api_limits.get("daily") is None and api_limits.get("hourly") is None:
                    cost_effective_ais.append((ai_name, current_score, diversification_score))
            if cost_effective_ais:
                cost_effective_ais.sort(key=lambda x: x[1] + x[2], reverse=True)
                selected_ai_name = cost_effective_ais[0][0]
            else: # Fallback au mode équilibré si pas de "pas cher" dispo
                available_primary_ais.sort(key=lambda x: x[1] + x[2], reverse=True)
                selected_ai_name = available_primary_ais[0][0]
        elif self.current_ia_strategy == "performance":
            # Prioriser l'IA avec le plus grand nombre de succès récents comme proxy de performance
            performance_ais = []
            for ai_name, current_score, diversification_score in available_primary_ais:
                status = self.memory_manager.get_ia_status(ai_name)
                performance_ais.append((ai_name, status["success_count"]))
            performance_ais.sort(key=lambda x: x[1], reverse=True)
            selected_ai_name = performance_ais[0][0]
        
        # Vérifier et consommer le quota pour l'IA sélectionnée
        if selected_ai_name and self.quota_manager.check_and_update_quota(selected_ai_name):
            log_message(f"IA primaire sélectionnée pour l'agent: {selected_ai_name} (Stratégie: {self.current_ia_strategy})")
            return self.core_ai_engines[selected_ai_name]
        return None

    async def _run_agent_with_tools(self, agent_config: Dict, query: str) -> str:
        """
        Exécute l'agent mixte en utilisant l'IA primaire sélectionnée
        et en sollicitant les outils pertinents.
        """
        primary_ai_client = await self._select_primary_ai_for_agent(agent_config)
        if not primary_ai_client:
            return f"Désolé, l'agent {agent_config['name']} ne peut pas opérer car aucune IA primaire n'est disponible."

        responses = []
        tools_called_for_report = []
        
        # Prepare tool descriptions for the AI
        available_tools_for_ai = {}
        for tool_name in agent_config.get("tools", []):
            if tool_name in self.tool_descriptions and self.api_clients.get(tool_name):
                available_tools_for_ai[tool_name] = self.tool_descriptions[tool_name]
        
        tool_prompt_part = ""
        if available_tools_for_ai:
            tool_prompt_part = "\n\nTu as accès aux outils suivants:\n"
            for tool_name, desc in available_tools_for_ai.items():
                tool_prompt_part += f"- **{tool_name}**: {desc}\n"
            tool_prompt_part += "\nSi tu as besoin d'utiliser un outil, réponds avec le format suivant: `TOOL_CALL:<nom_outil>:<paramètres_json>`. Par exemple: `TOOL_CALL:WEATHERAPI:{\"location\": \"Paris\"}`. Sinon, réponds normalement."
        
        full_prompt_for_ai = f"{query}{tool_prompt_part}"

        # 1. Obtenir une première réponse de l'IA primaire
        log_message(f"Agent {agent_config['name']} utilise {primary_ai_client.name} pour la requête: '{query}'")
        primary_response_raw = await primary_ai_client.query(full_prompt_for_ai)
        self.memory_manager.update_ia_status(primary_ai_client.name, not primary_response_raw.startswith("Erreur"))
        
        # Check for tool calls in the primary AI's response
        tool_call_match = re.match(r"TOOL_CALL:([A-Z_]+):(.+)", primary_response_raw)
        if tool_call_match:
            tool_name = tool_call_match.group(1)
            params_str = tool_call_match.group(2)
            
            try:
                tool_params = json.loads(params_str)
                tool_client = self.api_clients.get(tool_name)
                if tool_client and self.quota_manager.check_and_update_quota(tool_name):
                    log_message(f"Agent {agent_config['name']} exécute l'outil {tool_name} avec les paramètres: {tool_params}")
                    
                    tool_response = ""
                    # Dynamic tool call based on tool_name and parsed params
                    # This requires careful mapping of tool_params to actual method arguments
                    if tool_name == "SERPER":
                        tool_response = await tool_client.query(query_text=tool_params.get("query"))
                    elif tool_name == "TAVILY":
                        tool_response = await tool_client.query(query_text=tool_params.get("query"))
                    elif tool_name == "WOLFRAMALPHA":
                        tool_response = await tool_client.query(input_text=tool_params.get("input"))
                    elif tool_name == "WEATHERAPI":
                        tool_response = await tool_client.query(location=tool_params.get("location"))
                    elif tool_name == "OPENWEATHERMAP":
                        tool_response = await tool_client.query(location=tool_params.get("location"))
                    elif tool_name == "STORMGLASS":
                        tool_response = await tool_client.query(lat=tool_params.get("lat"), lng=tool_params.get("lng"), params=tool_params.get("params", "airTemperature,waveHeight"))
                    elif tool_name == "APIFLASH":
                        tool_response = await tool_client.query(url=tool_params.get("url"))
                    elif tool_name == "CRAWLBASE":
                        tool_response = await tool_client.query(url=tool_params.get("url"), use_js=tool_params.get("use_js", False))
                    elif tool_name == "DETECTLANGUAGE":
                        tool_response = await tool_client.query(text=tool_params.get("text"))
                    elif tool_name == "IP2LOCATION":
                        tool_response = await tool_client.query(ip_address=tool_params.get("ip_address"))
                    elif tool_name == "SHODAN":
                        tool_response = await tool_client.query(query_text=tool_params.get("query", ""))
                    elif tool_name == "GREYNOISE":
                        tool_response = await tool_client.query(ip_address=tool_params.get("ip_address"))
                    elif tool_name == "PULSEDIVE":
                        tool_response = await tool_client.query(indicator=tool_params.get("indicator"), type=tool_params.get("type", "auto"))
                    elif tool_name == "CLOUDMERSIVE":
                        tool_response = await tool_client.query(domain=tool_params.get("domain"))
                    elif tool_name == "JSONBIN":
                        if "bin_id" in tool_params:
                            tool_response = await tool_client.query(bin_id=tool_params["bin_id"])
                        else:
                            tool_response = await tool_client.query(data=tool_params.get("data", {}), private=tool_params.get("private", True))
                    elif tool_name == "MOCKAROO":
                        tool_response = await tool_client.query(count=tool_params.get("count", 1), fields_json=tool_params.get("fields_json"))
                    elif tool_name == "RANDOMMER":
                        tool_response = await tool_client.query(country_code=tool_params.get("country_code", "US"), quantity=tool_params.get("quantity", 1))
                    elif tool_name == "OPENPAGERANK":
                        tool_response = await tool_client.query(domains=tool_params.get("domains", []))
                    elif tool_name == "RAPIDAPI":
                        tool_response = await tool_client.query(api_name=tool_params.get("api_name"), **tool_params.get("kwargs", {}))
                    elif tool_name == "TWILIO":
                        tool_response = await tool_client.query()
                    elif tool_name == "ABSTRACTAPI":
                        tool_response = await tool_client.query(input_value=tool_params.get("input_value"), api_type=tool_params.get("api_type"))
                    
                    if tool_response:
                        responses.append(f"Réponse outil ({tool_name}): {tool_response}")
                        tools_called_for_report.append({"name": tool_name, "params": tool_params, "result": tool_response})
                    self.memory_manager.update_ia_status(tool_name, not tool_response.startswith("Erreur"))
                    
                    # Feed tool response back to primary AI for final answer
                    follow_up_prompt = f"J'ai exécuté l'outil {tool_name} avec les paramètres {params_str}. Voici le résultat:\n{tool_response}\n\nMaintenant, réponds à la question originale: {query}"
                    final_ai_response = await primary_ai_client.query(follow_up_prompt)
                    self.memory_manager.update_ia_status(primary_ai_client.name, not final_ai_response.startswith("Erreur"))
                    responses.append(f"Réponse finale ({primary_ai_client.name}): {final_ai_response}")

                else:
                    responses.append(f"Erreur: L'outil {tool_name} n'est pas disponible ou le quota est dépassé.")
                    tools_called_for_report.append({"name": tool_name, "params": tool_params, "result": "Quota dépassé ou non disponible."})
            except json.JSONDecodeError:
                responses.append(f"Erreur: Paramètres JSON invalides pour l'outil {tool_name}: {params_str}")
                tools_called_for_report.append({"name": tool_name, "params": params_str, "result": "JSON invalide."})
            except Exception as e:
                responses.append(f"Erreur lors de l'exécution de l'outil {tool_name}: {e}")
                self.memory_manager.update_ia_status(tool_name, False, str(e))
                tools_called_for_report.append({"name": tool_name, "params": params_str, "result": f"Erreur: {e}"})
        else:
            # If no tool call, the primary AI's initial response is the main response
            responses.append(f"Réponse principale ({primary_ai_client.name}): {primary_response_raw}")
        
        return "\n\n".join(responses), tools_called_for_report


    async def process_query(self, query: str) -> str:
        """Traite une requête en sélectionnant un agent mixte et en obtenant une réponse."""
        self._rotate_strategy_if_needed() # Rotation de la stratégie et de l'agent

        # Sélectionner l'agent mixte actuel
        current_agent_config = self.mixed_agents[self.current_agent_index]
        log_message(f"Traitement de la requête avec l'agent: {current_agent_config['name']}")

        # Exécuter l'agent avec ses outils
        agent_raw_response, tools_called_for_report = await self._run_agent_with_tools(current_agent_config, query)
        
        # Synthèse Optimisée des Réponses
        # Vérifier si la réponse est simple ou si elle contient des marqueurs de multiples réponses/outils
        if "Réponse principale (" in agent_raw_response and ("Réponse outil (" in agent_raw_response or len(agent_raw_response.split('\n\n')) > 1):
            log_message("Plusieurs réponses détectées, appel à la synthèse.")
            final_response = await self.synthesize_response(query, [agent_raw_response])
        else:
            log_message("Réponse unique ou simple, pas de synthèse nécessaire.")
            final_response = agent_raw_response # Si une seule réponse, pas besoin de synthétiser

        return final_response, tools_called_for_report

    async def synthesize_response(self, question: str, responses: List[str]) -> str:
        """
        Synthétise les réponses de plusieurs IA en utilisant DeepSeek (le module d'optimisation).
        """
        if not responses:
            return "Je n'ai reçu aucune réponse des IA pour le moment."

        combined_responses = "\n\n".join([f"Réponse {i+1}:\n{r}" for i, r in enumerate(responses)])
        synthesis_prompt = SYNTHESIS_PROMPT_TEMPLATE.format(question=question, responses=combined_responses)

        deepseek_client = self.core_ai_engines.get("DEEPSEEK")
        if not deepseek_client:
            log_message("DeepSeek n'est pas disponible pour la synthèse.", level="warning")
            return "J'ai plusieurs réponses, mais je ne peux pas les synthétiser pour le moment. Voici les réponses brutes:\n\n" + combined_responses

        try:
            synthesis = await deepseek_client.query(synthesis_prompt)
            self.memory_manager.update_ia_status("DEEPSEEK", True) # Update DeepSeek status for synthesis
            return detect_and_correct_toxicity(synthesis)
        except Exception as e:
            log_message(f"Erreur lors de la synthèse avec DeepSeek: {e}", level="error")
            self.memory_manager.update_ia_status("DEEPSEEK", False, str(e))
            return "J'ai rencontré un problème lors de la synthèse des informations. Voici les réponses brutes:\n\n" + combined_responses

# Instancier l'orchestrateur
orchestrator = IAOrchestrator(memory_manager, quota_manager, ALL_API_CLIENTS)

# --- Tâche de fond pour les Health Checks des Endpoints ---
async def periodic_health_check():
    """Exécute des health checks périodiques pour tous les services."""
    while True:
        log_message("Lancement des health checks périodiques pour tous les services...")
        for service_name in API_CONFIG.keys():
            await endpoint_health_manager.run_health_check_for_service(service_name)
        log_message("Health checks périodiques terminés. Prochain check dans 300 secondes.")
        await asyncio.sleep(300) # Vérifie toutes les 5 minutes

# --- Structured Reporting to Private Group ---
async def send_structured_report_to_private_group(context: ContextTypes.DEFAULT_TYPE, report_data: Dict) -> None:
    """Envoie un rapport structuré au groupe privé Telegram."""
    try:
        report_text = f"📊 **Rapport d'Action IA**\n\n"
        report_text += f"**Timestamp**: `{report_data.get('timestamp')}`\n"
        report_text += f"**Agent**: `{report_data.get('agent_name')}`\n"
        report_text += f"**Intention Détectée**: `{report_data.get('intention')}`\n"
        report_text += f"**Requête Utilisateur**: `{report_data.get('user_query')}`\n"
        report_text += f"**IA Primaire Utilisée**: `{report_data.get('primary_ai_used')}`\n"
        
        tools_called = report_data.get('tools_called', [])
        if tools_called:
            report_text += "**Outils Appelés**:\n"
            for tool in tools_called:
                # Truncate tool result for report to avoid very long messages
                tool_result_display = str(tool['result'])
                if len(tool_result_display) > 100:
                    tool_result_display = tool_result_display[:100] + "..."
                report_text += f"- `{tool['name']}` (Params: `{tool['params']}`, Résultat: `{tool_result_display}`)\n"
        else:
            report_text += "**Outils Appelés**: Aucun\n"
        
        # Truncate final response for report
        final_response_display = report_data.get('final_response', '')
        if len(final_response_display) > 500:
            final_response_display = final_response_display[:500] + "..."
        report_text += f"**Réponse Finale**: `{final_response_display}`\n"
        report_text += f"**Durée Totale**: `{report_data.get('duration'):.2f}s`\n"
        report_text += f"**Erreur**: `{report_data.get('error', 'Non')}`\n"

        await context.bot.send_message(chat_id=PRIVATE_GROUP_ID, text=report_text, parse_mode='Markdown')
        log_message(f"Rapport structuré envoyé au groupe privé: {PRIVATE_GROUP_ID}")
    except Exception as e:
        log_message(f"Erreur lors de l'envoi du rapport structuré au groupe privé: {e}", level="error")

# --- Handlers de commandes Telegram ---

async def start(update: Update, context: ContextTypes.DEFAULT_TYPE) -> None:
    """Envoie un message lorsque la commande /start est émise."""
    user = update.effective_user
    await update.message.reply_html(
        f"Salut {user.mention_html()} ! Je suis ton assistant IA de 2025. "
        "Pose-moi une question, demande-moi d'écrire du code, ou de chercher des infos. "
        "Utilise /help pour voir ce que je peux faire.",
        reply_markup=ForceReply(selective=True),
    )
    log_message(f"Commande /start reçue de {user.id}")

async def help_command(update: Update, context: ContextTypes.DEFAULT_TYPE) -> None:
    """Envoie un message lorsque la commande /help est émise."""
    help_text = """
    Voici ce que je peux faire :
    - Pose-moi n'importe quelle question factuelle.
    - Demande-moi d'écrire ou d'améliorer du code (Python, Shell).
    - Cherche des informations sur le web (actualités, météo, géolocalisation IP, etc.).
    - Demande-moi de faire une capture d'écran d'un site web (donne l'URL).
    - Demande-moi d'analyser le contenu d'une page web (donne l'URL).
    - Demande-moi de détecter la langue d'un texte.
    - Demande-moi de valider un numéro de téléphone ou de géolocaliser une IP ou un email.
    - Gère tes rappels et alarmes (Ex: "Rappelle-moi d'acheter du lait à 18h", "Mets une alarme à 7h du matin").
    - Vérifie le statut de mes APIs avec /status.
    - Affiche mon historique de conversation avec /history.
    - Affiche le statut des quotas API avec /quotas.
    - Affiche les APIs où il est opportun de "brûler" le quota avec /burn_quota.

    Exemples :
    - "Quelle est la capitale de la France ?"
    - "Écris un script Python pour trier une liste."
    - "Météo à Paris"
    - "Capture d'écran de https://google.com"
    - "Analyse de https://openai.com"
    - "Détecte la langue de 'Hello world'"
    - "Valide le numéro +33612345678"
    - "Géolocalise l'IP 8.8.8.8"
    - "Valide l'email test@example.com"
    - "Rappelle-moi de faire les courses demain à 10h"
    - "Mets une alarme pour 7h du matin"
    """
    await update.message.reply_text(help_text)
    log_message(f"Commande /help reçue de {update.effective_user.id}")

async def status_command(update: Update, context: ContextTypes.DEFAULT_TYPE) -> None:
    """Affiche le statut et les scores des IA."""
    status_message = "📊 **Statut des IA**:\n"
    now = get_current_time()
    for ia_name, status in memory_manager.ia_status.items():
        cooldown_until_str = status.get("cooldown_until")
        cooldown_status = "Prête"
        if cooldown_until_str:
            cooldown_until = datetime.strptime(cooldown_until_str, "%Y-%m-%d %H:%M:%S UTC").replace(tzinfo=None)
            if now < cooldown_until:
                remaining = cooldown_until - now
                cooldown_status = f"Cooldown ({remaining.total_seconds():.0f}s restantes)"
        
        last_used_str = status.get("last_used", "Jamais")
        if last_used_str != "Jamais":
            last_used_dt = datetime.strptime(last_used_str, "%Y-%m-%d %H:%M:%S UTC").replace(tzinfo=None)
            time_since_last_used = (now - last_used_dt).total_seconds()
            if time_since_last_used < 60:
                last_used_display = f"{time_since_last_used:.0f}s ago"
            elif time_since_last_used < 3600:
                last_used_display = f"{time_since_last_used / 60:.0f}m ago"
            else:
                last_used_display = f"{time_since_last_used / 3600:.1f}h ago"
        else:
            last_used_display = "Jamais"

        status_message += (
            f"- **{ia_name}**: Score: `{status['current_score']:.2f}`, Diversification: `{status['diversification_score']:.2f}`, "
            f"Succès: `{status['success_count']}`, Erreurs: `{status['error_count']}`, "
            f"Statut: `{cooldown_status}`, Dernière utilisation: `{last_used_display}`\n"
        )
    status_message += f"\nStratégie actuelle: `{orchestrator.current_ia_strategy}`"
    status_message += f"\nAgent mixte actuel: `{orchestrator.mixed_agents[orchestrator.current_agent_index]['name']}`"
    await update.message.reply_markdown(status_message)
    log_message(f"Commande /status reçue de {update.effective_user.id}")

async def history_command(update: Update, context: ContextTypes.DEFAULT_TYPE) -> None:
    """Affiche les 10 derniers messages de l'historique."""
    history = memory_manager.get_chat_history()
    if not history:
        await update.message.reply_text("L'historique de conversation est vide.")
        return

    history_text = "📜 **Historique des 10 dernières interactions**:\n\n"
    for entry in history:
        history_text += f"**{entry['role'].capitalize()}** ({entry['timestamp']}):\n{entry['content'][:150]}...\n\n"
    await update.message.reply_markdown(history_text)
    log_message(f"Commande /history reçue de {update.effective_user.id}")

async def quotas_command(update: Update, context: ContextTypes.DEFAULT_TYPE) -> None:
    """Affiche le statut actuel des quotas API."""
    quotas_status = quota_manager.get_all_quotas_status()
    message = "📈 **Statut des Quotas API**:\n\n"
    for api_name, data in quotas_status.items():
        message += (
            f"**{api_name}**:\n"
            f"  - Mensuel: `{data['monthly_usage']}` / `{data['monthly_limit']}`\n"
            f"  - Journalier: `{data['daily_usage']}` / `{data['daily_limit']}`\n"
            f"  - Horaire: `{data['hourly_usage']}` / `{data['hourly_limit']}`\n"
            f"  - Total appels: `{data['total_calls']}`\n"
            f"  - Dernière utilisation: `{data['last_usage'] if data['last_usage'] else 'N/A'}`\n"
            f"  - Reset Mensuel: `{data['last_reset_month']}`\n"
            f"  - Reset Journalier: `{data['last_reset_day']}`\n"
            f"  - Reset Horaire: `{data['last_hourly_reset']}`\n\n"
        )
    await update.message.reply_markdown(message)
    log_message(f"Commande /quotas reçue de {update.effective_user.id}")

async def burn_quota_command(update: Update, context: ContextTypes.DEFAULT_TYPE) -> None:
    """Affiche les APIs où il est opportun de "brûler" le quota."""
    burn_apis = quota_manager.get_burn_window_apis()
    if burn_apis:
        message = "🔥 **APIs où il est opportun de 'brûler' le quota avant réinitialisation**:\n\n"
        for api_info in burn_apis:
            message += f"- {api_info}\n"
        message += f"\nFenêtre de brûlage: {QUOTA_BURN_WINDOW_HOURS} heures avant le reset."
    else:
        message = "🎉 Aucune API n'est actuellement dans une fenêtre de 'brûlage' de quota. Tout est optimisé !"
    await update.message.reply_markdown(message)
    log_message(f"Commande /burn_quota reçue de {update.effective_user.id}")

async def detect_intent(query: str) -> str:
    """Détecte l'intention de l'utilisateur en utilisant Gemini API."""
    prompt = f"Classe la requête suivante dans une des catégories suivantes: 'programmation', 'image', 'météo', 'langue', 'recherche', 'sécurité', 'données', 'communication', 'actualités', 'général'. Réponds uniquement avec le nom de la catégorie. Requête: '{query}'"
    gemini_client = orchestrator.core_ai_engines.get("GEMINI_API")
    if gemini_client:
        try:
            response = await gemini_client.query(prompt)
            # Clean up response to get just the category name
            category = response.strip().lower().replace('.', '').replace('catégorie: ', '')
            if category in ['programmation', 'image', 'météo', 'langue', 'recherche', 'sécurité', 'données', 'communication', 'actualités', 'général']:
                return category
            return "général" # Fallback
        except Exception as e:
            log_message(f"Erreur lors de la détection d'intention avec Gemini: {e}", level="error")
            return "général" # Fallback if AI fails
    return "général" # Fallback if Gemini client not available

# --- Gestionnaire de messages (le cœur du bot) ---

async def handle_message(update: Update, context: ContextTypes.DEFAULT_TYPE) -> None:
    """Traite les messages texte de l'utilisateur."""
    user_message = update.message.text
    user_id = update.effective_user.id
    log_message(f"Message reçu de {user_id}: {user_message}")

    memory_manager.add_message_to_history("user", user_message)

    response_text = ""
    start_processing_time = time.monotonic()
    
    # Intention Detection
    detected_intention = await detect_intent(user_message)
    log_message(f"Intention détectée pour '{user_message}': {detected_intention}")

    tools_called_report = []
    error_occurred = False

    try:
        # Détection d'intentions spécifiques (prioritaires sur l'orchestrateur général)
        if any(keyword in user_message.lower() for keyword in ["alarme", "réveil", "timer", "minuteur", "rappelle-moi", "rappel", "reminder"]):
            log_message("Intention détectée: Alarme/Rappel (Simulé).")
            response_text = "Je peux t'aider avec les alarmes, minuteurs et rappels ! Dis-moi par exemple : 'Mets une alarme à 7h du matin' ou 'Rappelle-moi d'acheter du lait à 18h'."
        elif "```python" in user_message or "```shell" in user_message or "exécute ce code" in user_message.lower() or "teste ce script" in user_message.lower():
            log_message("Intention détectée: Exécution de code.")
            lang_match = re.search(r"```(python|shell)\n(.*?)```", user_message, re.DOTALL)
            if lang_match:
                language = lang_match.group(1)
                code = lang_match.group(2)
                response_text = await run_in_sandbox(code, language)
            else:
                response_text = "Veuillez formater votre code avec des triple backticks et spécifier le langage (ex: ```python\\nprint('Hello')``` ou ```shell\\nls -l```)."
        elif "analyse ce code python" in user_message.lower() or "vérifie ce script python" in user_message.lower():
            log_message("Intention détectée: Analyse de code Python.")
            code_match = re.search(r"```python\n(.*?)```", user_message, re.DOTALL)
            if code_match:
                code = code_match.group(1)
                response_text = await analyze_python_code(code)
            else:
                response_text = "Veuillez fournir le code Python à analyser formaté avec ```python\\n...```."
        elif "extraire texte image" in user_message.lower() or "ocr" in user_message.lower() or "lis cette image" in user_message.lower():
            log_message("Intention détectée: OCR.")
            url_match = re.search(r'https?://[^\s]+(?:\.jpg|\.jpeg|\.png|\.gif|\.bmp|\.tiff)', user_message, re.IGNORECASE)
            if url_match:
                image_url = url_match.group(0)
                # For OCR, we'll try to use Cloudmersive if a key is available for OCR
                # The provided Cloudmersive config is for Domain Check, not OCR.
                # If an OCR endpoint was configured, it would be called here.
                # For now, we'll return a message indicating no direct OCR API.
                response_text = "Désolé, je n'ai pas d'API OCR directement configurée pour le moment. Mon client Cloudmersive est pour la validation de domaine."
            else:
                response_text = "Veuillez fournir une URL d'image valide (jpg, png, etc.) pour l'extraction de texte."
        else:
            log_message("Intention générale, utilisation de l'orchestrateur d'IA.")
            response_text, tools_called_report = await orchestrator.process_query(user_message)

    except Exception as e:
        log_message(f"Erreur majeure lors du traitement du message: {e}", level="error")
        response_text = f"Désolé, une erreur inattendue est survenue: {e}"
        error_occurred = True

    final_response = clean_html_tags(response_text)
    final_response = neutralize_urls(final_response)
    final_response = detect_and_correct_toxicity(final_response)

    await update.message.reply_text(final_response)
    memory_manager.add_message_to_history("assistant", final_response)
    log_message(f"Réponse envoyée à {user_id}.")

    # Send structured report to private group
    end_processing_time = time.monotonic()
    processing_duration = end_processing_time - start_processing_time

    report_data = {
        "timestamp": format_datetime(get_current_time()),
        "agent_name": orchestrator.mixed_agents[orchestrator.current_agent_index]['name'],
        "intention": detected_intention,
        "user_query": user_message,
        "primary_ai_used": orchestrator.core_ai_engines.get(orchestrator.mixed_agents[orchestrator.current_agent_index]['primary_ais'][0]).name if orchestrator.mixed_agents[orchestrator.current_agent_index]['primary_ais'] else "N/A", # Simplified
        "tools_called": tools_called_report, # This needs to be populated by _run_agent_with_tools
        "final_response": final_response,
        "duration": processing_duration,
        "error": "Oui" if error_occurred else "Non"
    }
    await send_structured_report_to_private_group(context, report_data)


# --- Fonction principale pour démarrer le bot ---

async def main() -> None:
    """Démarre le bot."""
    log_message("Démarrage du bot Telegram...")
    application = Application.builder().token(TELEGRAM_BOT_TOKEN).build()

    application.add_handler(CommandHandler("start", start))
    application.add_handler(CommandHandler("help", help_command))
    application.add_handler(CommandHandler("status", status_command))
    application.add_handler(CommandHandler("history", history_command))
    application.add_handler(CommandHandler("quotas", quotas_command))
    application.add_handler(CommandHandler("burn_quota", burn_quota_command))

    application.add_handler(MessageHandler(filters.TEXT & ~filters.COMMAND, handle_message))

    # Démarrer la tâche de fond pour les health checks
    asyncio.create_task(periodic_health_check())

    log_message("Bot prêt à recevoir des messages.")
    await application.run_polling(allowed_updates=Update.ALL_TYPES)

if __name__ == "__main__":
    try:
        # Utilise asyncio.run() pour démarrer la fonction asynchrone principale.
        # C'est la méthode recommandée pour les scripts simples et gère la boucle d'événements.
        asyncio.run(main())
    except KeyboardInterrupt:
        # Gère l'interruption par l'utilisateur (Ctrl+C) pour un arrêt propre.
        logging.info("Bot arrêté par l'utilisateur (Ctrl+C).")
    except Exception as e:
        # Capture et log toute autre erreur fatale au démarrage du bot.
        logging.error(f"Erreur fatale lors du démarrage du bot: {e}", exc_info=True)
        print(f"Une erreur est survenue au démarrage du bot: {e}")

# --- FIN DU FICHIER PRINCIPAL ---


import os
from pathlib import Path

# ==============================================================================
# Paramètres Généraux du Bot
# ==============================================================================

# Token de votre bot Telegram
BOT_TOKEN = "7902342551:AAG6r1QA2GTMZcmcsWHi36Ivd_PVeMXULOs"

# ID du groupe privé où le bot enverra des notifications (ex: alertes quotas, archives)
PRIVATE_GROUP_ID = "-1001234567890"

# Message de démarrage affiché dans la console au lancement du bot
STARTUP_MESSAGE = """
===================================================
🚀 Bot IA Démarré ! 🚀
Version: 1.0.0
Prêt à interagir. Tapez vos commandes ou questions.
===================================================
"""

# ==============================================================================
# Configuration des Chemins de Fichiers
# ==============================================================================

# Répertoire de base pour les données du bot (logs, historiques, quotas, etc.)
BASE_DIR = Path(__file__).parent.parent / "bot_data"
BASE_DIR.mkdir(parents=True, exist_ok=True)

# Chemin du fichier de log principal
LOG_FILE = BASE_DIR / "bot_activity.log"

# Chemin du fichier de log pour les erreurs critiques
ERROR_LOG_PATH = BASE_DIR / "bot_errors.log"

# Fichier pour stocker l'état de santé des endpoints API
ENDPOINT_HEALTH_FILE = BASE_DIR / "endpoint_health.json"

# Fichier pour stocker les informations de quota d'utilisation des APIs
QUOTAS_FILE = BASE_DIR / "api_quotas.json"

# Fichier pour stocker le statut de performance et de diversification des IA
IA_STATUS_FILE = BASE_DIR / "ia_status.json"

# Répertoire pour archiver les pages web
ARCHIVES_DIR = "archives"

# Fichier pour stocker l'historique de chat de chaque utilisateur
USER_CHAT_HISTORY_FILE = "chat_history.json"

# Taille maximale des fichiers (ex: images pour OCR) en octets (10 MB)
MAX_FILE_SIZE = 10 * 1024 * 1024
MAX_IMAGE_SIZE = 10 * 1024 * 1024 # Taille maximale pour les images OCR

# ==============================================================================
# Configuration des APIs (Clés et Paramètres)
# ==============================================================================

# Clés API (Hardcodées comme demandé)
GEMINI_API_KEYS = [
    "YOUR_GEMINI_API_KEY_1",
    "YOUR_GEMINI_API_KEY_2"
]
OCR_API_KEYS = [
    "K8900987654321",
    "K1234567890987"
]
DEEPSEEK_API_KEYS = [
    "sk-ef08317d125947b3a1ce5916592bef00",
    "sk-d73750d96142421cb1098c7056dd7f01"
]
SERPER_API_KEY = "YOUR_SERPER_API_KEY_HERE"
WOLFRAMALPHA_APP_IDS = [
    "YOUR_WOLFRAMALPHA_APP_ID_1",
    "YOUR_WOLFRAMALPHA_APP_ID_2"
]
TAVILY_API_KEYS = [
    "YOUR_TAVILY_API_KEY_1",
    "YOUR_TAVILY_API_KEY_2"
]
APIFLASH_ACCESS_KEY = "YOUR_APIFLASH_ACCESS_KEY_HERE"
CRAWLBASE_API_KEY = "YOUR_CRAWLBASE_API_KEY_HERE"
DETECTLANGUAGE_API_KEY = "YOUR_DETECTLANGUAGE_API_KEY_HERE"
GUARDIAN_API_KEY = "YOUR_GUARDIAN_API_KEY_HERE"
IP2LOCATION_API_KEY = "YOUR_IP2LOCATION_API_KEY_HERE"
SHODAN_API_KEY = "YOUR_SHODAN_API_KEY_HERE"
WEATHERAPI_KEY = "YOUR_WEATHERAPI_KEY_HERE"
CLOUDMERSIVE_API_KEY = "YOUR_CLOUDMERSIVE_API_KEY_HERE"
GREYNOISE_API_KEY = "YOUR_GREYNOISE_API_KEY_HERE"
PULSEDIVE_API_KEY = "YOUR_PULSEDIVE_API_KEY_HERE"
STORMGLASS_API_KEY = "YOUR_STORMGLASS_API_KEY_HERE"
LOGINRADIUS_API_KEY = "YOUR_LOGINRADIUS_API_KEY_HERE"
JSONBIN_API_KEY = "YOUR_JSONBIN_API_KEY_HERE"
HUGGINGFACE_API_KEYS = [
    "hf_YOUR_HUGGINGFACE_API_KEY_1",
    "hf_YOUR_HUGGINGFACE_API_KEY_2"
]
TWILIO_ACCOUNT_SID = "ACxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
TWILIO_AUTH_TOKEN = "your_twilio_auth_token"
ABSTRACTAPI_API_KEYS = [
    "YOUR_ABSTRACTAPI_API_KEY_1",
    "YOUR_ABSTRACTAPI_API_KEY_2"
]
GOOGLE_CUSTOM_SEARCH_API_KEYS = [
    "YOUR_GOOGLE_CUSTOM_SEARCH_API_KEY_1",
    "YOUR_GOOGLE_CUSTOM_SEARCH_API_KEY_2"
]
GOOGLE_CUSTOM_SEARCH_CX_LIST = [
    "YOUR_GOOGLE_CUSTOM_SEARCH_CX_1",
    "YOUR_GOOGLE_CUSTOM_SEARCH_CX_2"
]
RANDOMMER_API_KEY = "YOUR_RANDOMMER_API_KEY_HERE"
TOMORROWIO_API_KEY = "YOUR_TOMORROWIO_API_KEY_HERE"
OPENWEATHERMAP_API_KEY = "YOUR_OPENWEATHERMAP_API_KEY_HERE"
MOCKAROO_API_KEY = "YOUR_MOCKAROO_API_KEY_HERE"
OPENPAGERANK_API_KEY = "YOUR_OPENPAGERANK_API_KEY_HERE"
RAPIDAPI_KEY = "YOUR_RAPIDAPI_KEY_HERE"


# Configuration détaillée des endpoints API
API_CONFIG = {
    "GEMINI_API": [
        {
            "endpoint_name": f"Gemini Chat (Key {i+1})",
            "url": "https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash-latest:generateContent",
            "method": "POST",
            "key": key,
            "key_field": "key",
            "key_location": "param",
            "timeout": 60,
            "health_check_params": {"prompt": "test"},
            "health_check_url_suffix": f"?key={key}"
        }
        for i, key in enumerate(GEMINI_API_KEYS)
    ],
    "OCR_API": [
        {
            "endpoint_name": f"OCR.space (Key {i+1})",
            "url": "https://api.ocr.space/parse/image",
            "method": "POST",
            "key": key,
            "key_field": "apikey",
            "key_location": "header",
            "timeout": 30,
            "fixed_headers": {"Content-Type": "application/json"},
            "health_check_json": {"base64Image": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAQAAAC1HAwCAAAAC0lEQVR42mNkYAAAAAYAAjCB0C8AAAAASUVORK5CYII=", "language": "eng"}, # Minimal valid base64 for health check
        }
        for i, key in enumerate(OCR_API_KEYS)
    ],
    "DEEPSEEK": [
        {
            "endpoint_name": f"DeepSeek Chat (Key {i+1})",
            "url": "https://api.deepseek.com/chat/completions",
            "method": "POST",
            "key": key,
            "key_field": "Authorization",
            "key_location": "header",
            "key_prefix": "Bearer ",
            "timeout": 60,
            "fixed_headers": {"Content-Type": "application/json"},
            "health_check_json": {"model": "deepseek-chat", "messages": [{"role": "user", "content": "hi"}]}
        }
        for i, key in enumerate(DEEPSEEK_API_KEYS)
    ],
    "SERPER": [
        {
            "endpoint_name": "Serper Search",
            "url": "https://google.serper.dev/search",
            "method": "POST",
            "key": SERPER_API_KEY,
            "key_field": "X-API-KEY",
            "key_location": "header",
            "timeout": 30,
            "fixed_headers": {"Content-Type": "application/json"},
            "health_check_json": {"q": "test"}
        }
    ],
    "WOLFRAMALPHA": [
        {
            "endpoint_name": f"WolframAlpha Query (App ID {i+1})",
            "url": "http://api.wolframalpha.com/v2/query",
            "method": "GET",
            "key": app_id,
            "key_field": "appid",
            "key_location": "param",
            "timeout": 30,
            "fixed_params": {"output": "json"},
            "health_check_params": {"input": "2+2", "output": "json"}
        }
        for i, app_id in enumerate(WOLFRAMALPHA_APP_IDS)
    ],
    "TAVILY": [
        {
            "endpoint_name": f"Tavily Search (Key {i+1})",
            "url": "https://api.tavily.com/parse",
            "method": "POST",
            "key": key,
            "key_field": "apikey",
            "key_location": "header",
            "timeout": 30,
            "fixed_headers": {"Content-Type": "application/json"},
            "health_check_json": {"query": "test", "max_results": 1}
        }
        for i, key in enumerate(TAVILY_API_KEYS)
    ],
    "APIFLASH": [
        {
            "endpoint_name": "ApiFlash Screenshot",
            "url": "https://api.apiflash.com/v1/urltoimage",
            "method": "GET",
            "key": APIFLASH_ACCESS_KEY,
            "key_field": "access_key",
            "key_location": "param",
            "timeout": 45,
            "health_check_params": {"url": "example.com", "format": "jpeg"}
        }
    ],
    "CRAWLBASE": [
        {
            "endpoint_name": "Crawlbase Scraper",
            "url": "https://api.crawlbase.com/",
            "method": "GET",
            "key": CRAWLBASE_API_KEY,
            "key_field": "token",
            "key_location": "param",
            "timeout": 60,
            "health_check_params": {"url": "http://example.com", "format": "json"}
        },
        {
            "endpoint_name": "Crawlbase JS Scraper",
            "url": "https://api.crawlbase.com/js",
            "method": "GET",
            "key": CRAWLBASE_API_KEY,
            "key_field": "token",
            "key_location": "param",
            "timeout": 90,
            "health_check_params": {"url": "http://example.com", "format": "json"}
        }
    ],
    "DETECTLANGUAGE": [
        {
            "endpoint_name": "DetectLanguage Detect",
            "url": "https://ws.detectlanguage.com/0.2/detect",
            "method": "POST",
            "key": DETECTLANGUAGE_API_KEY,
            "key_field": "X-Detectlanguage-Api-Key",
            "key_location": "header",
            "timeout": 15,
            "fixed_headers": {"Content-Type": "application/json"},
            "health_check_json": {"q": "Hello world"}
        }
    ],
    "GUARDIAN": [
        {
            "endpoint_name": "Guardian Content",
            "url": "https://content.guardianapis.com/search",
            "method": "GET",
            "key": GUARDIAN_API_KEY,
            "key_field": "api-key",
            "key_location": "param",
            "timeout": 20,
            "health_check_params": {"q": "test"}
        }
    ],
    "IP2LOCATION": [
        {
            "endpoint_name": "IP2Location Geolocation",
            "url": "https://api.ip2location.com/v2/",
            "method": "GET",
            "key": IP2LOCATION_API_KEY,
            "key_field": "key",
            "key_location": "param",
            "timeout": 10,
            "health_check_params": {"ip": "8.8.8.8", "addon": "country,city"}
        }
    ],
    "SHODAN": [
        {
            "endpoint_name": "Shodan API Info",
            "url": "https://api.shodan.io/api-info",
            "method": "GET",
            "key": SHODAN_API_KEY,
            "key_field": "key",
            "key_location": "param",
            "timeout": 15,
            "health_check_url_suffix": f"?key={SHODAN_API_KEY}"
        },
        {
            "endpoint_name": "Shodan Host Info",
            "url": "https://api.shodan.io/shodan/host",
            "method": "GET",
            "key": SHODAN_API_KEY,
            "key_field": "key",
            "key_location": "param",
            "timeout": 20,
            "health_check_url_suffix": f"/8.8.8.8?key={SHODAN_API_KEY}"
        }
    ],
    "WEATHERAPI": [
        {
            "endpoint_name": "WeatherAPI Current",
            "url": "http://api.weatherapi.com/v1/current.json",
            "method": "GET",
            "key": WEATHERAPI_KEY,
            "key_field": "key",
            "key_location": "param",
            "timeout": 15,
            "health_check_params": {"q": "London"}
        }
    ],
    "CLOUDMERSIVE": [
        {
            "endpoint_name": "Cloudmersive Validate Domain",
            "url": "https://api.cloudmersive.com/validate/domain/full",
            "method": "POST",
            "key": CLOUDMERSIVE_API_KEY,
            "key_field": "Apikey",
            "key_location": "header",
            "timeout": 20,
            "fixed_headers": {"Content-Type": "application/json"},
            "health_check_json": {"domain": "example.com"}
        }
    ],
    "GREYNOISE": [
        {
            "endpoint_name": "GreyNoise IP Lookup",
            "url": "https://api.greynoise.io/v3/community",
            "method": "GET",
            "key": GREYNOISE_API_KEY,
            "key_field": "key",
            "key_location": "header",
            "timeout": 20,
            "health_check_url_suffix": "/8.8.8.8"
        }
    ],
    "PULSEDIVE": [
        {
            "endpoint_name": "Pulsedive Indicator",
            "url": "https://pulsedive.com/api/v1/indicator.php",
            "method": "GET",
            "key": PULSEDIVE_API_KEY,
            "key_field": "key",
            "key_location": "param",
            "timeout": 25,
            "fixed_params": {"pretty": "1"},
            "health_check_params": {"indicator": "8.8.8.8", "pretty": "1"}
        }
    ],
    "STORMGLASS": [
        {
            "endpoint_name": "StormGlass Weather",
            "url": "https://api.stormglass.io/v2/weather/point",
            "method": "GET",
            "key": STORMGLASS_API_KEY,
            "key_field": "Authorization",
            "key_location": "header",
            "timeout": 30,
            "health_check_params": {"lat": 0, "lng": 0, "params": "airTemperature", "start": 0, "end": 0},
            "health_check_url_suffix": "?lat=0&lng=0&params=airTemperature&start=0&end=0"
        }
    ],
    "LOGINRADIUS": [
        {
            "endpoint_name": "LoginRadius Ping",
            "url": "https://api.loginradius.com/identity/v2/auth/ping",
            "method": "GET",
            "key": LOGINRADIUS_API_KEY,
            "key_field": "apiKey",
            "key_location": "param",
            "timeout": 10,
            "health_check_url_suffix": f"?apiKey={LOGINRADIUS_API_KEY}"
        }
    ],
    "JSONBIN": [
        {
            "endpoint_name": "Bin Create",
            "url": "https://api.jsonbin.io/v3/b",
            "method": "POST",
            "key": JSONBIN_API_KEY,
            "key_field": "X-Master-Key",
            "key_location": "header",
            "timeout": 20,
            "fixed_headers": {"Content-Type": "application/json", "X-Bin-Private": "true"},
            "health_check_json": {"test": "data"}
        },
        {
            "endpoint_name": "Bin Access",
            "url": "https://api.jsonbin.io/v3/b",
            "method": "GET",
            "key": JSONBIN_API_KEY,
            "key_field": "X-Master-Key",
            "key_location": "header",
            "timeout": 20,
            "health_check_url_suffix": "/60c7b9b0f1a9a87d2b7b7b7b"
        }
    ],
    "HUGGINGFACE": [
        {
            "endpoint_name": f"HuggingFace Inference (Key {i+1})",
            "url": "https://api-inference.huggingface.co/models/",
            "method": "POST",
            "key": key,
            "key_field": "Authorization",
            "key_location": "header",
            "key_prefix": "Bearer ",
            "timeout": 60,
            "fixed_headers": {"Content-Type": "application/json"},
            "health_check_url_suffix": "distilbert-base-uncased-finetuned-sst-2-english",
            "health_check_json": {"inputs": "Hello world"}
        }
        for i, key in enumerate(HUGGINGFACE_API_KEYS)
    ],
    "TWILIO": [
        {
            "endpoint_name": "Account Balance",
            "url": f"https://api.twilio.com/2010-04-01/Accounts/{TWILIO_ACCOUNT_SID}/Balance.json",
            "method": "GET",
            "key": (TWILIO_ACCOUNT_SID, TWILIO_AUTH_TOKEN),
            "key_location": "auth_basic",
            "timeout": 20,
            "health_check_url_suffix": ""
        }
    ],
    "ABSTRACTAPI": [
        {
            "endpoint_name": f"Email Validation (Key {i+1})",
            "url": "https://emailvalidation.abstractapi.com/v1/?",
            "method": "GET",
            "key": key,
            "key_field": "api_key",
            "key_location": "param",
            "timeout": 15,
            "health_check_params": {"email": "test@example.com"}
        }
        for i, key in enumerate(ABSTRACTAPI_API_KEYS)
    ] + [
        {
            "endpoint_name": f"Phone Validation (Key {i+1})",
            "url": "https://phonevalidation.abstractapi.com/v1/?",
            "method": "GET",
            "key": key,
            "key_field": "api_key",
            "key_location": "param",
            "timeout": 15,
            "health_check_params": {"phone": "14151234567"}
        }
        for i, key in enumerate(ABSTRACTAPI_API_KEYS)
    ] + [
        {
            "endpoint_name": f"Exchange Rates (Key {i+1})",
            "url": "https://exchangerates.abstractapi.com/v1/live",
            "method": "GET",
            "key": key,
            "key_field": "api_key",
            "key_location": "param",
            "timeout": 15,
            "health_check_params": {"base": "USD"}
        }
        for i, key in enumerate(ABSTRACTAPI_API_KEYS)
    ] + [
        {
            "endpoint_name": f"Holidays (Key {i+1})",
            "url": "https://holidays.abstractapi.com/v1/",
            "method": "GET",
            "key": key,
            "key_field": "api_key",
            "key_location": "param",
            "timeout": 15,
            "health_check_params": {"country": "US", "year": "2023", "month": "1", "day": "1"}
        }
        for i, key in enumerate(ABSTRACTAPI_API_KEYS)
    ],
    "GOOGLE_CUSTOM_SEARCH": [
        {
            "endpoint_name": f"Google Custom Search (API Key {i+1}, CX {j+1})",
            "url": "https://www.googleapis.com/customsearch/v1",
            "method": "GET",
            "key": GOOGLE_CUSTOM_SEARCH_API_KEYS[i],
            "key_field": "key",
            "key_location": "param",
            "timeout": 30,
            "fixed_params": {"cx": GOOGLE_CUSTOM_SEARCH_CX_LIST[j]},
            "health_check_params": {"q": "test", "cx": GOOGLE_CUSTOM_SEARCH_CX_LIST[j]}
        }
        for i in range(len(GOOGLE_CUSTOM_SEARCH_API_KEYS))
        for j in range(len(GOOGLE_CUSTOM_SEARCH_CX_LIST))
    ],
    "RANDOMMER": [
        {
            "endpoint_name": "Randommer Phone Numbers",
            "url": "https://randommer.io/api/Phone/Generate",
            "method": "GET",
            "key": RANDOMMER_API_KEY,
            "key_field": "X-Api-Key",
            "key_location": "header",
            "timeout": 15,
            "fixed_headers": {"Content-Type": "application/json"},
            "health_check_params": {"CountryCode": "US", "Quantity": 1}
        }
    ],
    "TOMORROW.IO": [
        {
            "endpoint_name": "Tomorrow.io Weather",
            "url": "https://api.tomorrow.io/v4/weather/realtime",
            "method": "GET",
            "key": TOMORROWIO_API_KEY,
            "key_field": "apikey",
            "key_location": "param",
            "timeout": 20,
            "health_check_params": {"location": "42.3478,-71.0466", "fields": "temperature"}
        }
    ],
    "OPENWEATHERMAP": [
        {
            "endpoint_name": "OpenWeatherMap Current",
            "url": "https://api.openweathermap.org/data/2.5/weather",
            "method": "GET",
            "key": OPENWEATHERMAP_API_KEY,
            "key_field": "appid",
            "key_location": "param",
            "timeout": 15,
            "health_check_params": {"q": "London"}
        }
    ],
    "MOCKAROO": [
        {
            "endpoint_name": "Mockaroo Generate Data",
            "url": "https://api.mockaroo.com/api/generate.json",
            "method": "GET",
            "key": MOCKAROO_API_KEY,
            "key_field": "key",
            "key_location": "param",
            "timeout": 30,
            "health_check_params": {"count": 1, "fields": '[{"name":"id","type":"Row Number"}]'}
        }
    ],
    "OPENPAGERANK": [
        {
            "endpoint_name": "OpenPageRank Domains",
            "url": "https://openpagerank.com/api/v1.0/getPageRank",
            "method": "GET",
            "key": OPENPAGERANK_API_KEY,
            "key_field": "api_key",
            "key_location": "param",
            "timeout": 20,
            "health_check_params": {"domains[]": ["google.com"]}
        }
    ],
    "RAPIDAPI": [
        {
            "endpoint_name": "RapidAPI Programming Joke",
            "url": "https://programming-jokes-api.p.rapidapi.com/jokes/random",
            "method": "GET",
            "key": RAPIDAPI_KEY,
            "key_field": "X-RapidAPI-Key",
            "key_location": "header",
            "timeout": 20,
            "fixed_headers": {"X-RapidAPI-Host": "programming-jokes-api.p.rapidapi.com"},
            "health_check_url_suffix": ""
        },
        {
            "endpoint_name": "RapidAPI Currency List Quotes",
            "url": "https://currency-exchange.p.rapidapi.com/listquotes",
            "method": "GET",
            "key": RAPIDAPI_KEY,
            "key_field": "X-RapidAPI-Key",
            "key_location": "header",
            "timeout": 20,
            "fixed_headers": {"X-RapidAPI-Host": "currency-exchange.p.rapidapi.com"},
            "health_check_url_suffix": ""
        },
        {
            "endpoint_name": "RapidAPI Random Fact",
            "url": "https://random-facts-api.p.rapidapi.com/api/random",
            "method": "GET",
            "key": RAPIDAPI_KEY,
            "key_field": "X-RapidAPI-Key",
            "key_location": "header",
            "timeout": 20,
            "fixed_headers": {"X-RapidAPI-Host": "random-facts-api.p.rapidapi.com"},
            "health_check_url_suffix": ""
        }
    ]
}

# ==============================================================================
# Configuration des Modèles Gemini
# ==============================================================================

# Paramètres de génération pour l'API Gemini
GEMINI_TEMPERATURE = 0.7
GEMINI_TOP_P = 0.95
GEMINI_TOP_K = 40
GEMINI_MAX_OUTPUT_TOKENS = 8192

# Paramètres de sécurité pour l'API Gemini
GEMINI_SAFETY_SETTINGS = [
    {"category": "HARM_CATEGORY_HARASSMENT", "threshold": "BLOCK_NONE"},
    {"category": "HARM_CATEGORY_HATE_SPEECH", "threshold": "BLOCK_NONE"},
    {"category": "HARM_CATEGORY_SEXUALLY_EXPLICIT", "threshold": "BLOCK_NONE"},
    {"category": "HARM_CATEGORY_DANGEROUS_CONTENT", "threshold": "BLOCK_NONE"},
]

# ==============================================================================
# Configuration des Outils (Tool Calling)
# ==============================================================================

# Définition des outils que le bot peut utiliser via le "Function Calling"
TOOL_CONFIG = {
    "serper_query": {
        "description": "Effectue une recherche web via l'API Serper et retourne les snippets pertinents.",
        "parameters": {
            "type": "object",
            "properties": {
                "query_text": {"type": "string", "description": "La requête de recherche."}
            },
            "required": ["query_text"]
        }
    },
    "wolframalpha_query": {
        "description": "Interroge WolframAlpha pour des calculs, des faits ou des données complexes.",
        "parameters": {
            "type": "object",
            "properties": {
                "input_text": {"type": "string", "description": "La requête à soumettre à WolframAlpha."}
            },
            "required": ["input_text"]
        }
    },
    "tavily_query": {
        "description": "Effectue une recherche web avancée via l'API Tavily, fournissant des extraits et une réponse directe.",
        "parameters": {
            "type": "object",
            "properties": {
                "query_text": {"type": "string", "description": "La requête de recherche."},
                "max_results": {"type": "integer", "description": "Nombre maximum de résultats à retourner.", "default": 3}
            },
            "required": ["query_text"]
        }
    },
    "run_in_sandbox": {
        "description": "Exécute du code Python ou Shell dans un environnement sandbox simulé et retourne la sortie.",
        "parameters": {
            "type": "object",
            "properties": {
                "code": {"type": "string", "description": "Le code à exécuter."},
                "language": {"type": "string", "description": "Le langage du code ('python' ou 'shell').", "enum": ["python", "shell"], "default": "python"}
            },
            "required": ["code"]
        }
    },
    "perform_ocr_api": {
        "description": "Effectue une reconnaissance optique de caractères (OCR) sur une image donnée par URL et retourne le texte extrait.",
        "parameters": {
            "type": "object",
            "properties": {
                "image_url": {"type": "string", "description": "L'URL de l'image à traiter par OCR."}
            },
            "required": ["image_url"]
        }
    },
    "fetch_and_archive_pages": {
        "description": "Récupère le contenu de pages web spécifiées, les archive localement et envoie les liens d'archive au groupe privé.",
        "parameters": {
            "type": "object",
            "properties": {
                "links": {"type": "array", "items": {"type": "string"}, "description": "Liste des URLs des pages à archiver."},
                "user_id": {"type": "string", "description": "L'ID de l'utilisateur demandant l'archivage."}
            },
            "required": ["links", "user_id"]
        }
    },
    "ocr_extract_text": {
        "description": "Extrait le texte d'une image encodée en base64 en utilisant l'OCR. Utile pour les images directement fournies dans le chat.",
        "parameters": {
            "type": "object",
            "properties": {
                "image_base64": {"type": "string", "description": "L'image encodée en base64, incluant le préfixe mimeType (ex: 'data:image/png;base64,...')."}
            },
            "required": ["image_base64"]
        }
    },
    "apiflash_query": {
        "description": "Capture une capture d'écran d'une URL via ApiFlash et retourne l'URL de l'image capturée.",
        "parameters": {
            "type": "object",
            "properties": {
                "url": {"type": "string", "description": "L'URL de la page à capturer."}
            },
            "required": ["url"]
        }
    },
    "crawlbase_query": {
        "description": "Scrape le contenu HTML ou JavaScript d'une URL via Crawlbase. Utilisez 'use_js' pour les pages dynamiques.",
        "parameters": {
            "type": "object",
            "properties": {
                "url": {"type": "string", "description": "L'URL de la page à scraper."},
                "use_js": {"type": "boolean", "description": "Définir à true pour le scraping JavaScript.", "default": False}
            },
            "required": ["url"]
        }
    },
    "detectlanguage_query": {
        "description": "Détecte la langue d'un texte via DetectLanguage API.",
        "parameters": {
            "type": "object",
            "properties": {
                "text": {"type": "string", "description": "Le texte dont la langue doit être détectée."}
            },
            "required": ["text"]
        }
    },
    "guardian_query": {
        "description": "Recherche des articles de presse via l'API The Guardian.",
        "parameters": {
            "type": "object",
            "properties": {
                "query_text": {"type": "string", "description": "La requête de recherche pour les articles."}
            },
            "required": ["query_text"]
        }
    },
    "ip2location_query": {
        "description": "Géolocalise une adresse IP via IP2Location API.",
        "parameters": {
            "type": "object",
            "properties": {
                "ip_address": {"type": "string", "description": "L'adresse IP à géolocaliser."}
            },
            "required": ["ip_address"]
        }
    },
    "shodan_query": {
        "description": "Interroge Shodan pour des informations sur un hôte IP ou des informations sur la clé API.",
        "parameters": {
            "type": "object",
            "properties": {
                "query_text": {"type": "string", "description": "L'adresse IP à rechercher ou vide pour les infos de la clé API."}
            },
            "required": []
        }
    },
    "weatherapi_query": {
        "description": "Récupère les conditions météorologiques actuelles pour une localisation via WeatherAPI.",
        "parameters": {
            "type": "object",
            "properties": {
                "location": {"type": "string", "description": "La ville ou le code postal pour la météo."}
            },
            "required": ["location"]
        }
    },
    "cloudmersive_query": {
        "description": "Vérifie la validité et le type d'un domaine via Cloudmersive API.",
        "parameters": {
            "type": "object",
            "properties": {
                "domain": {"type": "string", "description": "Le nom de domaine à vérifier."}
            },
            "required": ["domain"]
        }
    },
    "greynoise_query": {
        "description": "Analyse une adresse IP pour détecter des activités 'bruit' (malveillantes) via GreyNoise.",
        "parameters": {
            "type": "object",
            "properties": {
                "ip_address": {"type": "string", "description": "L'adresse IP à analyser."}
            },
            "required": ["ip_address"]
        }
    },
    "pulsedive_query": {
        "description": "Analyse un indicateur de menace (IP, domaine, URL) via Pulsedive.",
        "parameters": {
            "type": "object",
            "properties": {
                "indicator": {"type": "string", "description": "L'indicateur de menace à analyser (IP, domaine, URL)."},
                "type": {"type": "string", "description": "Le type d'indicateur ('auto', 'ip', 'domain', 'url').", "default": "auto"}
            },
            "required": ["indicator"]
        }
    },
    "stormglass_query": {
        "description": "Récupère les données météorologiques maritimes pour une coordonnée (latitude, longitude) via StormGlass.",
        "parameters": {
            "type": "object",
            "properties": {
                "lat": {"type": "number", "format": "float", "description": "La latitude."},
                "lng": {"type": "number", "format": "float", "description": "La longitude."},
                "params": {"type": "string", "description": "Paramètres météo à récupérer (ex: 'airTemperature,waveHeight').", "default": "airTemperature,waveHeight"}
            },
            "required": ["lat", "lng"]
        }
    },
    "loginradius_query": {
        "description": "Effectue un simple ping à l'API LoginRadius pour vérifier sa disponibilité.",
        "parameters": {
            "type": "object",
            "properties": {}
        }
    },
    "jsonbin_query": {
        "description": "Crée un nouveau 'bin' JSON ou accède à un bin existant via Jsonbin.io.",
        "parameters": {
            "type": "object",
            "properties": {
                "data": {"type": "object", "description": "Les données JSON à sauvegarder lors de la création d'un bin.", "nullable": True},
                "private": {"type": "boolean", "description": "Indique si le bin doit être privé (true) ou public (false).", "default": True},
                "bin_id": {"type": "string", "description": "L'ID du bin existant à accéder (si pas de 'data').", "nullable": True}
            },
            "required": []
        }
    },
    "huggingface_query": {
        "description": "Effectue une inférence sur un modèle HuggingFace (ex: classification de texte, génération).",
        "parameters": {
            "type": "object",
            "properties": {
                "model_name": {"type": "string", "description": "Le nom du modèle HuggingFace à utiliser (ex: 'distilbert-base-uncased-finetuned-sst-2-english').", "default": "distilbert-base-uncased-finetuned-sst-2-english"},
                "input_text": {"type": "string", "description": "Le texte d'entrée pour l'inférence."}
            },
            "required": ["input_text"]
        }
    },
    "twilio_query": {
        "description": "Récupère le solde du compte Twilio.",
        "parameters": {
            "type": "object",
            "properties": {}
        }
    },
    "abstractapi_query": {
        "description": "Interroge diverses APIs d'AbstractAPI (validation email/téléphone, taux de change, jours fériés).",
        "parameters": {
            "type": "object",
            "properties": {
                "input_value": {"type": "string", "description": "La valeur d'entrée (email, numéro de téléphone, code pays, devise de base)."},
                "api_type": {"type": "string", "description": "Le type d'API AbstractAPI à utiliser ('PHONE_VALIDATION', 'EMAIL_VALIDATION', 'EXCHANGE_RATES', 'HOLIDAYS').", "enum": ["PHONE_VALIDATION", "EMAIL_VALIDATION", "EXCHANGE_RATES", "HOLIDAYS"]}
            },
            "required": ["api_type"]
        }
    },
    "google_custom_search_query": {
        "description": "Effectue une recherche personnalisée Google via l'API Custom Search.",
        "parameters": {
            "type": "object",
            "properties": {
                "query_text": {"type": "string", "description": "La requête de recherche."}
            },
            "required": ["query_text"]
        }
    },
    "randommer_query": {
        "description": "Génère des numéros de téléphone aléatoires via Randommer.io.",
        "parameters": {
            "type": "object",
            "properties": {
                "country_code": {"type": "string", "description": "Le code pays (ex: 'US', 'FR').", "default": "US"},
                "quantity": {"type": "integer", "description": "Le nombre de numéros à générer.", "default": 1}
            },
            "required": []
        }
    },
    "tomorrowio_query": {
        "description": "Récupère les prévisions météorologiques via Tomorrow.io.",
        "parameters": {
            "type": "object",
            "properties": {
                "location": {"type": "string", "description": "La localisation (nom de ville, code postal ou coordonnées)."},
                "fields": {"type": "array", "items": {"type": "string"}, "description": "Liste des champs météo à récupérer (ex: ['temperature', 'humidity']).", "default": ["temperature", "humidity", "windSpeed"]}
            },
            "required": ["location"]
        }
    },
    "openweathermap_query": {
        "description": "Récupère les conditions météorologiques actuelles pour une localisation via OpenWeatherMap.",
        "parameters": {
            "type": "object",
            "properties": {
                "location": {"type": "string", "description": "La ville ou le code postal pour la météo."}
            },
            "required": ["location"]
        }
    },
    "mockaroo_query": {
        "description": "Génère des données de test via Mockaroo.",
        "parameters": {
            "type": "object",
            "properties": {
                "count": {"type": "integer", "description": "Le nombre d'enregistrements à générer.", "default": 1},
                "fields_json": {"type": "string", "description": "Une chaîne JSON décrivant les champs à générer (ex: '[{\"name\":\"name\",\"type\":\"Full Name\"}]').", "nullable": True}
            },
            "required": []
        }
    },
    "openpagerank_query": {
        "description": "Récupère le PageRank de domaines via OpenPageRank.",
        "parameters": {
            "type": "object",
            "properties": {
                "domains": {"type": "array", "items": {"type": "string"}, "description": "Liste des noms de domaine à vérifier."}
            },
            "required": ["domains"]
        }
    },
    "rapidapi_query": {
        "description": "Interroge diverses APIs disponibles via RapidAPI (blagues, taux de change, faits aléatoires).",
        "parameters": {
            "type": "object",
            "properties": {
                "api_name": {"type": "string", "description": "Le nom de l'API RapidAPI à utiliser (ex: 'Programming Joke', 'Currency List Quotes', 'Random Fact').", "enum": ["Programming Joke", "Currency List Quotes", "Random Fact"]},
                "kwargs": {"type": "object", "description": "Arguments supplémentaires spécifiques à l'API RapidAPI appelée.", "additionalProperties": True}
            },
            "required": ["api_name"]
        }
    }
}

# ==============================================================================
# Paramètres du Chat et de la Mémoire
# ==============================================================================

# Longueur maximale de l'historique du chat à conserver en mémoire et sur disque
MAX_CHAT_HISTORY_LENGTH = 20

# ==============================================================================
# Paramètres des Checks de Santé des Endpoints
# ==============================================================================

# Activer ou désactiver les checks de santé périodiques des endpoints API
ENABLE_HEALTH_CHECKS = True

# Intervalle en secondes entre chaque exécution des checks de santé
HEALTH_CHECK_INTERVAL_SECONDS = 2700

import json
import logging
from datetime import datetime, timezone
from pathlib import Path
import re
import asyncio
import os
from typing import Any, Optional, Dict

# Import des constantes du fichier de configuration
from config import LOG_FILE, ERROR_LOG_PATH, BASE_DIR, MAX_FILE_SIZE, API_CONFIG, TOOL_CONFIG

# ==== Configuration du logging ====
# Configure le logger principal pour le bot
logger = logging.getLogger("bot_logger")
logger.setLevel(logging.INFO)

# Crée le répertoire de base si nécessaire
BASE_DIR.mkdir(parents=True, exist_ok=True)

# Gestionnaire pour le fichier de log principal
file_handler = logging.FileHandler(LOG_FILE)
file_handler.setLevel(logging.INFO)
formatter = logging.Formatter('%(asctime)s - %(levelname)s - %(message)s')
file_handler.setFormatter(formatter)
logger.addHandler(file_handler)

# Gestionnaire pour les erreurs critiques (fichier séparé)
error_file_handler = logging.FileHandler(ERROR_LOG_PATH)
error_file_handler.setLevel(logging.ERROR)
error_file_handler.setFormatter(formatter)
logger.addHandler(error_file_handler)

# Gestionnaire pour la console (logs en temps réel)
console_handler = logging.StreamHandler()
console_handler.setLevel(logging.INFO)
console_handler.setFormatter(formatter)
logger.addHandler(console_handler)

# Verrou pour les opérations de fichier asynchrones
_file_lock: Optional[asyncio.Lock] = None

def set_file_lock(lock: asyncio.Lock):
    """Définit l'instance du verrou asyncio pour les opérations de fichier."""
    global _file_lock
    _file_lock = lock

def log_message(message: str, level: str = "info"):
    """
    Enregistre un message dans le fichier de log et la console.
    Args:
        message (str): Le message à enregistrer.
        level (str): Le niveau de log ('debug', 'info', 'warning', 'error', 'critical').
    """
    if level == "debug":
        logger.debug(message)
    elif level == "info":
        logger.info(message)
    elif level == "warning":
        logger.warning(message)
    elif level == "error":
        logger.error(message)
    elif level == "critical":
        logger.critical(message)
    else:
        logger.info(f"Niveau de log inconnu '{level}': {message}")

def get_current_time() -> datetime:
    """Retourne l'heure actuelle en UTC."""
    return datetime.now(timezone.utc)

def format_datetime(dt: datetime) -> str:
    """Formate un objet datetime en chaîne de caractères lisible."""
    return dt.strftime("%Y-%m-%d %H:%M:%S UTC")

async def load_json(file_path: Path, default_value: Any = None) -> Any:
    """
    Charge les données d'un fichier JSON de manière asynchrone.
    Crée le fichier avec une valeur par défaut si inexistant.
    Args:
        file_path (Path): Le chemin du fichier JSON.
        default_value (Any): La valeur à retourner si le fichier n'existe pas ou est vide.
    Returns:
        Any: Le contenu du fichier JSON ou la valeur par défaut.
    """
    if _file_lock is None:
        log_message("Le verrou de fichier n'est pas initialisé dans utils.py. Initialisation par défaut.", level="warning")
        global _file_lock
        _file_lock = asyncio.Lock()

    try:
        if not file_path.exists():
            log_message(f"Fichier non trouvé: {file_path}. Création avec valeur par défaut.", level="info")
            await save_json(file_path, default_value if default_value is not None else {})
            return default_value if default_value is not None else {}
        
        async with _file_lock:
            return await asyncio.to_thread(_load_json_sync, file_path)
    except json.JSONDecodeError:
        log_message(f"Erreur de décodage JSON pour le fichier: {file_path}. Le fichier pourrait être corrompu. Retourne la valeur par défaut.", level="error")
        await save_json(file_path, default_value if default_value is not None else {})
        return default_value if default_value is not None else {}
    except Exception as e:
        log_message(f"Erreur inattendue lors du chargement du JSON {file_path}: {e}", level="error")
        return default_value if default_value is not None else {}

def _load_json_sync(file_path: Path) -> Any:
    """Fonction synchrone pour charger le JSON, appelée par asyncio.to_thread."""
    with open(file_path, 'r', encoding='utf-8') as f:
        return json.load(f)

async def save_json(file_path: Path, data: Any):
    """
    Sauvegarde les données dans un fichier JSON de manière asynchrone.
    Args:
        file_path (Path): Le chemin du fichier JSON.
        data (Any): Les données à sauvegarder.
    """
    if _file_lock is None:
        log_message("Le verrou de fichier n'est pas initialisé dans utils.py. Initialisation par défaut.", level="warning")
        global _file_lock
        _file_lock = asyncio.Lock()

    try:
        file_path.parent.mkdir(parents=True, exist_ok=True)
        
        async with _file_lock:
            await asyncio.to_thread(_save_json_sync, file_path, data)
        log_message(f"Données sauvegardées dans {file_path}", level="debug")
    except Exception as e:
        log_message(f"Erreur lors de la sauvegarde du JSON {file_path}: {e}", level="error")

def _save_json_sync(file_path: Path, data: Any):
    """Fonction synchrone pour sauvegarder le JSON, appelée par asyncio.to_thread."""
    with open(file_path, 'w', encoding='utf-8') as f:
        json.dump(data, f, indent=4)

def neutralize_urls(text: str) -> str:
    """
    Remplace les URLs dans le texte par une version neutralisée pour éviter les problèmes de sécurité
    ou les tentatives d'accès non désirées par le modèle.
    """
    url_pattern = re.compile(r'https?://[^\s/$.?#].[^\s]*', re.IGNORECASE)
    
    neutralized_text = url_pattern.sub("[LIEN_NEUTRALISÉ]", text)
    return neutralized_text

def find_tool_by_name(tool_name: str) -> Optional[Dict[str, Any]]:
    """
    Recherche un outil dans TOOL_CONFIG par son nom.
    Args:
        tool_name (str): Le nom de l'outil à rechercher.
    Returns:
        Optional[Dict[str, Any]]: Le dictionnaire de configuration de l'outil si trouvé, sinon None.
    """
    return TOOL_CONFIG.get(tool_name)

async def append_to_file(file_path: Path, content: str):
    """
    Ajoute du contenu à un fichier, en créant le fichier/répertoire si nécessaire.
    Gère la rotation du fichier si sa taille dépasse MAX_FILE_SIZE.
    """
    if _file_lock is None:
        log_message("Le verrou de fichier n'est pas initialisé dans utils.py. Initialisation par défaut.", level="warning")
        global _file_lock
        _file_lock = asyncio.Lock()

    file_path.parent.mkdir(parents=True, exist_ok=True)

    if file_path.exists() and file_path.stat().st_size + len(content.encode('utf-8')) > MAX_FILE_SIZE:
        rotate_file(file_path)

    async with _file_lock:
        await asyncio.to_thread(_append_to_file_sync, file_path, content)

def _append_to_file_sync(file_path: Path, content: str):
    """Fonction synchrone pour ajouter du contenu à un fichier."""
    with open(file_path, 'a', encoding='utf-8') as f:
        f.write(content + "\n")

def rotate_file(file_path: Path):
    """
    Effectue une rotation de fichier simple: renomme le fichier actuel avec un horodatage.
    """
    timestamp = datetime.now(timezone.utc).strftime("%Y%m%d_%H%M%S")
    new_path = file_path.parent / f"{file_path.stem}_{timestamp}{file_path.suffix}"
    try:
        os.rename(file_path, new_path)
        log_message(f"Fichier {file_path.name} renommé en {new_path.name} pour rotation.", level="info")
    except OSError as e:
        log_message(f"Erreur lors de la rotation du fichier {file_path.name}: {e}", level="error")

import time
import httpx
import json
import base64
import asyncio
import re 
import traceback
from typing import Dict, Any, Optional, Union, List, Tuple

# Import des constantes et fonctions utilitaires
from config import API_CONFIG, ENDPOINT_HEALTH_FILE, MAX_IMAGE_SIZE, GEMINI_TEMPERATURE, GEMINI_TOP_P, GEMINI_TOP_K, GEMINI_MAX_OUTPUT_TOKENS, GEMINI_SAFETY_SETTINGS
from utils import load_json, save_json, get_current_time, format_datetime, log_message, neutralize_urls

class EndpointHealthManager:
    """
    Gère la santé des endpoints API et sélectionne le meilleur endpoint disponible
    en fonction de critères comme la latence, le taux de succès et le nombre d'erreurs.
    C'est un singleton pour s'assurer qu'il n'y a qu'une seule instance de gestionnaire de santé.
    """
    _instance = None
    _initialized = False

    def __new__(cls, *args, **kwargs):
        """Implémente le patron de conception Singleton."""
        if cls._instance is None:
            cls._instance = super(cls, cls).__new__(cls)
        return cls._instance

    def __init__(self):
        """Initialise le gestionnaire."""
        if self._initialized:
            return
        self.health_status = {}

    async def init_manager(self):
        """
        Initialise le gestionnaire de santé de manière asynchrone.
        Charge l'état de santé persistant et s'assure que tous les endpoints sont suivis.
        """
        if not self._initialized:
            self.health_status = await load_json(ENDPOINT_HEALTH_FILE, {})
            self._initialize_health_status()
            self._initialized = True
            log_message("Gestionnaire de santé des endpoints initialisé.")

    def _initialize_health_status(self):
        """
        Initialise ou met à jour le statut de santé pour tous les endpoints configurés dans `API_CONFIG`.
        Ajoute les nouveaux endpoints et s'assure que toutes les clés nécessaires sont présentes.
        """
        updated = False
        for service_name, endpoints_config in API_CONFIG.items():
            if service_name not in self.health_status:
                self.health_status[service_name] = {}
                updated = True
            for endpoint_config in endpoints_config:
                endpoint_key = f"{endpoint_config['endpoint_name']}-{str(endpoint_config['key'])}"
                if endpoint_key not in self.health_status[service_name]:
                    self.health_status[service_name][endpoint_key] = {
                        "latency": 0.0,
                        "success_rate": 1.0,
                        "last_checked": None,
                        "error_count": 0,
                        "total_checks": 0,
                        "is_healthy": True
                    }
                    updated = True
        if updated:
            asyncio.create_task(save_json(ENDPOINT_HEALTH_FILE, self.health_status))
            log_message("Statut de santé des endpoints initialisé/mis à jour.")

    async def run_health_check_for_service(self, service_name: str):
        """
        Exécute des checks de santé pour tous les endpoints d'un service donné.
        Tente d'appeler l'endpoint avec des paramètres de santé prédéfinis.
        """
        endpoints_config = API_CONFIG.get(service_name)
        if not endpoints_config:
            log_message(f"Aucune configuration d'endpoint trouvée pour le service: {service_name}", level="warning")
            return

        log_message(f"Lancement du health check pour le service: {service_name}")
        for endpoint_config in endpoints_config:
            endpoint_key = f"{endpoint_config['endpoint_name']}-{str(endpoint_config['key'])}"
            start_time = time.monotonic()
            success = False
            try:
                request_method = endpoint_config.get("method", "GET")
                url = endpoint_config["url"]
                
                params = endpoint_config.get("health_check_params", endpoint_config.get("fixed_params", {})).copy()
                json_data = endpoint_config.get("health_check_json", endpoint_config.get("fixed_json", {})).copy()
                headers = endpoint_config.get("fixed_headers", {}).copy()
                auth = None
                
                check_timeout = endpoint_config.get("timeout", 5)

                if "health_check_url_suffix" in endpoint_config:
                    url += endpoint_config["health_check_url_suffix"]

                key_field = endpoint_config.get("key_field")
                key_location = endpoint_config.get("key_location")
                key_prefix = endpoint_config.get("key_prefix", "")
                api_key = endpoint_config["key"]

                if key_field and key_location:
                    if key_location == "param":
                        params[key_field] = api_key
                    elif key_location == "header":
                        headers[key_field] = f"{key_prefix}{api_key}"
                    elif key_location == "auth_basic":
                        if isinstance(api_key, tuple) and len(api_key) == 2:
                            auth = httpx.BasicAuth(api_key[0], api_key[1])
                        else:
                            log_message(f"Clé API pour auth_basic non valide pour {service_name}:{endpoint_key}", level="error")
                            success = False
                            continue

                async with httpx.AsyncClient(timeout=check_timeout) as client:
                    response = await client.request(request_method, url, params=params, headers=headers, json=json_data, auth=auth)
                    response.raise_for_status()
                    success = True
            except httpx.HTTPStatusError as e:
                log_level = "warning"
                if 400 <= e.response.status_code < 500 and e.response.status_code != 429:
                    log_level = "debug" 
                log_message(f"Health check pour {endpoint_key} ({service_name}) a échoué (HTTP {e.response.status_code}): {e.response.text}", level=log_level)
                success = False
            except httpx.RequestError as e:
                log_message(f"Health check pour {endpoint_key} ({service_name}) a échoué (Réseau): {e}", level="warning")
                success = False
            except Exception as e:
                log_message(f"Health check pour {endpoint_key} ({service_name}) a échoué (Inattendu): {e}", level="error")
                success = False
            finally:
                latency = time.monotonic() - start_time
                self.update_endpoint_health(service_name, endpoint_key, success, latency)
        log_message(f"Health check terminé pour le service: {service_name}")

    def update_endpoint_health(self, service_name: str, endpoint_key: str, success: bool, latency: float):
        """
        Met à jour le statut de santé d'un endpoint spécifique.
        Utilise une moyenne glissante pour le taux de succès et la latence.
        """
        if service_name not in self.health_status:
            self.health_status[service_name] = {}
        if endpoint_key not in self.health_status[service_name]:
            self.health_status[service_name][endpoint_key] = {
                "latency": 0.0,
                "success_rate": 1.0,
                "last_checked": None,
                "error_count": 0,
                "total_checks": 0,
                "is_healthy": True
            }

        status = self.health_status[service_name][endpoint_key]
        status["total_checks"] += 1
        status["last_checked"] = format_datetime(get_current_time())

        alpha = 0.1
        if success:
            status["error_count"] = max(0, status["error_count"] - 1)
            status["success_rate"] = status["success_rate"] * (1 - alpha) + 1.0 * alpha
            status["latency"] = status["latency"] * (1 - alpha) + latency * alpha
        else:
            status["error_count"] += 1
            status["success_rate"] = status["success_rate"] * (1 - alpha) + 0.0 * alpha
            status["latency"] = status["latency"] * (1 - alpha) + 10.0 * alpha 

        if status["error_count"] >= 3 or status["success_rate"] < 0.5:
            status["is_healthy"] = False
        else:
            status["is_healthy"] = True
        
        asyncio.create_task(save_json(ENDPOINT_HEALTH_FILE, self.health_status))
        log_message(f"Santé de {service_name}:{endpoint_key} mise à jour: Succès: {success}, Latence: {latency:.2f}s, Taux Succès: {status['success_rate']:.2f}, Sain: {status['is_healthy']}", level="debug" if not status["is_healthy"] else "info")

    def get_best_endpoint(self, service_name: str) -> Optional[Dict]:
        """
        Sélectionne le meilleur endpoint pour un service donné basé sur son statut de santé.
        Priorise les endpoints sains, puis les moins mauvais en cas d'absence d'endpoints sains.
        """
        service_health = self.health_status.get(service_name)
        if not service_health:
            log_message(f"Aucune donnée de santé pour le service {service_name}. Retourne None.", level="warning")
            return None

        best_endpoint_key = None
        best_score = -float('inf')

        healthy_endpoints = [
            (key, status) for key, status in service_health.items() if status["is_healthy"]
        ]

        if not healthy_endpoints:
            log_message(f"Aucun endpoint sain pour le service {service_name}. Tentative de sélection d'un endpoint non sain.", level="warning")
            all_endpoints = service_health.items()
            if not all_endpoints: 
                return None
            
            sorted_endpoints = sorted(all_endpoints, key=lambda item: (item[1]["error_count"], item[1]["latency"]))
            best_endpoint_key = sorted_endpoints[0][0]
            log_message(f"Fallback: Endpoint {best_endpoint_key} sélectionné pour {service_name} (non sain).", level="warning")
        else:
            for endpoint_key, status in healthy_endpoints:
                score = (status["success_rate"] * 100) - (status["latency"] * 10) - (status["error_count"] * 5)
                if score > best_score:
                    best_score = score
                    best_endpoint_key = endpoint_key
            log_message(f"Meilleur endpoint sélectionné pour {service_name}: {best_endpoint_key} (Score: {best_score:.2f})")

        if best_endpoint_key:
            for endpoint_config in API_CONFIG.get(service_name, []):
                current_endpoint_key = f"{endpoint_config['endpoint_name']}-{str(endpoint_config['key'])}"
                if current_endpoint_key == best_endpoint_key:
                    return endpoint_config
        return None

# Instancier le gestionnaire de santé des endpoints (sera initialisé dans main.py)
endpoint_health_manager = EndpointHealthManager()

def set_endpoint_health_manager_global(manager: EndpointHealthManager):
    """
    Permet d'injecter l'instance du gestionnaire de santé des endpoints.
    Ceci est utilisé pour s'assurer que tous les clients API utilisent la même instance.
    """
    global endpoint_health_manager
    endpoint_health_manager = manager

class APIClient:
    """
    Classe de base pour tous les clients API.
    Elle gère la sélection dynamique d'endpoints, les réessais en cas d'échec
    et l'intégration avec le gestionnaire de santé des endpoints.
    """
    def __init__(self, name: str, endpoint_health_manager: EndpointHealthManager):
        self.name = name
        self.endpoints_config = API_CONFIG.get(name, [])
        self.endpoint_health_manager = endpoint_health_manager
        if not self.endpoints_config:
            log_message(f"Client API {self.name} initialisé sans configuration d'endpoint.", level="error")

    async def _make_request(self, params: Optional[Dict] = None, headers: Optional[Dict] = None, 
                            json_data: Optional[Dict] = None, timeout: Optional[int] = None, 
                            max_retries: int = 3, initial_delay: float = 1.0, 
                            url: Optional[str] = None, method: Optional[str] = None, 
                            key_field: Optional[str] = None, key_location: Optional[str] = None, 
                            api_key: Optional[Union[str, Tuple[str, str]]] = None, 
                            fixed_params: Optional[Dict] = None, fixed_headers: Optional[Dict] = None, 
                            fixed_json: Optional[Dict] = None) -> Optional[Union[Dict, str, bytes]]:
        """
        Méthode interne pour effectuer les requêtes HTTP en utilisant le meilleur endpoint avec réessais.
        """
        
        selected_endpoint_config = None
        endpoint_key_for_health = "Dynamic"

        if url and method:
            selected_endpoint_config = {
                "url": url,
                "method": method,
                "key_field": key_field,
                "key_location": key_location,
                "key": api_key,
                "fixed_params": fixed_params if fixed_params is not None else {},
                "fixed_headers": fixed_headers if fixed_headers is not None else {},
                "fixed_json": fixed_json if fixed_json is not None else {},
                "endpoint_name": "Dynamic",
                "timeout": timeout if timeout is not None else 30
            }
            if api_key:
                endpoint_key_for_health = f"Dynamic-{str(api_key)}"
            log_message(f"Requête dynamique pour {self.name} vers {url}")
        else:
            selected_endpoint_config = self.endpoint_health_manager.get_best_endpoint(self.name)
            if not selected_endpoint_config:
                log_message(f"Aucun endpoint sain ou disponible pour {self.name}.", level="error")
                return {"error": True, "message": f"Aucun endpoint sain ou disponible pour {self.name}."}
            endpoint_key_for_health = f"{selected_endpoint_config['endpoint_name']}-{str(selected_endpoint_config['key'])}"
            log_message(f"Endpoint sélectionné pour {self.name}: {selected_endpoint_config['endpoint_name']}")
            timeout = timeout if timeout is not None else selected_endpoint_config.get("timeout", 30)

        url_to_use = selected_endpoint_config["url"]
        method_to_use = selected_endpoint_config["method"]

        request_params = selected_endpoint_config.get("fixed_params", {}).copy()
        request_headers = selected_endpoint_config.get("fixed_headers", {}).copy()
        request_json_data = selected_endpoint_config.get("fixed_json", {}).copy()
        auth = None

        if params:
            request_params.update(params)
        if headers:
            request_headers.update(headers)
        if json_data:
            request_json_data.update(json_data)

        key_field_to_use = selected_endpoint_config.get("key_field")
        key_location_to_use = selected_endpoint_config.get("key_location")
        key_prefix = selected_endpoint_config.get("key_prefix", "")
        api_key_to_use = selected_endpoint_config["key"]

        if key_field_to_use and key_location_to_use:
            if key_location_to_use == "param":
                request_params[key_field_to_use] = api_key_to_use
            elif key_location_to_use == "header":
                request_headers[key_field_to_use] = f"{key_prefix}{api_key_to_use}"
            elif key_location_to_use == "auth_basic":
                if isinstance(api_key_to_use, tuple) and len(api_key_to_use) == 2:
                    auth = httpx.BasicAuth(api_key_to_use[0], api_key_to_use[1])
                else:
                    log_message(f"Clé API pour auth_basic non valide pour {self.name}:{endpoint_key_for_health}", level="error")
                    self.endpoint_health_manager.update_endpoint_health(self.name, endpoint_key_for_health, False, 0.0)
                    return {"error": True, "message": "Configuration d'authentification basique invalide."}

        current_delay = initial_delay
        for attempt in range(max_retries):
            start_time = time.monotonic()
            success = False
            try:
                async with httpx.AsyncClient(timeout=timeout) as client:
                    response = await client.request(method_to_use, url_to_use, params=request_params, headers=request_headers, json=request_json_data, auth=auth)
                    response.raise_for_status()
                    success = True
                    
                    content_type = response.headers.get("Content-Type", "").lower()
                    if "application/json" in content_type:
                        try:
                            return response.json()
                        except json.JSONDecodeError:
                            log_message(f"API {self.name} réponse non JSON valide (tentative {attempt+1}/{max_retries}): {response.text[:200]}...", level="warning")
                            if attempt < max_retries - 1:
                                await asyncio.sleep(current_delay)
                                current_delay *= 2
                                continue
                            return {"error": True, "message": "Réponse API non JSON valide.", "raw_response": response.text}
                    else:
                        log_message(f"API {self.name} a renvoyé un Content-Type non JSON: {content_type}", level="info")
                        return response.content

            except httpx.HTTPStatusError as e:
                log_message(f"API {self.name} erreur HTTP (tentative {attempt+1}/{max_retries}): {e.response.status_code} - {e.response.text}", level="warning")
                if 400 <= e.response.status_code < 500 and e.response.status_code != 429:
                    log_message(f"API {self.name}: Erreur client {e.response.status_code}, pas de réessai.", level="error")
                    self.endpoint_health_manager.update_endpoint_health(self.name, endpoint_key_for_health, False, e.response.elapsed.total_seconds())
                    return {"error": True, "status_code": e.response.status_code, "message": e.response.text}
                
                if attempt < max_retries - 1:
                    log_message(f"API {self.name}: Réessai dans {current_delay:.2f}s...", level="info")
                    await asyncio.sleep(current_delay)
                    current_delay *= 2
            except httpx.RequestError as e:
                log_message(f"API {self.name} erreur de requête (tentative {attempt+1}/{max_retries}): {e}", level="warning")
                if attempt < max_retries - 1:
                    log_message(f"API {self.name}: Réessai dans {current_delay:.2f}s...", level="info")
                    await asyncio.sleep(current_delay)
                    current_delay *= 2
            except Exception as e:
                log_message(f"API {self.name} erreur inattendue (tentative {attempt+1}/{max_retries}): {e}", level="error")
                self.endpoint_health_manager.update_endpoint_health(self.name, endpoint_key_for_health, False, time.monotonic() - start_time)
                return {"error": True, "message": str(e)}
            finally:
                if not success:
                    latency = time.monotonic() - start_time
                    self.endpoint_health_manager.update_endpoint_health(self.name, endpoint_key_for_health, False, latency)
        
        log_message(f"API {self.name}: Toutes les tentatives ont échoué après {max_retries} réessais.", level="error")
        return {"error": True, "message": f"Échec de la requête après {max_retries} tentatives."}

    async def query(self, *args, **kwargs) -> Any:
        """
        Méthode abstraite pour interroger l'API.
        Doit être implémentée par chaque sous-classe de client API.
        """
        raise NotImplementedError("La méthode query doit être implémentée par les sous-classes.")

# --- Clients API Spécifiques ---

class GeminiAPIClient(APIClient):
    """Client pour l'API Gemini, hérite de APIClient pour la gestion de santé."""
    def __init__(self):
        super().__init__("GEMINI_API", endpoint_health_manager)
        self.model_name = "gemini-1.5-flash-latest"
        self.generation_config = {
            "temperature": GEMINI_TEMPERATURE,
            "top_p": GEMINI_TOP_P,
            "top_k": GEMINI_TOP_K,
            "max_output_tokens": GEMINI_MAX_OUTPUT_TOKENS,
        }
        self.safety_settings = GEMINI_SAFETY_SETTINGS
        log_message(f"GeminiApiClient initialisé avec le modèle par défaut: {self.model_name}")

    async def generate_content(self, prompt: str, chat_history: List[Dict], image_data: Optional[str] = None, model: Optional[str] = None, tools: Optional[List[Dict]] = None) -> Union[Dict, str]:
        """Génère du contenu textuel ou multimodal en utilisant l'API Gemini."""
        model_to_use = model if model else self.model_name
        
        contents = []
        for msg in chat_history:
            role = "user" if msg["role"] == "user" else "model"
            contents.append({"role": role, "parts": msg["parts"]})

        if contents and contents[-1]["role"] == "user":
            contents[-1]["parts"].append({"text": prompt})
        else:
            contents.append({"role": "user", "parts": [{"text": prompt}]})

        if image_data:
            if "," in image_data:
                mime_type_part, base64_data = image_data.split(",", 1)
                mime_type = mime_type_part.split(":", 1)[1].split(";", 1)[0]
            else:
                mime_type = "image/jpeg" 
                base64_data = image_data

            if contents and contents[-1]["role"] == "user":
                contents[-1]["parts"].append({
                    "inlineData": {
                        "mimeType": mime_type,
                        "data": base64_data
                    }
                })
                log_message(f"Image ajoutée au prompt Gemini (mimeType: {mime_type}).")
            else:
                log_message("Impossible d'ajouter l'image au prompt Gemini: le dernier message n'est pas un utilisateur.", level="warning")

        payload = {
            "contents": contents,
            "generationConfig": self.generation_config,
            "safetySettings": self.safety_settings
        }

        if tools:
            payload["tools"] = tools

        log_message(f"Appel à Gemini API pour le modèle {model_to_use}...")
        
        # L'URL de l'endpoint Gemini peut varier en fonction du modèle.
        # On prend l'URL de base du premier endpoint configuré et on y ajoute le modèle.
        base_url_from_config = self.endpoints_config[0]["url"].split(':generateContent')[0]
        dynamic_url = f"{base_url_from_config}:{model_to_use}:generateContent"

        # Les headers et la clé API seront gérés par _make_request via la sélection d'endpoint
        response = await self._make_request(
            url=dynamic_url,
            method="POST",
            json_data=payload,
            timeout=60 # Utilise le timeout de la méthode _make_request
        )

        if response and not response.get("error"):
            return response
        return f"❌ Erreur Gemini: {response.get('message', 'Inconnu')}" if response else "❌ Erreur Gemini: Réponse vide ou erreur interne."

class OCRApiClient(APIClient):
    """Client pour l'API OCR.space, hérite de APIClient pour la gestion de santé."""
    def __init__(self):
        super().__init__("OCR_API", endpoint_health_manager)
        log_message("OCRApiClient initialisé.")

    async def query(self, image_base64: str) -> str:
        """
        Effectue une requête OCR à l'API OCR.space.
        `image_base64` doit être la chaîne base64 de l'image, incluant le préfixe mimeType.
        """
        payload = {
            "base64Image": image_base64,
            "language": "fre",
            "isOverlayRequired": False,
            "OCREngine": 2
        }
        
        # Les headers et la clé API seront gérés par _make_request via la sélection d'endpoint
        log_message("Appel à OCR.space API...")
        response = await self._make_request(
            json_data=payload,
            method="POST",
            timeout=30
        )

        if response and not response.get("error"):
            if response.get("IsErroredOnProcessing"):
                error_message = response.get("ErrorMessage", ["Erreur inconnue lors du traitement OCR."])
                log_message(f"Erreur OCR.space: {error_message}", level="error")
                return f"❌ Erreur OCR: {', '.join(error_message)}"
            
            parsed_text = ""
            if "ParsedResults" in response and response["ParsedResults"]:
                for parsed_result in response["ParsedResults"]:
                    parsed_text += parsed_result.get("ParsedText", "") + "\n"
            
            if parsed_text.strip():
                log_message("OCR.space: Texte extrait avec succès.")
                return parsed_text.strip()
            else:
                log_message("OCR.space: Aucun texte extrait.", level="warning")
                return "Aucun texte n'a pu être extrait de l'image."
        return f"❌ Erreur OCR: {response.get('message', 'Inconnu')}" if response else "❌ Erreur OCR: Réponse vide ou erreur interne."

class DeepSeekClient(APIClient):
    def __init__(self):
        super().__init__("DEEPSEEK", endpoint_health_manager)

    async def query(self, prompt: Union[str, List[Dict]], model: str = "deepseek-chat") -> str:
        """Interroge l'API DeepSeek pour des complétions de chat."""
        if isinstance(prompt, str):
            messages = [{"role": "user", "content": prompt}]
        else:
            messages = prompt

        payload = {"model": model, "messages": messages}
        response = await self._make_request(json_data=payload)
        if response and not response.get("error"):
            content = response.get("choices", [{}])[0].get("message", {}).get("content")
            if content:
                return content
            return "DeepSeek: Pas de contenu de réponse trouvé."
        return f"DeepSeek: Erreur: {response.get('message', 'Inconnu')}" if response else "DeepSeek: Réponse vide ou erreur interne."

class SerperClient(APIClient):
    def __init__(self):
        super().__init__("SERPER", endpoint_health_manager)

    async def query(self, query_text: str) -> str:
        """Effectue une recherche web via l'API Serper."""
        payload = {"q": query_text}
        response = await self._make_request(json_data=payload)
        if response and not response.get("error"):
            organic_results = response.get("organic", [])
            if organic_results:
                snippet = organic_results[0].get("snippet", "Pas de snippet.")
                link = organic_results[0].get("link", "")
                return f"Serper (recherche web):\n{snippet} {neutralize_urls(link)}"
            return "Serper: Aucune information trouvée."
        return f"Serper: Erreur: {response.get('message', 'Inconnu')}" if response else "Serper: Réponse vide ou erreur interne."

class WolframAlphaClient(APIClient):
    def __init__(self):
        super().__init__("WOLFRAMALPHA", endpoint_health_manager)

    async def query(self, input_text: str) -> str:
        """Interroge WolframAlpha pour des calculs ou des faits."""
        params = {"input": input_text}
        response = await self._make_request(params=params)
        if response and not response.get("error"):
            pods = response.get("queryresult", {}).get("pods", [])
            if pods:
                for pod in pods:
                    if pod.get("title") in ["Result", "Input interpretation", "Decimal approximation"]:
                        subpods = pod.get("subpods", [])
                        if subpods and subpods[0].get("plaintext"):
                            return f"WolframAlpha:\n{subpods[0]['plaintext']}"
                if pods and pods[0].get("subpods") and pods[0]["subpods"][0].get("plaintext"):
                    return f"WolframAlpha:\n{pods[0]['subpods'][0]['plaintext']}"
            return "WolframAlpha: Pas de résultat clair."
        return f"WolframAlpha: Erreur: {response.get('message', 'Inconnu')}" if response else "WolframAlpha: Réponse vide ou erreur interne."

class TavilyClient(APIClient):
    def __init__(self):
        super().__init__("TAVILY", endpoint_health_manager)

    async def query(self, query_text: str, max_results: int = 3) -> str:
        """Effectue une recherche web avancée via l'API Tavily."""
        payload = {"query": query_text, "max_results": max_results}
        response = await self._make_request(json_data=payload)
        if response and not response.get("error"):
            results = response.get("results", [])
            answer = response.get("answer", "Aucune réponse directe trouvée.")

            output = f"Tavily (recherche web):\nRéponse directe: {answer}\n"
            if results:
                output += "Extraits pertinents:\n"
                for i, res in enumerate(results[:max_results]):
                    output += f"- {res.get('title', 'N/A')}: {res.get('content', 'N/A')} {neutralize_urls(res.get('url', ''))}\n"
            return output
        return f"Tavily: Erreur: {response.get('message', 'Inconnu')}" if response else "Tavily: Réponse vide ou erreur interne."

class ApiFlashClient(APIClient):
    def __init__(self):
        super().__init__("APIFLASH", endpoint_health_manager)

    async def query(self, url: str) -> str:
        """Capture une capture d'écran d'une URL via ApiFlash."""
        params = {"url": url, "format": "jpeg", "full_page": "true"}
        response_content = await self._make_request(params=params)

        if isinstance(response_content, bytes):
            selected_endpoint_config = self.endpoint_health_manager.get_best_endpoint(self.name)
            if selected_endpoint_config:
                capture_url = f"{selected_endpoint_config['url']}?access_key={selected_endpoint_config['key']}&url={url}&format=jpeg&full_page=true"
                return f"ApiFlash (capture d'écran): {neutralize_urls(capture_url)} (Vérifiez le lien pour l'image)"
            return "ApiFlash: Impossible de générer l'URL de capture."
        elif isinstance(response_content, dict) and response_content.get("error"):
            return f"ApiFlash: Erreur: {response_content.get('message', 'Inconnu')}"
        else:
            log_message(f"ApiFlash a renvoyé un type de réponse inattendu: {type(response_content)}", level="warning")
            return f"ApiFlash: Réponse inattendue de l'API. {response_content}"

class CrawlbaseClient(APIClient):
    def __init__(self):
        super().__init__("CRAWLBASE", endpoint_health_manager)

    async def query(self, url: str, use_js: bool = False) -> str:
        """Scrape le contenu HTML ou JavaScript d'une URL via Crawlbase."""
        params = {"url": url, "format": "json"}
        
        selected_endpoint_config = None
        if use_js:
            for config in API_CONFIG.get(self.name, []):
                if "JS Scraper" in config.get("endpoint_name", ""):
                    selected_endpoint_config = config
                    break
        
        if not selected_endpoint_config: 
            selected_endpoint_config = self.endpoint_health_manager.get_best_endpoint(self.name)

        if not selected_endpoint_config:
            return f"Crawlbase: Aucun endpoint sain ou disponible pour {self.name}."

        response = await self._make_request(
            params=params,
            url=selected_endpoint_config["url"],
            method=selected_endpoint_config["method"],
            key_field=selected_endpoint_config["key_field"],
            key_location=selected_endpoint_config["key_location"],
            api_key=selected_endpoint_config["key"],
            fixed_params=selected_endpoint_config.get("fixed_params", {}),
            timeout=selected_endpoint_config.get("timeout")
        )

        if response and not response.get("error"):
            body = response.get("body")
            if body:
                try:
                    decoded_body = base64.b64decode(body).decode('utf-8', errors='ignore')
                    return f"Crawlbase (contenu web):\n{decoded_body[:1000]}..."
                except Exception:
                    return f"Crawlbase (contenu web - brut):\n{body[:1000]}..."
            return "Crawlbase: Contenu non trouvé."
        return f"Crawlbase: Erreur: {response.get('message', 'Inconnu')}" if response else "Crawlbase: Réponse vide ou erreur interne."

class DetectLanguageClient(APIClient):
    def __init__(self):
        super().__init__("DETECTLANGUAGE", endpoint_health_manager)

    async def query(self, text: str) -> str:
        """Détecte la langue d'un texte via DetectLanguage API."""
        payload = {"q": text}
        response = await self._make_request(json_data=payload)
        if response and not response.get("error"):
            detections = response.get("data", {}).get("detections", [])
            if detections:
                first_detection = detections[0]
                lang = first_detection.get("language")
                confidence = first_detection.get("confidence")
                return f"Langue détectée: {lang} (confiance: {confidence})"
            return "DetectLanguage: Aucune langue détectée."
        return f"DetectLanguage: Erreur: {response.get('message', 'Inconnu')}" if response else "DetectLanguage: Réponse vide ou erreur interne."

class GuardianClient(APIClient):
    def __init__(self):
        super().__init__("GUARDIAN", endpoint_health_manager)

    async def query(self, query_text: str) -> str:
        """Recherche des articles de presse via l'API The Guardian."""
        params = {"q": query_text}
        response = await self._make_request(params=params)
        if response and not response.get("error"):
            results = response.get("response", {}).get("results", [])
            if results:
                output = "Articles The Guardian:\n"
                for res in results[:3]:
                    output += f"- {res.get('webTitle', 'N/A')}: {res.get('fields', {}).get('trailText', 'N/A')} {neutralize_urls(res.get('webUrl', ''))}\n"
                return output
            return "Guardian: Aucun article trouvé."
        return f"Guardian: Erreur: {response.get('message', 'Inconnu')}" if response else "Guardian: Réponse vide ou erreur interne."

class IP2LocationClient(APIClient):
    def __init__(self):
        super().__init__("IP2LOCATION", endpoint_health_manager)

    async def query(self, ip_address: str) -> str:
        """Géolocalise une adresse IP via IP2Location API."""
        params = {"ip": ip_address}
        response = await self._make_request(params=params)
        if response and not response.get("error"):
            if "country_name" in response:
                return f"IP2Location (Géolocalisation IP {ip_address}): Pays: {response['country_name']}, Ville: {response.get('city_name', 'N/A')}"
            return "IP2Location: Informations non trouvées."
        return f"IP2Location: Erreur: {response.get('message', 'Inconnu')}" if response else "IP2Location: Réponse vide ou erreur interne."

class ShodanClient(APIClient):
    def __init__(self):
        super().__init__("SHODAN", endpoint_health_manager)

    async def query(self, query_text: str = "") -> str:
        """
        Interroge Shodan pour des informations sur un hôte IP ou des informations sur la clé API.
        Si `query_text` est une IP, tente de récupérer les infos de l'hôte.
        Sinon, ou en cas d'échec, retourne les infos de la clé API.
        """
        if re.match(r"^\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}$", query_text):
            selected_endpoint_config = None
            for config in API_CONFIG.get(self.name, []):
                if "Host Info" in config.get("endpoint_name", ""):
                    selected_endpoint_config = config
                    break
            if selected_endpoint_config:
                url = f"{selected_endpoint_config['url'].rstrip('/')}/{query_text}"
                response = await self._make_request(
                    params={"key": selected_endpoint_config["key"]},
                    url=url,
                    method="GET",
                    key_field=selected_endpoint_config["key_field"],
                    key_location=selected_endpoint_config["key_location"],
                    api_key=selected_endpoint_config["key"],
                    timeout=selected_endpoint_config.get("timeout")
                )
                if response and not response.get("error"):
                    return f"Shodan (info hôte {query_text}): Pays: {response.get('country_name', 'N/A')}, Ports: {response.get('ports', 'N/A')}, Vulnérabilités: {response.get('vulns', 'Aucune')}"
                return f"Shodan (info hôte): Erreur: {response.get('message', 'Inconnu')}" if response else "Shodan: Réponse vide ou erreur interne."
            else:
                return "Shodan: Endpoint 'Host Info' non configuré."
        else:
            response = await self._make_request()
            if response and not response.get("error"):
                return f"Shodan (info clé): Requêtes restantes: {response.get('usage_limits', {}).get('query_credits', 'N/A')}, Scan crédits: {response.get('usage_limits', {}).get('scan_credits', 'N/A')}"
            return f"Shodan: Erreur: {response.get('message', 'Inconnu')}" if response else "Shodan: Réponse vide ou erreur interne."

class WeatherAPIClient(APIClient):
    def __init__(self):
        super().__init__("WEATHERAPI", endpoint_health_manager)

    async def query(self, location: str) -> str:
        """Récupère les conditions météorologiques actuelles pour une localisation via WeatherAPI."""
        params = {"q": location}
        response = await self._make_request(params=params)
        if response and not response.get("error"):
            current = response.get("current", {})
            location_info = response.get("location", {})
            if current and location_info:
                return (
                    f"Météo à {location_info.get('name', 'N/A')}, {location_info.get('country', 'N/A')}:\n"
                    f"Température: {current.get('temp_c', 'N/A')}°C, "
                    f"Conditions: {current.get('condition', {}).get('text', 'N/A')}, "
                    f"Vent: {current.get('wind_kph', 'N/A')} km/h"
                )
            return "WeatherAPI: Données météo non trouvées."
        return f"WeatherAPI: Erreur: {response.get('message', 'Inconnu')}" if response else "WeatherAPI: Réponse vide ou erreur interne."

class CloudmersiveClient(APIClient):
    def __init__(self):
        super().__init__("CLOUDMERSIVE", endpoint_health_manager)

    async def query(self, domain: str) -> str:
        """Vérifie la validité et le type d'un domaine via Cloudmersive API."""
        payload = {"domain": domain}
        response = await self._make_request(json_data=payload)
        if response and not response.get("error"):
            return f"Cloudmersive (vérification de domaine {domain}): Valide: {response.get('ValidDomain', 'N/A')}, Type: {response.get('DomainType', 'N/A')}"
        return f"Cloudmersive: Erreur: {response.get('message', 'Inconnu')}" if response else "Cloudmersive: Réponse vide ou erreur interne."

class GreyNoiseClient(APIClient):
    def __init__(self):
        super().__init__("GREYNOISE", endpoint_health_manager)

    async def query(self, ip_address: str) -> str:
        """Analyse une adresse IP pour détecter des activités 'bruit' (malveillantes) via GreyNoise."""
        selected_endpoint_config = self.endpoint_health_manager.get_best_endpoint(self.name)
        if not selected_endpoint_config:
            return f"GreyNoise: Aucun endpoint sain ou disponible pour {self.name}."

        url = f"{selected_endpoint_config['url'].rstrip('/')}/{ip_address}"
        method = selected_endpoint_config["method"]
        headers = {selected_endpoint_config["key_field"]: selected_endpoint_config["key"]}

        response = await self._make_request(
            headers=headers,
            url=url,
            method=method,
            key_field=selected_endpoint_config["key_field"],
            key_location=selected_endpoint_config["key_location"],
            api_key=selected_endpoint_config["key"],
            timeout=selected_endpoint_config.get("timeout")
        )

        if response and not response.get("error"):
            if response.get("noise"):
                return f"GreyNoise (IP {ip_address}): C'est une IP 'bruit' (malveillante). Classification: {response.get('classification', 'N/A')}, Nom d'acteur: {response.get('actor', 'N/A')}"
            return f"GreyNoise (IP {ip_address}): Pas de 'bruit' détecté. Statut: {response.get('status', 'N/A')}"
        return f"GreyNoise: Erreur: {response.get('message', 'Inconnu')}" if response else "GreyNoise: Réponse vide ou erreur interne."

class PulsediveClient(APIClient):
    def __init__(self):
        super().__init__("PULSEDIVE", endpoint_health_manager)

    async def query(self, indicator: str, type: str = "auto") -> str:
        """Analyse un indicateur de menace (IP, domaine, URL) via Pulsedive."""
        params = {"indicator": indicator, "type": type}
        response = await self._make_request(params=params)
        if response and not response.get("error"):
            if response.get("results"):
                result = response["results"][0]
                return (
                    f"Pulsedive (Analyse {indicator}): Type: {result.get('type', 'N/A')}, "
                    f"Risk: {result.get('risk', 'N/A')}, "
                    f"Description: {result.get('description', 'N/A')[:200]}..."
                )
            return "Pulsedive: Aucun résultat d'analyse trouvé."
        return f"Pulsedive: Erreur: {response.get('message', 'Inconnu')}" if response else "Pulsedive: Réponse vide ou erreur interne."

class StormGlassClient(APIClient):
    def __init__(self):
        super().__init__("STORMGLASS", endpoint_health_manager)

    async def query(self, lat: float, lng: float, params: str = "airTemperature,waveHeight") -> str:
        """Récupère les données météorologiques maritimes pour une coordonnée via StormGlass."""
        now = int(time.time())
        request_params = {
            "lat": lat,
            "lng": lng,
            "params": params,
            "start": now,
            "end": now + 3600
        }
        response = await self._make_request(params=request_params)
        if response and not response.get("error"):
            data = response.get("hours", [])
            if data:
                first_hour = data[0]
                temp = first_hour.get('airTemperature', [{}])[0].get('value', 'N/A')
                wave_height = first_hour.get('waveHeight', [{}])[0].get('value', 'N/A')
                return f"StormGlass (Météo maritime à {lat},{lng}): Température air: {temp}°C, Hauteur vagues: {wave_height}m"
            return "StormGlass: Données non trouvées."
        return f"StormGlass: Erreur: {response.get('message', 'Inconnu')}" if response else "StormGlass: Réponse vide ou erreur interne."

class LoginRadiusClient(APIClient):
    def __init__(self):
        super().__init__("LOGINRADIUS", endpoint_health_manager)

    async def query(self) -> str:
        """Effectue un simple ping à l'API LoginRadius pour vérifier sa disponibilité."""
        response = await self._make_request()
        if response and not response.get("error"):
            return f"LoginRadius (Ping API): Statut: {response.get('Status', 'N/A')}, Message: {response.get('Message', 'N/A')}"
        return f"LoginRadius: Erreur: {response.get('message', 'Inconnu')}" if response else "LoginRadius: Réponse vide ou erreur interne."

class JsonbinClient(APIClient):
    def __init__(self):
        super().__init__("JSONBIN", endpoint_health_manager)

    async def query(self, data: Optional[Dict[str, Any]] = None, private: bool = True, bin_id: Optional[str] = None) -> str:
        """
        Crée un nouveau 'bin' JSON ou accède à un bin existant via Jsonbin.io.
        `data` est pour la création, `bin_id` pour l'accès.
        """
        if bin_id:
            selected_endpoint_config = None
            for config in API_CONFIG.get(self.name, []):
                if "Bin Access" in config.get("endpoint_name", ""):
                    selected_endpoint_config = config
                    break
            if not selected_endpoint_config:
                return f"Jsonbin: Aucun endpoint d'accès de bin sain ou disponible pour {self.name}."

            url = f"{selected_endpoint_config['url'].rstrip('/')}/{bin_id}"
            method = "GET"
            headers = {selected_endpoint_config["key_field"]: selected_endpoint_config["key"]}
            
            response = await self._make_request(
                headers=headers,
                url=url,
                method=method,
                timeout=selected_endpoint_config.get("timeout")
            )
            if response and not response.get("error"):
                return f"Jsonbin (Accès bin {bin_id}):\n{json.dumps(response, indent=2)}"
            return f"Jsonbin (Accès bin): Erreur: {response.get('message', 'Inconnu')}" if response else "Jsonbin: Réponse vide ou erreur interne."
        
        else:
            selected_endpoint_config = None
            for config in API_CONFIG.get(self.name, []):
                if "Bin Create" in config.get("endpoint_name", ""):
                    selected_endpoint_config = config
                    break
            
            if not selected_endpoint_config:
                return f"Jsonbin: Aucun endpoint de création de bin sain ou disponible pour {self.name}."

            url = selected_endpoint_config["url"]
            method = "POST"
            headers = {selected_endpoint_config["key_field"]: selected_endpoint_config["key"], "Content-Type": "application/json"}
            payload = {"record": data if data is not None else {}, "private": private}

            response = await self._make_request(
                json_data=payload,
                headers=headers,
                url=url,
                method=method,
                timeout=selected_endpoint_config.get("timeout")
            )

            if response and not response.get("error"):
                return f"Jsonbin (Création de bin): ID: {response.get('metadata', {}).get('id', 'N/A')}, URL: {neutralize_urls(response.get('metadata', {}).get('url', 'N/A'))}"
            return f"Jsonbin (Création de bin): Erreur: {response.get('message', 'Inconnu')}" if response else "Jsonbin: Réponse vide ou erreur interne."

class HuggingFaceClient(APIClient):
    def __init__(self):
        super().__init__("HUGGINGFACE", endpoint_health_manager)

    async def query(self, model_name: str = "distilbert-base-uncased-finetuned-sst-2-english", input_text: str = "Hello world") -> str:
        """Effectue une inférence sur un modèle HuggingFace (ex: classification de texte, génération)."""
        selected_endpoint_config = self.endpoint_health_manager.get_best_endpoint(self.name)
        if not selected_endpoint_config:
            return f"HuggingFace: Aucun endpoint sain ou disponible pour {self.name}."

        inference_url = f"https://api-inference.huggingface.co/models/{model_name}"
        
        headers = {
            selected_endpoint_config["key_field"]: f"{selected_endpoint_config['key_prefix']}{selected_endpoint_config['key']}",
            "Content-Type": "application/json"
        }
        payload = {"inputs": input_text}

        response = await self._make_request(
            json_data=payload,
            headers=headers,
            url=inference_url,
            method="POST",
            timeout=selected_endpoint_config.get("timeout")
        )

        if response and not response.get("error"):
            if isinstance(response, list) and response:
                first_result = response[0]
                if isinstance(first_result, list) and first_result:
                    return f"HuggingFace ({model_name} - {first_result[0].get('label')}): Score {first_result[0].get('score', 'N/A'):.2f}"
                elif isinstance(first_result, dict) and "generated_text" in first_result:
                    return f"HuggingFace ({model_name}): {first_result.get('generated_text')}"
            return f"HuggingFace ({model_name}): Réponse non parsée. {response}"
        return f"HuggingFace: Erreur: {response.get('message', 'Inconnu')}" if response else "HuggingFace: Réponse vide ou erreur interne."

class TwilioClient(APIClient):
    def __init__(self):
        super().__init__("TWILIO", endpoint_health_manager)

    async def query(self) -> str:
        """Récupère le solde du compte Twilio."""
        selected_endpoint_config = None
        for config in API_CONFIG.get(self.name, []):
            if "Account Balance" in config.get("endpoint_name", ""):
                selected_endpoint_config = config
                break
        if not selected_endpoint_config:
            if self.endpoints_config:
                selected_endpoint_config = self.endpoints_config[0]
            else:
                return f"Twilio: Aucune configuration d'endpoint disponible pour {self.name}."

        response = await self._make_request(
            url=selected_endpoint_config["url"],
            method=selected_endpoint_config["method"],
            key_location=selected_endpoint_config["key_location"],
            api_key=selected_endpoint_config["key"],
            timeout=selected_endpoint_config.get("timeout")
        )
        if response and not response.get("error"):
            return f"Twilio (Balance): {response.get('balance', 'N/A')} {response.get('currency', 'N/A')}"
        return f"Twilio: Erreur: {response.get('message', 'Inconnu')}" if response else "Twilio: Réponse vide ou erreur interne."

class AbstractAPIClient(APIClient):
    def __init__(self):
        super().__init__("ABSTRACTAPI", endpoint_health_manager)

    async def query(self, input_value: str, api_type: str) -> str:
        """
        Interroge diverses APIs d'AbstractAPI (validation email/téléphone, taux de change, jours fériés).
        `input_value` dépend du `api_type`.
        """
        params = {}
        target_endpoint_name = ""

        if api_type == "PHONE_VALIDATION":
            params["phone"] = input_value
            target_endpoint_name = "Phone Validation"
        elif api_type == "EMAIL_VALIDATION":
            params["email"] = input_value
            target_endpoint_name = "Email Validation"
        elif api_type == "EXCHANGE_RATES":
            params["base"] = input_value if input_value else "USD" 
            target_endpoint_name = "Exchange Rates"
        elif api_type == "HOLIDAYS":
            params["country"] = input_value if input_value else "US"
            from datetime import datetime
            params["year"] = datetime.now(timezone.utc).year
            target_endpoint_name = "Holidays"
        else:
            return f"AbstractAPI: Type d'API '{api_type}' non supporté pour la requête."

        selected_endpoint_config = None
        for config in API_CONFIG.get(self.name, []):
            if target_endpoint_name in config["endpoint_name"]:
                selected_endpoint_config = config
                break
        
        if not selected_endpoint_config:
            return f"AbstractAPI: Aucun endpoint sain ou disponible pour {self.name} pour le type {api_type}."

        response = await self._make_request(
            params=params,
            url=selected_endpoint_config["url"],
            method=selected_endpoint_config["method"],
            key_field=selected_endpoint_config["key_field"],
            key_location=selected_endpoint_config["key_location"],
            api_key=selected_endpoint_config["key"],
            fixed_params=selected_endpoint_config.get("fixed_params", {}),
            timeout=selected_endpoint_config.get("timeout")
        )

        if response and not response.get("error"):
            if api_type == "PHONE_VALIDATION":
                return (
                    f"AbstractAPI (Validation Tél): Numéro: {response.get('phone', 'N/A')}, "
                    f"Valide: {response.get('valid', 'N/A')}, "
                    f"Pays: {response.get('country', {}).get('name', 'N/A')}"
                )
            elif api_type == "EMAIL_VALIDATION":
                return (
                    f"AbstractAPI (Validation Email): Email: {response.get('email', 'N/A')}, "
                    f"Valide: {response.get('is_valid_format', 'N/A')}, "
                    f"Deliverable: {response.get('is_deliverable', 'N/A')}"
                )
            elif api_type == "EXCHANGE_RATES":
                return f"AbstractAPI (Taux de change): Base: {response.get('base', 'N/A')}, Taux (USD): {response.get('exchange_rates', {}).get('USD', 'N/A')}"
            elif api_type == "HOLIDAYS":
                holidays = [h.get('name', 'N/A') for h in response if h.get('name')]
                return f"AbstractAPI (Jours fériés {params.get('country', 'US')} {params.get('year')}): {', '.join(holidays[:5])}..." if holidays else "Aucun jour férié trouvé."
            return f"AbstractAPI ({api_type}): Réponse brute: {response}"
        return f"AbstractAPI ({api_type}): Erreur: {response.get('message', 'Inconnu')}" if response else "AbstractAPI: Réponse vide ou erreur interne."

class GoogleCustomSearchClient(APIClient):
    def __init__(self):
        super().__init__("GOOGLE_CUSTOM_SEARCH", endpoint_health_manager)

    async def query(self, query_text: str) -> str:
        """Effectue une recherche personnalisée Google via l'API Custom Search."""
        params = {"q": query_text}
        response = await self._make_request(params=params)
        if response and not response.get("error"):
            items = response.get("items", [])
            if items:
                output = "Google Custom Search:\n"
                for item in items[:3]:
                    output += f"- {item.get('title', 'N/A')}: {item.get('snippet', 'N/A')} {neutralize_urls(item.get('link', ''))}\n"
                return output
            return "Google Custom Search: Aucun résultat trouvé."
        return f"Google Custom Search: Erreur: {response.get('message', 'Inconnu')}" if response else "Google Custom Search: Réponse vide ou erreur interne."

class RandommerClient(APIClient):
    def __init__(self):
        super().__init__("RANDOMMER", endpoint_health_manager)

    async def query(self, country_code: str = "US", quantity: int = 1) -> str:
        """Génère des numéros de téléphone aléatoires via Randommer.io."""
        params = {"CountryCode": country_code, "Quantity": quantity}
        response = await self._make_request(params=params)
        if response and not response.get("error"):
            if isinstance(response, list) and response:
                return f"Randommer (Numéros de téléphone): {', '.join(response)}"
            return f"Randommer: {response}"
        return f"Randommer: Erreur: {response.get('message', 'Inconnu')}" if response else "Randommer: Réponse vide ou erreur interne."

class TomorrowIOClient(APIClient):
    def __init__(self):
        super().__init__("TOMORROW.IO", endpoint_health_manager)

    async def query(self, location: str, fields: Optional[List[str]] = None) -> str:
        """Récupère les prévisions météorologiques via Tomorrow.io."""
        if fields is None:
            fields = ["temperature", "humidity", "windSpeed"]
        payload = {"location": location, "fields": fields, "units": "metric", "timesteps": ["1h"]}
        response = await self._make_request(json_data=payload)
        if response and not response.get("error"):
            data = response.get("data", {}).get("timelines", [{}])[0].get("intervals", [{}])[0].get("values", {})
            if data:
                output = f"Météo (Tomorrow.io) à {location}:\n"
                for field in fields:
                    output += f"- {field.capitalize()}: {data.get(field, 'N/A')}\n"
                return output
            return "Tomorrow.io: Données météo non trouvées."
        return f"Tomorrow.io: Erreur: {response.get('message', 'Inconnu')}" if response else "Tomorrow.io: Réponse vide ou erreur interne."

class OpenWeatherMapClient(APIClient):
    def __init__(self):
        super().__init__("OPENWEATHERMAP", endpoint_health_manager)

    async def query(self, location: str) -> str:
        """Récupère les conditions météorologiques actuelles via OpenWeatherMap."""
        params = {"q": location}
        response = await self._make_request(params=params)
        if response and not response.get("error"):
            main_data = response.get("main", {})
            weather_desc = response.get("weather", [{}])[0].get("description", "N/A")
            if main_data:
                temp_kelvin = main_data.get('temp', 'N/A')
                feels_like_kelvin = main_data.get('feels_like', 'N/A')
                
                temp_celsius = f"{temp_kelvin - 273.15:.2f}" if isinstance(temp_kelvin, (int, float)) else "N/A"
                feels_like_celsius = f"{feels_like_kelvin - 273.15:.2f}" if isinstance(feels_like_kelvin, (int, float)) else "N/A"

                return (
                    f"Météo (OpenWeatherMap) à {location}:\n"
                    f"Température: {temp_celsius}°C, "
                    f"Ressenti: {feels_like_celsius}°C, "
                    f"Humidité: {main_data.get('humidity', 'N/A')}%, "
                    f"Conditions: {weather_desc}"
                )
            return "OpenWeatherMap: Données météo non trouvées."
        return f"OpenWeatherMap: Erreur: {response.get('message', 'Inconnu')}" if response else "OpenWeatherMap: Réponse vide ou erreur interne."

class MockarooClient(APIClient):
    def __init__(self):
        super().__init__("MOCKAROO", endpoint_health_manager)

    async def query(self, count: int = 1, fields_json: Optional[str] = None) -> str:
        """Génère des données de test via Mockaroo."""
        params = {"count": count}
        if fields_json:
            params["fields"] = fields_json
        response = await self._make_request(params=params)
        if response and not response.get("error"):
            return f"Mockaroo (Génération de données):\n{json.dumps(response, indent=2)}"
        return f"Mockaroo: Erreur: {response.get('message', 'Inconnu')}" if response else "Mockaroo: Réponse vide ou erreur interne."

class OpenPageRankClient(APIClient):
    def __init__(self):
        super().__init__("OPENPAGERANK", endpoint_health_manager)

    async def query(self, domains: List[str]) -> str:
        """Récupère le PageRank de domaines via OpenPageRank."""
        params = {"domains[]": domains}
        response = await self._make_request(params=params)
        if response and not response.get("error"):
            results = response.get("response", [])
            if results:
                output = "OpenPageRank (Classement de domaine):\n"
                for res in results:
                    output += f"- Domaine: {res.get('domain', 'N/A')}, PageRank: {res.get('page_rank', 'N/A')}\n"
                return output
            return "OpenPageRank: Aucun résultat trouvé."
        return f"OpenPageRank: Erreur: {response.get('message', 'Inconnu')}" if response else "OpenPageRank: Réponse vide ou erreur interne."

class RapidAPIClient(APIClient):
    def __init__(self):
        super().__init__("RAPIDAPI", endpoint_health_manager)

    async def query(self, api_name: str, **kwargs) -> str:
        """
        Interroge diverses APIs disponibles via RapidAPI (blagues, taux de change, faits aléatoires).
        `api_name` spécifie l'API RapidAPI à utiliser.
        """
        selected_endpoint_config = None
        for config in API_CONFIG.get(self.name, []):
            if api_name.lower() in config["endpoint_name"].lower():
                selected_endpoint_config = config
                break
        
        if not selected_endpoint_config:
            return f"RapidAPI: Endpoint pour '{api_name}' non trouvé ou non configuré."

        url = selected_endpoint_config["url"]
        method = selected_endpoint_config["method"]
        
        request_params = selected_endpoint_config.get("fixed_params", {}).copy()
        request_headers = selected_endpoint_config.get("fixed_headers", {}).copy()
        request_json_data = selected_endpoint_config.get("fixed_json", {}).copy()

        if method == "GET":
            request_params.update(kwargs)
        elif method == "POST":
            request_json_data.update(kwargs)

        headers = {
            selected_endpoint_config["key_field"]: selected_endpoint_config["key"],
            "X-RapidAPI-Host": selected_endpoint_config["fixed_headers"].get("X-RapidAPI-Host")
        }
        
        response = await self._make_request(
            params=request_params,
            headers=headers,
            json_data=request_json_data,
            url=url,
            method=method,
            timeout=selected_endpoint_config.get("timeout")
        )

        if response and not response.get("error"):
            if api_name.lower() == "programming joke":
                return f"RapidAPI (Blague de Programmation): {response.get('setup', '')} - {response.get('punchline', '')}"
            elif api_name.lower() == "currency list quotes":
                return f"RapidAPI (Devises): {json.dumps(response, indent=2)}"
            elif api_name.lower() == "random fact":
                return f"RapidAPI (Fait Aléatoire): {response.get('text', 'N/A')}"
            return f"RapidAPI ({api_name}): {json.dumps(response, indent=2)}"
        return f"RapidAPI ({api_name}): Erreur: {response.get('message', 'Inconnu')}" if response else "RapidAPI: Réponse vide ou erreur interne."

# Liste de tous les clients API instanciables
ALL_API_CLIENTS = [
    GeminiAPIClient(),
    OCRApiClient(),
    DeepSeekClient(),
    SerperClient(),
    WolframAlphaClient(),
    TavilyClient(),
    ApiFlashClient(),
    CrawlbaseClient(),
    DetectLanguageClient(),
    GuardianClient(),
    IP2LocationClient(),
    ShodanClient(),
    WeatherAPIClient(),
    CloudmersiveClient(),
    GreyNoiseClient(),
    PulsediveClient(),
    StormGlassClient(),
    LoginRadiusClient(),
    JsonbinClient(),
    HuggingFaceClient(),
    TwilioClient(),
    AbstractAPIClient(),
    GoogleCustomSearchClient(),
    RandommerClient(),
    TomorrowIOClient(),
    OpenWeatherMapClient(),
    MockarooClient(),
    OpenPageRankClient(),
    RapidAPIClient()
]

import asyncio
import json
import re
import base64
from typing import Dict, Any, List, Optional, Union

# Import des clients API
from api_clients import (
    GeminiAPIClient, OCRApiClient, DeepSeekClient, SerperClient,
    WolframAlphaClient, TavilyClient, ApiFlashClient, CrawlbaseClient,
    DetectLanguageClient, GuardianClient, IP2LocationClient, ShodanClient,
    WeatherAPIClient, CloudmersiveClient, GreyNoiseClient, PulsediveClient,
    StormGlassClient, LoginRadiusClient, JsonbinClient, HuggingFaceClient,
    TwilioClient, AbstractAPIClient, GoogleCustomSearchClient,
    RandommerClient, TomorrowIOClient, OpenWeatherMapClient, MockarooClient,
    OpenPageRankClient, RapidAPIClient
)

# Import des fonctions utilitaires
from utils import log_message, neutralize_urls, find_tool_by_name
from config import TOOL_CONFIG

# Instanciation des clients API
gemini_client = GeminiAPIClient()
ocr_client = OCRApiClient()
deepseek_client = DeepSeekClient()
serper_client = SerperClient()
wolfram_alpha_client = WolframAlphaClient()
tavily_client = TavilyClient()
apiflash_client = ApiFlashClient()
crawlbase_client = CrawlbaseClient()
detect_language_client = DetectLanguageClient()
guardian_client = GuardianClient()
ip2location_client = IP2LocationClient()
shodan_client = ShodanClient()
weather_api_client = WeatherAPIClient()
cloudmersive_client = CloudmersiveClient()
greynoise_client = GreyNoiseClient()
pulsedive_client = PulsediveClient()
stormglass_client = StormGlassClient()
loginradius_client = LoginRadiusClient()
jsonbin_client = JsonbinClient()
huggingface_client = HuggingFaceClient()
twilio_client = TwilioClient()
abstractapi_client = AbstractAPIClient()
google_custom_search_client = GoogleCustomSearchClient()
randommer_client = RandommerClient()
tomorrow_io_client = TomorrowIOClient()
openweathermap_client = OpenWeatherMapClient()
mockaroo_client = MockarooClient()
openpagerank_client = OpenPageRankClient()
rapidapi_client = RapidAPIClient()

async def execute_tool(tool_name: str, **kwargs) -> str:
    """
    Exécute un outil spécifique en fonction de son nom et des arguments fournis.
    C'est le point d'entrée principal pour l'exécution de toutes les fonctions d'outils.
    """
    log_message(f"Exécution de l'outil: {tool_name} avec kwargs: {kwargs}")
    tool_config = find_tool_by_name(tool_name)

    if not tool_config:
        log_message(f"Outil non trouvé: {tool_name}", level="error")
        return f"Erreur: Outil '{tool_name}' non trouvé ou non configuré."

    try:
        if tool_name == "google_search":
            return await google_search_tool(kwargs.get("queries"))
        elif tool_name == "media_control":
            action = kwargs.get("action")
            if action == "like":
                return await media_control_like_tool()
            elif action == "dislike":
                return await media_control_dislike_tool()
            elif action == "next":
                return await media_control_next_tool()
            elif action == "previous":
                return await media_control_previous_tool()
            elif action == "pause":
                return await media_control_pause_tool()
            elif action == "resume":
                return await media_control_resume_tool()
            elif action == "stop":
                return await media_control_stop_tool()
            elif action == "replay":
                return await media_control_replay_tool()
            elif action == "seek_absolute":
                return await media_control_seek_absolute_tool(kwargs.get("position"))
            elif action == "seek_relative":
                return await media_control_seek_relative_tool(kwargs.get("offset"))
            else:
                return f"Action non supportée pour media_control: {action}"
        elif tool_name == "clock":
            action = kwargs.get("action")
            if action == "create_alarm":
                return await clock_create_alarm_tool(
                    duration=kwargs.get("duration"),
                    time=kwargs.get("time"),
                    date=kwargs.get("date"),
                    label=kwargs.get("label"),
                    recurrence=kwargs.get("recurrence")
                )
            elif action == "create_timer":
                return await clock_create_timer_tool(
                    duration=kwargs.get("duration"),
                    time=kwargs.get("time"),
                    label=kwargs.get("label")
                )
            elif action == "show_matching_alarms":
                return await clock_show_matching_alarms_tool(
                    query=kwargs.get("query"),
                    alarm_type=kwargs.get("alarm_type"),
                    alarm_ids=kwargs.get("alarm_ids"),
                    date=kwargs.get("date"),
                    start_date=kwargs.get("start_date"),
                    end_date=kwargs.get("end_date")
                )
            elif action == "show_matching_timers":
                return await clock_show_matching_timers_tool(
                    query=kwargs.get("query"),
                    timer_type=kwargs.get("timer_type"),
                    timer_ids=kwargs.get("timer_ids")
                )
            elif action == "modify_alarm_v2":
                return await clock_modify_alarm_v2_tool(
                    alarm_filters=kwargs.get("alarm_filters"),
                    alarm_modifications=kwargs.get("alarm_modifications")
                )
            elif action == "modify_timer_v2":
                return await clock_modify_timer_v2_tool(
                    timer_filters=kwargs.get("timer_filters"),
                    timer_modifications=kwargs.get("timer_modifications")
                )
            elif action == "snooze":
                return await clock_snooze_tool()
            else:
                return f"Action non supportée pour clock: {action}"
        elif tool_name == "ocr_space":
            return await ocr_space_tool(kwargs.get("image_base64"))
        elif tool_name == "deepseek_chat":
            return await deepseek_chat_tool(kwargs.get("prompt"), kwargs.get("model"))
        elif tool_name == "serper_dev":
            return await serper_dev_tool(kwargs.get("query_text"))
        elif tool_name == "wolfram_alpha":
            return await wolfram_alpha_tool(kwargs.get("input_text"))
        elif tool_name == "tavily_search":
            return await tavily_search_tool(kwargs.get("query_text"), kwargs.get("max_results"))
        elif tool_name == "apiflash_screenshot":
            return await apiflash_screenshot_tool(kwargs.get("url"))
        elif tool_name == "crawlbase_scraper":
            return await crawlbase_scraper_tool(kwargs.get("url"), kwargs.get("use_js"))
        elif tool_name == "detect_language":
            return await detect_language_tool(kwargs.get("text"))
        elif tool_name == "guardian_news":
            return await guardian_news_tool(kwargs.get("query_text"))
        elif tool_name == "ip2location":
            return await ip2location_tool(kwargs.get("ip_address"))
        elif tool_name == "shodan":
            return await shodan_tool(kwargs.get("query_text"))
        elif tool_name == "weather_api":
            return await weather_api_tool(kwargs.get("location"))
        elif tool_name == "cloudmersive_domain":
            return await cloudmersive_domain_tool(kwargs.get("domain"))
        elif tool_name == "greynoise":
            return await greynoise_tool(kwargs.get("ip_address"))
        elif tool_name == "pulsedive":
            return await pulsedive_tool(kwargs.get("indicator"), kwargs.get("type"))
        elif tool_name == "stormglass":
            return await stormglass_tool(kwargs.get("lat"), kwargs.get("lng"), kwargs.get("params"))
        elif tool_name == "loginradius_ping":
            return await loginradius_ping_tool()
        elif tool_name == "jsonbin_io":
            return await jsonbin_io_tool(kwargs.get("data"), kwargs.get("private"), kwargs.get("bin_id"))
        elif tool_name == "huggingface_inference":
            return await huggingface_inference_tool(kwargs.get("model_name"), kwargs.get("input_text"))
        elif tool_name == "twilio_balance":
            return await twilio_balance_tool()
        elif tool_name == "abstractapi":
            return await abstractapi_tool(kwargs.get("input_value"), kwargs.get("api_type"))
        elif tool_name == "google_custom_search":
            return await google_custom_search_tool(kwargs.get("query_text"))
        elif tool_name == "randommer_phone":
            return await randommer_phone_tool(kwargs.get("country_code"), kwargs.get("quantity"))
        elif tool_name == "tomorrow_io_weather":
            return await tomorrow_io_weather_tool(kwargs.get("location"), kwargs.get("fields"))
        elif tool_name == "openweathermap_weather":
            return await openweathermap_weather_tool(kwargs.get("location"))
        elif tool_name == "mockaroo_data":
            return await mockaroo_data_tool(kwargs.get("count"), kwargs.get("fields_json"))
        elif tool_name == "openpagerank":
            return await openpagerank_tool(kwargs.get("domains"))
        elif tool_name == "rapidapi":
            return await rapidapi_tool(kwargs.get("api_name"), **kwargs.get("api_kwargs", {}))
        else:
            log_message(f"Aucun gestionnaire d'outil défini pour: {tool_name}", level="error")
            return f"Erreur: Aucun gestionnaire d'outil défini pour '{tool_name}'."
    except Exception as e:
        log_message(f"Erreur lors de l'exécution de l'outil {tool_name}: {e}", level="error")
        return f"Erreur lors de l'exécution de l'outil {tool_name}: {e}"

# --- Fonctions d'outils spécifiques (wrappers autour des clients API) ---

async def google_search_tool(queries: List[str]) -> str:
    """Effectue une recherche Google."""
    results = []
    for query in queries:
        log_message(f"Recherche Google pour: {query}")
        # Ici, nous utilisons un client générique pour Google Search
        # car il n'y a pas de client spécifique 'google_search' dans api_clients.py
        # Il faudrait soit créer un GoogleSearchClient, soit utiliser un client existant
        # comme SerperClient ou TavilyClient pour simuler la recherche.
        # Pour l'exemple, nous allons simuler une réponse ou utiliser un client de recherche existant.
        # Si 'google_search' est censé utiliser Serper ou Tavily, il faut le mapper ici.
        # Supposons que 'google_search' est un alias pour 'serper_dev' pour cet exemple.
        response = await serper_client.query(query)
        results.append(f"Résultat pour '{query}': {response}")
    return "\n".join(results)

async def media_control_like_tool() -> str:
    """Aime le média en cours de lecture."""
    # Simule l'appel à l'API media_control.like()
    # Dans un vrai scénario, cela appellerait une API de contrôle média sur l'appareil.
    log_message("Action media_control.like() simulée.")
    return "Média actuel aimé."

async def media_control_dislike_tool() -> str:
    """N'aime pas le média en cours de lecture."""
    log_message("Action media_control.dislike() simulée.")
    return "Média actuel non aimé."

async def media_control_next_tool() -> str:
    """Passe à l'élément multimédia suivant."""
    log_message("Action media_control.next() simulée.")
    return "Passage au média suivant."

async def media_control_previous_tool() -> str:
    """Passe à l'élément multimédia précédent."""
    log_message("Action media_control.previous() simulée.")
    return "Passage au média précédent."

async def media_control_pause_tool() -> str:
    """Met en pause le média en cours de lecture."""
    log_message("Action media_control.pause() simulée.")
    return "Média actuel mis en pause."

async def media_control_resume_tool() -> str:
    """Reprend la lecture du média en pause."""
    log_message("Action media_control.resume() simulée.")
    return "Lecture du média reprise."

async def media_control_stop_tool() -> str:
    """Arrête le média en cours de lecture."""
    log_message("Action media_control.stop() simulée.")
    return "Média actuel arrêté."

async def media_control_replay_tool() -> str:
    """Rejoue le média actuel depuis le début."""
    log_message("Action media_control.replay() simulée.")
    return "Média actuel rejoué."

async def media_control_seek_absolute_tool(position: int) -> str:
    """Saute à une position absolue dans le média."""
    log_message(f"Action media_control.seek_absolute({position}) simulée.")
    return f"Média avancé à la position {position} secondes."

async def media_control_seek_relative_tool(offset: int) -> str:
    """Ajuste la lecture du média par une durée relative."""
    log_message(f"Action media_control.seek_relative({offset}) simulée.")
    return f"Média avancé de {offset} secondes."

async def clock_create_alarm_tool(duration: Optional[str] = None, time: Optional[str] = None, date: Optional[str] = None, label: Optional[str] = None, recurrence: Optional[List[str]] = None) -> str:
    """Crée une alarme."""
    # Simule l'appel à l'API clock.create_alarm()
    log_message(f"Action clock.create_alarm() simulée avec durée={duration}, heure={time}, date={date}, label={label}, récurrence={recurrence}.")
    return f"Alarme créée pour {time if time else duration}."

async def clock_create_timer_tool(duration: Optional[str] = None, time: Optional[str] = None, label: Optional[str] = None) -> str:
    """Crée un minuteur."""
    # Simule l'appel à l'API clock.create_timer()
    log_message(f"Action clock.create_timer() simulée avec durée={duration}, heure={time}, label={label}.")
    return f"Minuteur créé pour {time if time else duration}."

async def clock_show_matching_alarms_tool(query: Optional[str] = None, alarm_type: Optional[str] = None, alarm_ids: Optional[List[str]] = None, date: Optional[str] = None, start_date: Optional[str] = None, end_date: Optional[str] = None) -> str:
    """Affiche les alarmes correspondantes."""
    # Simule l'appel à l'API clock.show_matching_alarms()
    log_message(f"Action clock.show_matching_alarms() simulée avec query={query}, type={alarm_type}, ids={alarm_ids}, date={date}, start_date={start_date}, end_date={end_date}.")
    return "Affichage des alarmes correspondantes (simulé)."

async def clock_show_matching_timers_tool(query: Optional[str] = None, timer_type: Optional[str] = None, timer_ids: Optional[List[str]] = None) -> str:
    """Affiche les minuteurs correspondants."""
    # Simule l'appel à l'API clock.show_matching_timers()
    log_message(f"Action clock.show_matching_timers() simulée avec query={query}, type={timer_type}, ids={timer_ids}.")
    return "Affichage des minuteurs correspondants (simulé)."

async def clock_modify_alarm_v2_tool(alarm_filters: Dict[str, Any], alarm_modifications: Dict[str, Any]) -> str:
    """Modifie une alarme."""
    # Simule l'appel à l'API clock.modify_alarm_v2()
    log_message(f"Action clock.modify_alarm_v2() simulée avec filtres={alarm_filters}, modifications={alarm_modifications}.")
    return "Alarme modifiée (simulé)."

async def clock_modify_timer_v2_tool(timer_filters: Dict[str, Any], timer_modifications: Dict[str, Any]) -> str:
    """Modifie un minuteur."""
    # Simule l'appel à l'API clock.modify_timer_v2()
    log_message(f"Action clock.modify_timer_v2() simulée avec filtres={timer_filters}, modifications={timer_modifications}.")
    return "Minuteur modifié (simulé)."

async def clock_snooze_tool() -> str:
    """Met en veille une alarme."""
    # Simule l'appel à l'API clock.snooze()
    log_message("Action clock.snooze() simulée.")
    return "Alarme mise en veille."

async def ocr_space_tool(image_base64: str) -> str:
    """Extrait le texte d'une image via OCR.space."""
    return await ocr_client.query(image_base64)

async def deepseek_chat_tool(prompt: Union[str, List[Dict]], model: str = "deepseek-chat") -> str:
    """Interroge DeepSeek pour des conversations ou complétions."""
    return await deepseek_client.query(prompt, model)

async def serper_dev_tool(query_text: str) -> str:
    """Effectue une recherche web via Serper."""
    return await serper_client.query(query_text)

async def wolfram_alpha_tool(input_text: str) -> str:
    """Interroge WolframAlpha pour des calculs ou des faits."""
    return await wolfram_alpha_client.query(input_text)

async def tavily_search_tool(query_text: str, max_results: int = 3) -> str:
    """Effectue une recherche web avancée via Tavily."""
    return await tavily_client.query(query_text, max_results)

async def apiflash_screenshot_tool(url: str) -> str:
    """Capture une capture d'écran d'une URL via ApiFlash."""
    return await apiflash_client.query(url)

async def crawlbase_scraper_tool(url: str, use_js: bool = False) -> str:
    """Scrape le contenu HTML ou JavaScript d'une URL via Crawlbase."""
    return await crawlbase_client.query(url, use_js)

async def detect_language_tool(text: str) -> str:
    """Détecte la langue d'un texte via DetectLanguage API."""
    return await detect_language_client.query(text)

async def guardian_news_tool(query_text: str) -> str:
    """Recherche des articles de presse via l'API The Guardian."""
    return await guardian_client.query(query_text)

async def ip2location_tool(ip_address: str) -> str:
    """Géolocalise une adresse IP via IP2Location API."""
    return await ip2location_client.query(ip_address)

async def shodan_tool(query_text: str = "") -> str:
    """Interroge Shodan pour des informations sur un hôte IP ou des informations sur la clé API."""
    return await shodan_client.query(query_text)

async def weather_api_tool(location: str) -> str:
    """Récupère les conditions météorologiques actuelles pour une localisation via WeatherAPI."""
    return await weather_api_client.query(location)

async def cloudmersive_domain_tool(domain: str) -> str:
    """Vérifie la validité et le type d'un domaine via Cloudmersive API."""
    return await cloudmersive_client.query(domain)

async def greynoise_tool(ip_address: str) -> str:
    """Analyse une adresse IP pour détecter des activités 'bruit' (malveillantes) via GreyNoise."""
    return await greynoise_client.query(ip_address)

async def pulsedive_tool(indicator: str, type: str = "auto") -> str:
    """Analyse un indicateur de menace (IP, domaine, URL) via Pulsedive."""
    return await pulsedive_client.query(indicator, type)

async def stormglass_tool(lat: float, lng: float, params: str = "airTemperature,waveHeight") -> str:
    """Récupère les données météorologiques maritimes pour une coordonnée via StormGlass."""
    return await stormglass_client.query(lat, lng, params)

async def loginradius_ping_tool() -> str:
    """Effectue un simple ping à l'API LoginRadius pour vérifier sa disponibilité."""
    return await loginradius_client.query()

async def jsonbin_io_tool(data: Optional[Dict[str, Any]] = None, private: bool = True, bin_id: Optional[str] = None) -> str:
    """Crée un nouveau 'bin' JSON ou accède à un bin existant via Jsonbin.io."""
    return await jsonbin_client.query(data, private, bin_id)

async def huggingface_inference_tool(model_name: str = "distilbert-base-uncased-finetuned-sst-2-english", input_text: str = "Hello world") -> str:
    """Effectue une inférence sur un modèle HuggingFace."""
    return await huggingface_client.query(model_name, input_text)

async def twilio_balance_tool() -> str:
    """Récupère le solde du compte Twilio."""
    return await twilio_client.query()

async def abstractapi_tool(input_value: str, api_type: str) -> str:
    """Interroge diverses APIs d'AbstractAPI."""
    return await abstractapi_client.query(input_value, api_type)

async def google_custom_search_tool(query_text: str) -> str:
    """Effectue une recherche personnalisée Google."""
    return await google_custom_search_client.query(query_text)

async def randommer_phone_tool(country_code: str = "US", quantity: int = 1) -> str:
    """Génère des numéros de téléphone aléatoires via Randommer.io."""
    return await randommer_client.query(country_code, quantity)

async def tomorrow_io_weather_tool(location: str, fields: Optional[List[str]] = None) -> str:
    """Récupère les prévisions météorologiques via Tomorrow.io."""
    return await tomorrow_io_client.query(location, fields)

async def openweathermap_weather_tool(location: str) -> str:
    """Récupère les conditions météorologiques actuelles via OpenWeatherMap."""
    return await openweathermap_client.query(location)

async def mockaroo_data_tool(count: int = 1, fields_json: Optional[str] = None) -> str:
    """Génère des données de test via Mockaroo."""
    return await mockaroo_client.query(count, fields_json)

async def openpagerank_tool(domains: List[str]) -> str:
    """Récupère le PageRank de domaines via OpenPageRank."""
    return await openpagerank_client.query(domains)

async def rapidapi_tool(api_name: str, **api_kwargs) -> str:
    """Interroge diverses APIs disponibles via RapidAPI."""
    return await rapidapi_client.query(api_name, **api_kwargs)

import asyncio
import json
import os
import re
import base64
import mimetypes
import datetime
from typing import Dict, Any, List, Optional, Union, Tuple

# Import des modules et fonctions
from config import (
    API_CONFIG, ENDPOINT_HEALTH_FILE, MAX_IMAGE_SIZE,
    GEMINI_TEMPERATURE, GEMINI_TOP_P, GEMINI_TOP_K, GEMINI_MAX_OUTPUT_TOKENS,
    GEMINI_SAFETY_SETTINGS, TOOL_CONFIG
)
from utils import (
    load_json, save_json, get_current_time, format_datetime, log_message,
    neutralize_urls, find_tool_by_name, get_mime_type_from_base64
)
from api_clients import (
    GeminiAPIClient, OCRApiClient, DeepSeekClient, SerperClient,
    WolframAlphaClient, TavilyClient, ApiFlashClient, CrawlbaseClient,
    DetectLanguageClient, GuardianClient, IP2LocationClient, ShodanClient,
    WeatherAPIClient, CloudmersiveClient, GreyNoiseClient, PulsediveClient,
    StormGlassClient, LoginRadiusClient, JsonbinClient, HuggingFaceClient,
    TwilioClient, AbstractAPIClient, GoogleCustomSearchClient,
    RandommerClient, TomorrowIOClient, OpenWeatherMapClient, MockarooClient,
    OpenPageRankClient, RapidAPIClient,
    EndpointHealthManager, set_endpoint_health_manager_global
)
from tools import execute_tool # Import de la fonction execute_tool

# Initialisation du gestionnaire de santé des endpoints
endpoint_health_manager = EndpointHealthManager()
set_endpoint_health_manager_global(endpoint_health_manager)

# Instanciation des clients API
gemini_client = GeminiAPIClient()
ocr_client = OCRApiClient()
deepseek_client = DeepSeekClient()
serper_client = SerperClient()
wolfram_alpha_client = WolframAlphaClient()
tavily_client = TavilyClient()
apiflash_client = ApiFlashClient()
crawlbase_client = CrawlbaseClient()
detect_language_client = DetectLanguageClient()
guardian_client = GuardianClient()
ip2location_client = IP2locationClient()
shodan_client = ShodanClient()
weather_api_client = WeatherAPIClient()
cloudmersive_client = CloudmersiveClient()
greynoise_client = GreyNoiseClient()
pulsedive_client = PulsediveClient()
stormglass_client = StormGlassClient()
loginradius_client = LoginRadiusClient()
jsonbin_client = JsonbinClient()
huggingface_client = HuggingFaceClient()
twilio_client = TwilioClient()
abstractapi_client = AbstractAPIClient()
google_custom_search_client = GoogleCustomSearchClient()
randommer_client = RandommerClient()
tomorrow_io_client = TomorrowIOClient()
openweathermap_client = OpenWeatherMapClient()
mockaroo_client = MockarooClient()
openpagerank_client = OpenPageRankClient()
rapidapi_client = RapidAPIClient()


# Définition des outils disponibles pour Gemini
def get_gemini_tools() -> List[Dict]:
    """
    Construit la liste des outils disponibles pour l'API Gemini
    à partir de la configuration TOOL_CONFIG.
    """
    tools = []
    for tool_name, tool_info in TOOL_CONFIG.items():
        if tool_info.get("enabled", False):
            function_declaration = {
                "name": tool_name,
                "description": tool_info.get("description", ""),
                "parameters": {
                    "type": "OBJECT",
                    "properties": {},
                    "required": []
                }
            }
            for param_name, param_info in tool_info.get("parameters", {}).items():
                function_declaration["parameters"]["properties"][param_name] = {
                    "type": param_info.get("type", "STRING"),
                    "description": param_info.get("description", "")
                }
                if param_info.get("required", False):
                    function_declaration["parameters"]["required"].append(param_name)
            
            # Ajout de la gestion des actions pour les outils "clock" et "media_control"
            if tool_name in ["clock", "media_control"]:
                function_declaration["parameters"]["properties"]["action"] = {
                    "type": "STRING",
                    "description": f"L'action à effectuer pour l'outil {tool_name}."
                }
                function_declaration["parameters"]["required"].append("action")

                # Ajout des sous-paramètres spécifiques à chaque action
                for action_name, action_info in tool_info.get("actions", {}).items():
                    # Crée un objet pour les paramètres spécifiques à cette action
                    action_params_props = {}
                    action_required_params = []
                    for param_name, param_info in action_info.get("parameters", {}).items():
                        action_params_props[param_name] = {
                            "type": param_info.get("type", "STRING"),
                            "description": param_info.get("description", "")
                        }
                        if param_info.get("required", False):
                            action_required_params.append(param_name)
                    
                    # Ajoute ces paramètres comme une propriété conditionnelle ou imbriquée
                    # Gemini ne supporte pas directement les schémas conditionnels pour les outils.
                    # La meilleure approche est de lister tous les paramètres possibles et de laisser le modèle
                    # choisir ceux qui sont pertinents en fonction de l'action.
                    # Ou, pour une meilleure clarté, créer des fonctions distinctes pour chaque action si possible.
                    # Pour l'instant, on va juste ajouter les paramètres à la liste globale.
                    # C'est au modèle de comprendre quels paramètres sont pertinents pour quelle action.
                    function_declaration["parameters"]["properties"].update(action_params_props)
                    function_declaration["parameters"]["required"].extend(action_required_params)
                    
                    # Pour les filtres et modifications complexes (ex: clock.modify_alarm_v2)
                    if action_name in ["modify_alarm_v2", "modify_timer_v2"]:
                        if "alarm_filters" in action_info.get("parameters", {}):
                            function_declaration["parameters"]["properties"]["alarm_filters"] = {
                                "type": "OBJECT",
                                "description": "Filtres pour identifier les alarmes à modifier.",
                                "properties": action_info["parameters"]["alarm_filters"].get("properties", {}),
                                "required": action_info["parameters"]["alarm_filters"].get("required", [])
                            }
                        if "alarm_modifications" in action_info.get("parameters", {}):
                            function_declaration["parameters"]["properties"]["alarm_modifications"] = {
                                "type": "OBJECT",
                                "description": "Modifications à apporter aux alarmes.",
                                "properties": action_info["parameters"]["alarm_modifications"].get("properties", {}),
                                "required": action_info["parameters"]["alarm_modifications"].get("required", [])
                            }
                        if "timer_filters" in action_info.get("parameters", {}):
                            function_declaration["parameters"]["properties"]["timer_filters"] = {
                                "type": "OBJECT",
                                "description": "Filtres pour identifier les minuteurs à modifier.",
                                "properties": action_info["parameters"]["timer_filters"].get("properties", {}),
                                "required": action_info["parameters"]["timer_filters"].get("required", [])
                            }
                        if "timer_modifications" in action_info.get("parameters", {}):
                            function_declaration["parameters"]["properties"]["timer_modifications"] = {
                                "type": "OBJECT",
                                "description": "Modifications à apporter aux minuteurs.",
                                "properties": action_info["parameters"]["timer_modifications"].get("properties", {}),
                                "required": action_info["parameters"]["timer_modifications"].get("required", [])
                            }

            tools.append({"function_declarations": [function_declaration]})
    return tools

async def process_user_query(user_query: str, chat_history: List[Dict], image_data: Optional[str] = None) -> Tuple[str, List[Dict]]:
    """
    Traite la requête de l'utilisateur, interagit avec Gemini et exécute les outils si nécessaire.
    """
    log_message(f"Requête utilisateur: {user_query}")
    log_message(f"Historique du chat (avant): {chat_history}")

    # Initialiser l'historique du chat si vide
    if not chat_history:
        chat_history = []

    # Obtenir les outils disponibles
    gemini_tools = get_gemini_tools()
    log_message(f"Outils disponibles pour Gemini: {json.dumps(gemini_tools, indent=2)}")

    # Appel à Gemini
    gemini_response = await gemini_client.generate_content(
        prompt=user_query,
        chat_history=chat_history,
        image_data=image_data,
        tools=gemini_tools
    )

    if isinstance(gemini_response, str) and gemini_response.startswith("❌"):
        log_message(f"Erreur de Gemini: {gemini_response}", level="error")
        return gemini_response, chat_history

    if not gemini_response:
        log_message("Réponse vide de Gemini.", level="warning")
        return "Désolé, je n'ai pas pu obtenir de réponse de Gemini.", chat_history

    # Traiter la réponse de Gemini
    try:
        if "candidates" in gemini_response and gemini_response["candidates"]:
            candidate = gemini_response["candidates"][0]
            if "content" in candidate and "parts" in candidate["content"]:
                for part in candidate["content"]["parts"]:
                    if "text" in part:
                        # Si Gemini répond avec du texte, l'ajouter à l'historique et le retourner
                        chat_history.append({"role": "model", "parts": [{"text": part["text"]}]})
                        log_message(f"Réponse textuelle de Gemini: {part['text']}")
                        return part["text"], chat_history
                    elif "functionCall" in part:
                        # Si Gemini demande d'appeler une fonction (outil)
                        function_call = part["functionCall"]
                        tool_name = function_call["name"]
                        tool_args = function_call.get("args", {})
                        log_message(f"Gemini a demandé l'outil: {tool_name} avec args: {tool_args}")

                        # Exécuter l'outil
                        tool_output = await execute_tool(tool_name, **tool_args)
                        log_message(f"Sortie de l'outil {tool_name}: {tool_output}")

                        # Ajouter la requête de l'outil et sa sortie à l'historique du chat
                        chat_history.append({"role": "model", "parts": [{"functionCall": function_call}]})
                        chat_history.append({"role": "tool", "parts": [{"functionResponse": {"name": tool_name, "response": {"result": tool_output}}}]})

                        # Rappeler Gemini avec l'historique mis à jour pour obtenir la réponse finale
                        log_message("Rappel de Gemini après exécution de l'outil...")
                        final_gemini_response = await gemini_client.generate_content(
                            prompt=user_query, # On garde le prompt original pour le contexte
                            chat_history=chat_history,
                            image_data=image_data,
                            tools=gemini_tools
                        )

                        if isinstance(final_gemini_response, str) and final_gemini_response.startswith("❌"):
                            log_message(f"Erreur de Gemini après exécution de l'outil: {final_gemini_response}", level="error")
                            return final_gemini_response, chat_history
                        
                        if not final_gemini_response:
                            log_message("Réponse vide de Gemini après exécution de l'outil.", level="warning")
                            return "Désolé, je n'ai pas pu obtenir de réponse de Gemini après l'exécution de l'outil.", chat_history

                        if "candidates" in final_gemini_response and final_gemini_response["candidates"]:
                            final_candidate = final_gemini_response["candidates"][0]
                            if "content" in final_candidate and "parts" in final_candidate["content"]:
                                for final_part in final_candidate["content"]["parts"]:
                                    if "text" in final_part:
                                        chat_history.append({"role": "model", "parts": [{"text": final_part["text"]}]})
                                        log_message(f"Réponse finale de Gemini: {final_part['text']}")
                                        return final_part["text"], chat_history
                                    else:
                                        log_message(f"Partie de réponse finale inattendue de Gemini: {final_part}", level="warning")
                                        return "Désolé, je n'ai pas pu traiter la réponse finale de Gemini.", chat_history
                        log_message("Aucune réponse textuelle finale de Gemini après exécution de l'outil.", level="warning")
                        return "Désolé, je n'ai pas pu obtenir de réponse textuelle finale de Gemini après l'exécution de l'outil.", chat_history
            log_message("Aucune partie de contenu valide trouvée dans la réponse de Gemini.", level="warning")
            return "Désolé, je n'ai pas pu comprendre la réponse de Gemini.", chat_history
        log_message(f"Aucun candidat valide dans la réponse de Gemini: {gemini_response}", level="warning")
        return "Désolé, Gemini n'a pas fourni de réponse valide.", chat_history
    except Exception as e:
        log_message(f"Erreur lors du traitement de la réponse de Gemini: {e}", level="error")
        log_message(f"Traceback: {traceback.format_exc()}", level="error")
        return f"Une erreur interne est survenue lors du traitement de la réponse: {e}", chat_history

async def main():
    """Fonction principale pour exécuter le chatbot."""
    await endpoint_health_manager.init_manager()
    log_message("Démarrage du chatbot. Tapez 'quitter' pour arrêter.")

    # Lancer les checks de santé périodiques en arrière-plan
    async def periodic_health_checks():
        while True:
            for service_name in API_CONFIG.keys():
                await endpoint_health_manager.run_health_check_for_service(service_name)
            await asyncio.sleep(300) # Vérifier toutes les 5 minutes

    asyncio.create_task(periodic_health_checks())

    chat_history = []
    
    # Charger l'historique de chat précédent si disponible
    try:
        if os.path.exists("chat_history.json"):
            with open("chat_history.json", "r", encoding="utf-8") as f:
                loaded_history = json.load(f)
                # S'assurer que les rôles sont corrects pour Gemini
                for entry in loaded_history:
                    if entry.get("role") == "user" or entry.get("role") == "model":
                        chat_history.append(entry)
                    elif entry.get("role") == "tool":
                        # Gemini attend functionResponse dans "parts" pour les outils
                        if "functionCall" in entry.get("parts", [{}])[0]:
                            # C'est une requête d'outil, pas une réponse
                            chat_history.append(entry)
                        elif "functionResponse" in entry.get("parts", [{}])[0]:
                            chat_history.append(entry)
                        else:
                            log_message(f"Entrée d'historique d'outil inattendue: {entry}", level="warning")
                            # Tenter de convertir si c'est un format ancien
                            if "tool_code" in entry.get("parts", [{}])[0]:
                                tool_code_str = entry["parts"][0]["tool_code"]
                                # Extraire le nom de l'outil et la sortie
                                match = re.search(r"print\((\w+)\.([\w_]+)\((.*)\)\)", tool_code_str)
                                if match:
                                    tool_api_name = match.group(1)
                                    tool_method_name = match.group(2)
                                    # Pour l'historique, on a besoin du nom de l'outil tel que défini dans TOOL_CONFIG
                                    # Il faut une meilleure façon de mapper les méthodes API aux noms d'outils.
                                    # Pour l'instant, on va juste utiliser le nom de la méthode comme nom d'outil.
                                    tool_name_for_history = tool_method_name 
                                    
                                    # Simuler la réponse de l'outil
                                    tool_response_content = entry.get("parts", [{}])[1].get("text", "Réponse outil non spécifiée.")
                                    chat_history.append({
                                        "role": "tool",
                                        "parts": [{
                                            "functionResponse": {
                                                "name": tool_name_for_history,
                                                "response": {"result": tool_response_content}
                                            }
                                        }]
                                    })
                                else:
                                    log_message(f"Impossible de parser l'entrée tool_code: {tool_code_str}", level="warning")
                            else:
                                log_message(f"Entrée d'historique d'outil non reconnue: {entry}", level="warning")

                log_message("Historique du chat chargé avec succès.")
    except Exception as e:
        log_message(f"Erreur lors du chargement de l'historique du chat: {e}", level="error")
        chat_history = [] # Réinitialiser en cas d'erreur

    while True:
        user_input = input("Vous: ")
        if user_input.lower() == "quitter":
            break

        image_path = None
        image_data = None
        
        # Vérifier si l'utilisateur a fourni un chemin d'image
        image_match = re.search(r"\[image:(.+)\]", user_input)
        if image_match:
            image_path = image_match.group(1).strip()
            user_input = user_input.replace(image_match.group(0), "").strip() # Supprimer la balise image du prompt

            if os.path.exists(image_path):
                try:
                    with open(image_path, "rb") as image_file:
                        raw_image_data = image_file.read()
                        if len(raw_image_data) > MAX_IMAGE_SIZE:
                            log_message(f"L'image dépasse la taille maximale autorisée ({MAX_IMAGE_SIZE / (1024*1024):.2f} Mo).", level="warning")
                            print(f"⚠️ L'image est trop grande. Taille max: {MAX_IMAGE_SIZE / (1024*1024):.2f} Mo.")
                            image_data = None # Ne pas envoyer l'image si elle est trop grande
                        else:
                            base64_encoded_image = base64.b64encode(raw_image_data).decode('utf-8')
                            mime_type = get_mime_type_from_base64(base64_encoded_image)
                            if mime_type:
                                image_data = f"data:{mime_type};base64,{base64_encoded_image}"
                                log_message(f"Image chargée et encodée en base64: {image_path} (MIME: {mime_type})")
                            else:
                                log_message(f"Impossible de déterminer le type MIME de l'image: {image_path}", level="warning")
                                image_data = base64_encoded_image # Envoyer sans MIME si non détecté
                except Exception as e:
                    log_message(f"Erreur lors du chargement de l'image {image_path}: {e}", level="error")
                    print(f"❌ Erreur lors du chargement de l'image: {e}")
                    image_data = None
            else:
                log_message(f"Fichier image non trouvé: {image_path}", level="warning")
                print(f"❌ Erreur: Fichier image '{image_path}' non trouvé.")
                image_data = None

        # Ajouter la requête utilisateur à l'historique
        user_parts = [{"text": user_input}]
        if image_data:
            # Si l'image est incluse, elle sera ajoutée par generate_content
            pass
        chat_history.append({"role": "user", "parts": user_parts})

        response, chat_history = await process_user_query(user_input, chat_history, image_data)
        print(f"Bot: {response}")

        # Sauvegarder l'historique après chaque tour
        try:
            # Nettoyer l'historique pour la sauvegarde:
            # - Enlever les données d'image base64 (trop volumineux, non nécessaire pour la persistance)
            # - S'assurer que les objets functionCall/functionResponse sont bien formatés
            history_to_save = []
            for entry in chat_history:
                new_entry = entry.copy()
                if "parts" in new_entry:
                    new_parts = []
                    for part in new_entry["parts"]:
                        if "inlineData" in part:
                            # Ne pas sauvegarder les données d'image brutes
                            new_part = part.copy()
                            new_part["inlineData"] = {"mimeType": part["inlineData"]["mimeType"], "data": "[IMAGE_DATA_REMOVED_FOR_SAVE]"}
                            new_parts.append(new_part)
                        else:
                            new_parts.append(part)
                    new_entry["parts"] = new_parts
                history_to_save.append(new_entry)
            
            with open("chat_history.json", "w", encoding="utf-8") as f:
                json.dump(history_to_save, f, indent=2, ensure_ascii=False)
            log_message("Historique du chat sauvegardé.")
        except Exception as e:
            log_message(f"Erreur lors de la sauvegarde de l'historique du chat: {e}", level="error")

if __name__ == "__main__":
    import traceback
    try:
        asyncio.run(main())
    except KeyboardInterrupt:
        log_message("Chatbot arrêté par l'utilisateur.")
    except Exception as e:
        log_message(f"Une erreur inattendue est survenue: {e}", level="critical")
        log_message(f"Traceback: {traceback.format_exc()}", level="critical")


analyse ca en profondeur et tout les aspect possible tu a une autre analyse et des question qui arrive dans la suite oublie rien jai pas besoin de racapitulatif tu en fait un sait quil et pour toi ne fait rien de plus que une analyse complete 

nouveau script 
