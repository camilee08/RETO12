# RETO12
## Diccionarios
## Desarrollar un algoritmo que imprima de manera ascendente los valores (todos del mismo tipo) de un diccionario.
````
def valores_ascendentes(diccionario):
    # Obtiniene los valores del diccionario
    valores = list(diccionario.values())
    
    # Ordena de forma ascendente
    n = len(valores)
    for i in range(n):
        for j in range(0, n - i - 1):
            if valores[j] > valores[j + 1]:
                # Intercambiar
                temp = valores[j]
                valores[j] = valores[j + 1]
                valores[j + 1] = temp

    print("📈 Valores ordenados:")
    for v in valores:
        print(v)

    # Imprime los valores
    print("📈 Valores ordenados:")
    for v in valores:
        print(v)

if __name__ == "__main__":
    mi_diccionario = {
        "a": 15,
        "b": 11,
        "c": 18,
        "d": 33}

    valores_ascendentes(mi_diccionario)
````
## 2. Desarrollar una función que reciba dos diccionarios como parámetros y los mezcle, es decir, que se construya un nuevo diccionario con las llaves de los dos diccionarios; si hay una clave repetida en ambos diccionarios, se debe asignar el valor que tenga la clave en el primer diccionario.
````
def mezclar_diccionarios(diccionario1, diccionario2):
    nuevo_diccionario = {}  

   #Agrega todos los ítems de dicccionario 2
    for key in diccionario2:
        nuevo_diccionario[key] = diccionario2[key]

    #Agrega los de dicccionario1, se asigna el valor que tenga la clave en el primer diccionario.
    for key in diccionario1:
        nuevo_diccionario[key] = diccionario1[key]

    return nuevo_diccionario
````
## 3. Dado el JSON:
````
{
	"jadiazcoronado":{
		"nombres": "Juan Antonio",
		"apellidos": "Diaz Coronado",
		"edad":19,
		"colombiano":true,
		"deportes":["Futbol","Ajedrez","Gimnasia"]
	},
	"dmlunasol":{
		"nombres": "Dorotea Maritza",
		"apellidos": "Luna Sol",
		"edad":25,
		"colombiano":false,
		"deportes":["Baloncesto","Ajedrez","Gimnasia"]
	}
}
````
Cree un programa que lea de un archivo con dicho JSON y:  

- Imprima los nombres completos (nombre y apellidos) de las personas que practican el deporte ingresado por el usuario.  
- Imprima los nombres completos (nombre y apellidos) de las personas que estén en un rango de edades dado por el usuario.  
Primero guardo el json en un archivo llamado personas.json  
Luego, el código queda de la siguiente manera
````
import json

with open("personas.json", "r") as archivo:
    personas = json.load(archivo)

# consulta por deporte
deporte = input("Ingrese un deporte: ")
print("Personas que practican", deporte, ":")
for key in personas:
    if deporte in personas[key]["deportes"]:
        nombre = personas[key]["nombres"]
        apellido = personas[key]["apellidos"]
        print(nombre, apellido)

# Consulta por rango de edad
edad_min = int(input("Ingrese la edad mínima: "))
edad_max = int(input("Ingrese la edad máxima: "))
print("Personas entre", edad_min, "y", edad_max, ":")
for key in personas:
    edad = personas[key]["edad"]
    if edad_min <= edad <= edad_max:
        nombre = personas[key]["nombres"]
        apellido = personas[key]["apellidos"]
        print(nombre, apellido)
````
## 4. A través de un programa conectese a al menos 3 API's , obtenga el JSON, imprimalo y extraiga los pares de llave : valor.
Utilicé los siguientes  API's (agify, genderize y nationalize)   
https://api.agify.io?name=meelad  
https://api.genderize.io?name=luc  
https://api.nationalize.io?name=nathaniel
Luego utilizo json.loads() para deserializar
````
import requests
import json

# Agify (predice edad)
url1 = 'https://api.agify.io?name=meelad'
respuesta1 = requests.get(url1)
datos1 = json.loads(respuesta1.content)
print("Agify:")
for key in datos1:
    print(key, ":", datos1[key])
    print()

# Genderize (predice género)
url2 = 'https://api.genderize.io?name=luc'
respuesta2 = requests.get(url2)
datos2 = json.loads(respuesta2.content)
print("Genderize:")
for key in datos2:
    print(key, ":", datos2[key])
    print()

# Nationalize (predice nacionalidad)
url3 = 'https://api.nationalize.io?name=nathaniel'
respuesta3 = requests.get(url3)
datos3 = json.loads(respuesta3.content)
print("Nationalize:")
for key in datos3:
    print(key, ":", datos3[key])
````
## 5.Opcional
````
import json
from datetime import datetime

jsonString = '''
{"alertPrecip": {"0": "X", "1": "-", "2": "-", "3": "-", "4": "-", "5": "-", "6": "-", "7": "-"},
 "alertAlertas": {"0": "-", "1": "-", "2": "-", "3": "-", "4": "-", "5": "-", "6": "-", "7": "-"},
 "alertVelViento": {"0": "-", "1": "-", "2": "X", "3": "-", "4": "-", "5": "-", "6": "-", "7": "-"},
 "alertTmpMax": {"0": "-", "1": "-", "2": "-", "3": "-", "4": "-", "5": "X", "6": "-", "7": "-"},
 "alertTmpMin": {"0": "-", "1": "X", "2": "-", "3": "-", "4": "-", "5": "-", "6": "-", "7": "-"},
 "dt": {"0": 1685116800, "1": 1685203200, "2": 1685289600, "3": 1685376000, "4": 1685462400, "5": 1685548800, "6": 1685635200, "7": 1685721600},
 "prcp": {"0": 40.0, "1": 1.65, "2": 14.01, "3": 5.07, "4": 16.55, "5": 2.17, "6": 2.77, "7": 1.73},
 "velViento": {"0": 3.56, "1": 5.07, "2": 5.38, "3": 3.95, "4": 4.74, "5": 3.75, "6": 4.08, "7": 5.94},
 "tmpMax": {"0": 27.16, "1": 31.1, "2": 30.2, "3": 29.5, "4": 28.87, "5": 29.78, "6": 28.96, "7": 28.25},
 "tmpMin": {"0": 25.64, "1": 24.64, "2": 25.84, "3": 25.56, "4": 25.72, "5": 24.86, "6": 25.96, "7": 25.47}
}
'''

data = json.loads(jsonString)


def convertir_fecha(fecha):  
    return datetime.utcfromtimestamp(fecha).strftime("%Y-%m-%d")

for i in range(8):
    fecha = convertir_fecha(data["dt"][str(i)])  
    if data["alertPrecip"][str(i)] == "X":
        print("Alerta de lluvia el día", fecha, "con nivel de", data["prcp"][i]) 
    if data["alertVelViento"][str(i)] == "X":
        print("Alerta de viento el día", fecha, "con velocidad de", data["velViento"][str(i)])  
    if data["alertTmpMax"][str(i)] == "X":
        print("Alerta de temperatura máxima el día", fecha, ":", data["tmpMax"][str(i)])  
    if data["alertTmpMin"][str(i)] == "X":
        print("Alerta de temperatura mínima el día", fecha, ":", data["tmpMin"][str(i)])  
````
Gracias!!
