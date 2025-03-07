# Patrones
---------------------------------
#singleton
class UserSession:
    _instance = None

    def __new__(cls):
        if cls._instance is None:
            cls._instance = super(UserSession, cls).__new__(cls)
            cls._instance.points = 0  # Inicia con 0 puntos
            cls._instance.unlocked_images = set()  # Imágenes desbloqueadas
        return cls._instance

# Uso del Singleton
session1 = UserSession()
session2 = UserSession()
print(session1 is session2)  # True, ambas son la misma instancia
-----------------------
# Adapter
class APIImage:
    def fetch_image_data(self):
        return {"title": "Jaguar", "url": "https://example.com/jaguar.jpg"}

class ImageAdapter:
    def __init__(self, api_image):
        self.api_image = api_image

    def get_image(self):
        data = self.api_image.fetch_image_data()
        return {"name": data["title"], "image_url": data["url"]}

# Uso
api_image = APIImage()
adapted_image = ImageAdapter(api_image)
print(adapted_image.get_image())  # {"name": "Jaguar", "image_url": "https://example.com/jaguar.jpg"}
-----------------------
#Decorator
class Image:
    def __init__(self, title, url):
        self.title = title
        self.url = url

    def display(self):
        return f"Imagen: {self.title}, URL: {self.url}"

# Decorator para añadir descripción extra

class DescriptionDecorator:
    def __init__(self, image, description):
        self.image = image
        self.description = description

    def display(self):
        return f"{self.image.display()} - Descripción: {self.description}"

# Uso del decorador
img = Image("Jaguar", "https://example.com/jaguar.jpg")
decorated_img = DescriptionDecorator(img, "El jaguar es el felino más grande de América.")

print(decorated_img.display())  
# Imagen: Jaguar, URL: https://example.com/jaguar.jpg - Descripción: El jaguar es el felino más grande de América.

