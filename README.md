# Proyecto final análisis de datos

### Autores ✒️

_Todos los colaboradores del proyecto desde sus inicios son:_

- [Dustin Chávez](https://github.com/Dustinouwu)
- [Steven Guañuna](https://github.com/Seknys)
- [Miguel Muzo](https://github.com/Miguel-EMC)
- [Kevin Pinanjota](https://github.com/Dustinouwu)

--- 

### Descripción 📄

El equipo de trabajo para el proyecto denominado data lake el cual tiene como objetivo la recolección de datos y evaluación para poder determinar varias conclusiones.

![image](https://user-images.githubusercontent.com/74844624/155891550-57279e29-faa4-44f5-97f7-dff2f2e23824.png)

---
## Content 🚀
- [Pre-requisitos](#Pre-requisitos)
	- [Bases SQL](#bases-sql)
	- [Bases NO SQL](#Bases-NO-SQL)
	- [Fuentes de internet](#Fuentes-de-internet)
	- [Otras](#Otras)
- [Twitter to CouchDB](#Twitter-to-CouchDB)
- [Webscraping to Neo4j](#Webscraping-to-Neo4j)
- [Facebook to CouchDB](#cFacebook-to-CouchDB)
- [Twitter to MongoDB](#Twitter-to-MongoDB)
- [Kaggle to MySQL](#Kaggle-to-MySQL)
- [INEC to SQL Server](#INEC-to-SQL-Server)
- [WebScraping to PostgreSQL](#WebScraping-to-PostgreSQL)
- [Datos abiertos to MySQL](#Datos-abiertos-to-MySQL)
- [Video de Youtube](#Video-de-Youtube)

## Pre-requisitos 📋

_Para poder desarrollar el proyecto es necesario instalar las bases de datos y un ID en donde se vaya a ejecutar el script realizado en python_

### Bases SQL 

- Mysql: Una de las bases de datos más utilizadas de código abierto, para entornos de desarrollo web.  

- Sql lite: Sistema gestor de base de datos relacional, relativamente pequeña y además de código abierto. 

- Sql server: El lenguaje de desarrollo utilizado es Transact-SQL, una implementación del estándar ANSI del lenguaje SQL, utilizado para manipular y recuperar datos, tablas y definir relaciones entre ellas. 


 ### Bases NO SQL 

- CouchDB: Gestor de base de datos cuyo foco está puesto en la facilidad de su uso y en ser “una base de datos que asume la web de manera completa”. 

- Neon4J: Base de datos orientada a grafos, se describe como un motor de persistencia embebido, que almacena datos estructurados en lugar de tablas.  

- MongoDB: Es un sistema de base de datos orientado a documentos y a la vez de código abierto, también tiene distinta forma de guardar datos, especialmente guarda estructuras de datos BSON con un esquema dinámico. 

- MongoDB – Atlas: Trata del mismo concepto que la base de datos MongoDB, pero con la gran diferencia que esta se encuentra en la nube, haciéndola más efectiva al momento de hacer trabajos con muchas personas. 
 ### Fuentes de internet:  
- Facebook: Red social creada con el propósito a mantener contacto con personas a largas o cortas distancias, compartiendo diferente contenido, ya sea audiovisual, información, etc. 
- Twitter: Red social de microblogging, con un servicio de comunicación bidireccional con el que se puede llegar a compartir información de diverso tipo de forma rápida. 
### Otras:  
- Pycharm: Es un entorno de desarrollo integrado utilizado en la programación de computadoras, específicamente para el lenguaje Python. Está desarrollado por la empresa checa JetBrains. 
- PowerBI: Servicio de análisis de datos desarrollada por Microsoft, creado con la intención de proporcionar visualizaciones que logren ser interactivas y con capacidades de inteligencia empresarial. 


## Twitter To CouchDB

* [Importar un archivo CSV a CocuhDB]()
* [Migrar un database en CouchDB a MongoDB Atlas]()
* [Analisis PowerBI]()

_Una serie de ejemplos paso a paso que te dice lo que debes ejecutar para tener un entorno de desarrollo ejecutandose_

_Dí cómo será ese paso_

```
Da un ejemplo
```

_Y repite_

```
hasta finalizar
```

_Finaliza con un ejemplo de cómo obtener datos del sistema o como usarlos para una pequeña demo_

## Webscraping to Neo4j

* [Importar un archivo CSV a Neo4j]()
* [Envio de datos hacia MongoDB]()
* [Analisis PowerBI]()

Importar las librerías (neo4j) necesarias para establecer la conexión con la base de datos y tambien las librerías de BeautifulSoup para realizar la extracción de datos mediante Web Scraping

```py
from neo4j import GraphDatabase
import logging
from neo4j.exceptions import ServiceUnavailable
from bs4 import BeautifulSoup
import requests
```
-	Crear una clase y establecer funciones que permiten habilitar la conexión y cerrar esta
```py
class App:

    def __init__(self, uri, user, password):
        self.driver = GraphDatabase.driver(uri, auth=(user, password))

    def close(self):
        # Don't forget to close the driver connection when you are finished with it
        self.driver.close()
```

-	Se crea una función que permite establecer la relación entre los datos que ya deben existir en la base de datos 
```py
def create_friendship(self, person1_name, person2_name,total,Salud,Ataque,Defensa,
                          Velocidad_atck,Velocidad_defen,Velocidad):
        with self.driver.session() as session:
            result = session.write_transaction(
                self._create_and_return_friendship, person1_name, person2_name,total,Salud,
                Ataque,Defensa,Velocidad_atck,Velocidad_defen,Velocidad)
            for row in result:
                print("El pokemon {p1} es tipo {p2}".format(p1=row['p1'], p2=row['p2']))
```

-	Establecer la función principal, que permite recopilar la información en la base de datos, definiendo sus relaciones. Para esto la función tiene que recibir parámetros para que estos puedan ser enviados. (Estos parámetros son los extraídos mediante web scraping y cada uno es almacenado en una variable)
```py
@staticmethod #Importacion de los datos
    def _create_and_return_friendship(tx, person1_name, person2_name, person3_name, person4_name, 
                                      person5_name, person6_name, person7_name, person8_name, 
                                      person9_name):
```

-	Query que crea los datos con los parámetros enviados anteriormente, ademas de establecer una relación entre todos estos. Debido a que la base de datos es una NoSQL de nodos ( estas relaciones son las uniones de nodos)
```py
        query = ( 
            "CREATE (p1:Pokemon { name: $person1_name }) "
            "CREATE (p2:Pokemon { name: $person2_name }) "
            "CREATE (p3:Pokemon { name: $person3_name }) "
            "CREATE (p4:Pokemon { name: $person4_name }) "
            "CREATE (p5:Pokemon { name: $person5_name }) "
            "CREATE (p6:Pokemon { name: $person6_name }) "
            "CREATE (p7:Pokemon { name: $person7_name }) "
            "CREATE (p8:Pokemon { name: $person8_name }) "
            "CREATE (p9:Pokemon { name: $person9_name }) "
            "CREATE (p1)-[:TIPO]->(p2) "
            "CREATE (p1)-[:SALUD]->(p4) "
            "CREATE (p1)-[:ATAQUE]->(p5) "
            "CREATE (p1)-[:DEFENSA]->(p6) "
            "CREATE (p1)-[:VELOCIDAD_ATAQUE]->(p7) "
            "CREATE (p1)-[:VELOCIDAD_DEFENSA]->(p8) "
            "CREATE (p1)-[:VELOCIDAD]->(p9) "
            "CREATE (p1)-[:TOTAL]->(p3) "

            "RETURN p1, p2,p3,p4,p5,p6,p7,p8,p9"
        )
        result = tx.run(query, person1_name=person1_name, person2_name=person2_name, person3_name=person3_name, 
                        person4_name=person4_name, person5_name=person5_name, person6_name=person6_name, 
                        person7_name=person7_name, person8_name=person8_name, person9_name=person9_name)
```

-	Se crea un try and catch para capturer cualquier error que se pueda generar con el query enviado 
```py
  try:
            return [{"p1": row["p1"]["name"], "p2": row["p2"]["name"],"p3": row["p3"]["name"], 
                     "p4": row["p4"]["name"],"p5": row["p5"]["name"], "p6": row["p6"]["name"],
                     "p7": row["p7"]["name"], "p8": row["p8"]["name"], "p9": row["p9"]["name"]}
                    for row in result]
        # Capture any errors along with the query and data for traceability
        except ServiceUnavailable as exception:
            logging.error("{query} raised an error: \n {exception}".format(
                query=query, exception=exception))
            raise
```


-	Credenciales que la proia base de datos nos genera, cuando la creamos por primera vez 
![image](https://user-images.githubusercontent.com/74793607/155898225-9b996462-3e81-4406-8973-e2ba461e2d53.png)

- Para extraer los datos de la página web debemos usar las librerías BeautifulSoup, se debe buscar los nombres de las clases de los datos que querremos recopilar ( En este ejemplo es una tabla )
```py
            #Web Scraping#
tablelist=[]
url='https://pokemondb.net/pokedex/all'
req = requests.get(url)
soup = BeautifulSoup(req.text, 'html.parser')
league = soup.find('table',class_ = 'data-table block-wide')
for team in league.find_all('tbody'):
    rows = team.find_all('tr')
```

- Dentro de la tabla html  se crea un for que recorre todos los datos de la tabla, se crean variables para almacenar cada dato recopilado. Cuando existe algún mismo atributo con la misma clase para que las  funciones reconozcan los datos específicos que deseamos al final de los atributos y nombre de la clase se añade un corchete con el numero que el usuario desee
```py
    for row in rows: 
        nombre = row.find('td', class_ = 'cell-name').text.strip()
        clase = row.find('td', class_ = 'cell-icon').text.strip()
        total = row.find('td', class_ = 'cell-total').text.strip()
        Salud = row.find_all('td',class_='cell-num')[1].text
        Ataque = row.find_all('td',class_='cell-num')[2].text
        Defensa = row.find_all('td',class_='cell-num')[3].text
        Velocidad_atck = row.find_all('td',class_='cell-num')[4].text
        Velocidad_defen = row.find_all('td',class_='cell-num')[5].text
        Velocidad = row.find_all('td',class_='cell-num')[6].text
```

- Dentro del mismo for se crea una variable con formato tipo json para almacenar los datos y depues estos mismos añadirlos a una lista
```py
 teaminLeague = {
            'Nombre': nombre,
            'Tipo': clase,
            'Total': total,
            'Salud ': Salud,
            'Ataque':Ataque,
            'Defensa':Defensa,
            'Velocidad de Ataque': Velocidad_atck,
            'Velocidad de defensa': Velocidad_defen,
            'Velocidad': Velocidad
         }
```

- Dentro del mismo for llamamos a la función principal y le enviamos todas las variables requeridas y que fueron creadas y almacenadas con información anteriormente. Ademas cerramos la conexión una vez finalizada todo este proceso
```py
        if __name__ == "__main__": ###########Enviar los datos 
            # Aura queries use an encrypted connection using the "neo4j+s" URI scheme
            app.create_friendship(nombre, clase,total,Salud,Ataque,Defensa,Velocidad_atck,Velocidad_defen,Velocidad)
            app.close()
```

- Se crea un archivo csv para el análisis de los datos en Power bi, para esto se importa la librería pandas y se crea un data frame y se lo transforma a csv
```py
import pandas as pd
#################Creacion de un CSV
df= pd.DataFrame(tablelist)
df.to_csv('Tema Libre.csv')
```
- Se comprueba todos los datos subidos a neo4j mediante la propia herramienta que proporciona neo4j.
![image](https://user-images.githubusercontent.com/74793607/155897825-7aa603e3-77fa-41be-b5fd-e2c8a71beb65.png)

Puedes encontrar mucho más de cómo utilizar este script en [Importar un archivo CSV a Neo4j]()

### Envio de datos hacia MongoDB

- Importar las librerías necesarias para establecer la conexión con Mongo DB y otras para enviar los datos 
```py
from bs4 import BeautifulSoup
import requests
import pandas as pd
import pymongo
from pymongo import MongoClient
from pymongo.errors import ConnectionFailure
```

- Establecer la conexion con mongo db mediante las debidas credenciales
```py
cliente = MongoClient('localhost',27017)
```

- Crear una nueva base de datos llamada Scraping y una colección llamada listas
```py
db = cliente["Scraping"]
listas = db.listas
```

- Extraemos los datos mediante web Scraping
```py
url='https://pokemondb.net/pokedex/all'
req = requests.get(url)
soup = BeautifulSoup(req.text, 'html.parser')
league = soup.find('table',class_ = 'data-table block-wide')
for team in league.find_all('tbody'):
    rows = team.find_all('tr')
    for row in rows: 
        num = row.find('td', class_ = 'cell-num cell-fixed').text.strip()
        nombre = row.find('td', class_ = 'cell-name').text.strip()
        clase = row.find('td', class_ = 'cell-icon').text.strip()
        total = row.find('td', class_ = 'cell-total').text.strip()
        Salud = row.find_all('td',class_='cell-num')[1].text
        Ataque = row.find_all('td',class_='cell-num')[2].text
        Defensa = row.find_all('td',class_='cell-num')[3].text
        Velocidad_atck = row.find_all('td',class_='cell-num')[4].text
        Velocidad_defen = row.find_all('td',class_='cell-num')[5].text
        Velocidad = row.find_all('td',class_='cell-num')[6].text
```

- Dentro del for se crea una variable para poder enviar todos los datos ala base de datos Mongo Db

```py
        teaminLeague = [{
            '#': num,
            'Nombre': nombre,
            'Tipo': clase,
            'Total': total,
            'Salud ': Salud,
            'Ataque':Ataque,
            'Defensa':Defensa,
            'Velocidad de Ataque': Velocidad_atck,
            'Velocidad de defensa': Velocidad_defen,
            'Velocidad': Velocidad
         }]
```

-	Enviar los datos a la base de datos (Dentro del for)
```py
        listas.insert_many(teaminLeague)
```

- Se comprueba que los datos fueron recopilados exitosamente en la base de datos MongoDB.
- ![image](https://user-images.githubusercontent.com/74793607/155898531-9889e6a7-32a4-44d3-af6d-155e3d8c4c22.png)
Puedes encontrar mucho más de cómo utilizar este script en [Envio de datos hacia MongoDB]()

### Analisis
-	Para el analisis se utiliza la herrmienta Power  Bi que nos permite realizar graficos dependiendo del tipo de datos que deseemos analizar. Para este ejemplo vamos a analizar las estadisticas de cada pokemon, realizando graficos que relacionen el nombre, tipo y todas las estadisticas. Utilizando diferentes filtros como por categoria, por rango o por tipo se puede obtener muchas conclusiones, desde cual es el atributo mas fuerte de una clase en especifico, hasta una comparacion entre todos los atributos mediante un grafico de barras entre los pokemons escogidos.
![image](https://user-images.githubusercontent.com/74793607/155897802-2d9c6a10-128a-4bea-9938-ea98c202b9e8.png)


- En la siguiente imagen se puede observar como mendiante filtros somos capaces de recolectar informacion como :
El atributo mas alto de los pokemons que tienen un total (sumatoria de todas las estadisticas) entre 200 y 275. 
**Velocidad**
![image](https://user-images.githubusercontent.com/74793607/155898732-29bc0c38-b2cd-4e14-abb3-2bf837dbbaf0.png)
![image](https://user-images.githubusercontent.com/74793607/155898738-273485b8-6b4c-4a65-bd93-2ae7956dbdab.png)
- Otro tipo de analisis que se puede realizar, es cuando deseamos averiguar que pokemon tiene la salud mas alta en comparacion con los de su tipo de una clase especifica. 
**Emboar, Salud = 110**
![image](https://user-images.githubusercontent.com/74793607/155898890-c357ab99-7ae0-44f6-91b0-4be66dafde02.png)


## Facebook to CouchDB

* [Importar un archivo CSV a CouchDB]()
* [Migrar un database en CouchDB a MongoDB Atlas]()
* [Analisis PowerBI]()

_Explica que verifican estas pruebas y por qué_

```
Da un ejemplo
```

## Twitter to MongoDB

* [Importar un archivo CSV a MongoDB]()
* [Analisis PowerBI]()

_Explica que verifican estas pruebas y por qué_

```
Da un ejemplo
```

## Kaggle to MySQL

* [Importar un archivo CSV a MySQL]()
* [Migrar un database en MySQL a MongoDB Atlas]()
* [Analisis PowerBI]()

Lo primero es descargar un documento csv o json de la pagina de [kaggle](https://www.kaggle.com/)

![image](https://user-images.githubusercontent.com/74844624/155894152-63cbab26-e378-4a5d-9d99-6c175e5c639f.png)

- Procedimiento

Para poder cargar un archivo a MySQL se debe importar las librería de mysql.connnecto ya que esto nos va a permitir conectarnos con el servidor, además se deberá importar panadas para poder realizar la lectura al archivo csv.

```py
import mysql.connector as msql
import pandas as pd
from sqlalchemy import create_engine
```

Para realizar la conecxion se debe crear una variable con el nombre de ‘conections’ el cual debe conetener los datos de nuestro servidor y comprobamos si se realiza una conexión exitosa ya sea con if- else o con try – except.


```py
connections = msql.connect(
    host = 'localhost',
    user = 'miguel',
    password = 'miguel'
)
if connections.is_connected():
    cursor = connections.cursor()
    print("Conexion con exito")
else:
    print("Error")
```

Con la variable cursor.execute se podrá crear una base de datos con los comandos que se utiliza en MySQL, después se crea un engine para realizar una conexión directa a al base de datos y finalmente se deberá leer el archivo de formato csv.

```py
cursor.execute("CREATE DATABASE articles")
```

```py
engine = create_engine("mysql+mysqldb://miguel:miguel@localhost:3306/articles")
```

```py
dftosql = pd.read_csv("articles_data.csv", sep=',', encoding='UTF-8')
```

Para enviar el documento se debe crear una colección de con cualquier nombre y eso debe estar en un try para poder comprobar si la conexión se realiza con éxito o no.

```py
try:
    dftosql.to_sql('scraping',con=engine, if_exists='replace', index=False)
    print("Alamacenado con exito")
except Exception as ex:
    print(ex)
```

Puedes encontrar mucho más de cómo utilizar este script en [Arhivo csv to MYSQL](https://github.com/Miguel-EMC/Proyecto-Final-Analisis-de-datos/blob/main/05_Kaggle%20to%20MySQL/MYSQL.ipynb)

---
### Migración de MySQL To MongoDB

En la migración de MySQL a mongo lo primero es importar varias librear para poder ayudar a realizar la conexión, lo primero es importar pymongo y sqlite3 , después se importara pandas para que pueda ayudar a visualizar los datos que se quieren enviar.

```py
import sqlite3 as sq
import pandas as pd
import json
from pymongo import MongoClient
import mysql.connector
```

Lo primero es conectar con el servidor de MySQL, para eso se creará una variable en el cual debe encontrarse todos los datos del servidor, y también se debe incluir la base de datos a la cual queremos migrar. 

```py
mydb = mysql.connector.connect(
    host = "localhost",
    user = "miguel",
    password = "miguel",
    database = "articles"
)
```

Es importante crear un cursor para conectar directamente con la colección de la base de datos, para esto se debe utilizar el lenguaje de MySQL.

```py
mycursor = mydb.cursor()
mysql = "SELECT * FROM scraping"
mycursor.execute(mysql)
myresult = mycursor.fetchall()
)
```

También se debe conectar con el servidor de MongoDB, ya puede ser directamente con el url de mongo ATLAS o con los datos de mongoCompass y después se debe crear una variable en el cual se debe incluir el nombre de la base de datos que se va a crear en MongoDB y con un db vamos a conectar las dos bases de datos.

```py
client = MongoClient("mongodb+srv://miguel:miguel@cluster0.ed8kj.mongodb.net/test")

DBS = client.get_database('articles')
db = DBS.MySql
```

Mediante un for se va ir creando el nombre de las tablas que tiene nuestra base de datos en MySQL y mediante un try – except se comprueba si la migración fue realizada con éxito o si existió fallos.

```py
for row in myresult:
    doc={} 
    doc['id']=row[0]
    doc['source_id'] =row[1]
    doc['source_name'] = row[2]
    doc['author']=row[3]
    doc['title'] = row[4]
    doc['description'] =  row[5]
    doc['url'] = row[6]
    doc['url_to_image'] = row[7]
    doc['published_at'] = row[8]
    doc['content'] = row[9]
    doc['top_article'] = row[10]
    doc['engagement_reaction_count'] = row[11]
    doc['engagement_comment_count'] = row[12]
    doc['engagement_share_count'] = row[13]
    doc['engagement_comment_plugin_count'] = row[14]

    try:
       print(doc)
       db.insert_one(doc)
       print("Migracion exitosa")
    except Exception as ex:
        print(ex)
```

Puedes encontrar mucho más de cómo utilizar este script en [MYSQL to MongoDB Atlas](https://github.com/Miguel-EMC/Proyecto-Final-Analisis-de-datos/blob/main/05_Kaggle%20to%20MySQL/MYSQL_TO_MONGODB.ipynb)

---

### Analisis 

En un análisis de las publicaciones que se realizaron durante un año en EEUU las realizo abc-news la cual tiene una cantidad sumamente grande, de igual manera es la que tiene una mayoría de aceptación por las personas, la segunda es al-jazeera-english la que es una segunda publicación, son las dos que tienen publicaciones las que tienen publicaciones que se han encontrado en un top durante todo el año.
 

![image](https://user-images.githubusercontent.com/74844624/155894474-9317c31d-d027-46ed-a770-9de9898c3304.png)


## INEC to SQL Server

* [Importar un archivo CSV a SQL server](CSV-a-SQL-server)
* [Migrar un database en SQL server a MongoDB Atlas](SQL-server-a-MongoDB-Atlas)
* [Analisis PowerBI](Analisis-PowerBI)

Se debe descargar una base de datos sobre un tema libre en [INEC](https://www.ecuadorencifras.gob.ec/institucional/), ya sea en formato csv o json, para luego alamacenarlo en una base de datos

![image](https://user-images.githubusercontent.com/74844624/155895432-10fed1da-d4f3-4801-b677-29af0ae3ccc3.png)

---

### CSV-a-SQL-server

- Procedimiento 

Para crear un script el cual va a cargar un archivo csv a una base de datos en SQL server se debe instalar pip install pypyodbc el cual es una libreria para poder realizar una conexion con el servidor.

```py
pip install pypyodbc
```

Luego se debe importar las librerías de csv, psycopg2, pandas y las extensiones de la librería de psycopg2, estas librerías nos ayudaran a visualizar los datos que vamos a enviar a la base de datos.

```py
import pypyodbc as odbc
import pandas as pd
import pyodbc
```

Luego de se debera leer el archivo que se quiere importar a la base de datos, por lo cual se crea una varible y con ayuda de la libreria pandas de lee el documento convirtiendolo en una dataframe.

```py
datos = pd.read_csv('D:\Miguel\Documents\Analisis\Bases de datos_Proyecto\INEC\estudiantes.csv', encoding='latin1', sep=',')
df = pd.DataFrame(datos)
```

Para realizar una conexion con el servidor se debe crear una variable en el cual se debe colocar el Drive, server en el cual se debe colocar segun los datos de nuestro servidor, luego se debe colocar a la base de datos creada posteriormente, y finalmente truted_connection, luego para tener una conexion directa con la tabla se crea una variable denominada cursor.

```py
#Conectar con el servidor SQL SERVER
conn = pyodbc.connect('Driver={SQL Server};'
                      'Server=DESKTOP-QTJIJML;'
                      'Database=ESTUDIANTE;'
                      'Trusted_Connection=yes;')

cursor = conn.cursor()
```

Gracias al cursor, esto nos permitira tener una relacion directa con el servidor por lo cual nos va a permitir crear tablas e ingresar datos, ademas es importe conocer todas las columnas que tiene el documento csv y colocar la llave primaria.

```py
cursor.execute('''
	   CREATE TABLE estudiantes (
	    Provincia varchar(50),
            Canton varchar(50),
            Parroquia varchar(50),
            Femenino varchar(50),
            Masculino varchar(50),
            Textbox17 varchar(50),
            Textbox6 varchar(50),
            Textbox7 varchar(50),
            Textbox18 varchar(50),
	    id int primary key
			)
               ''')
```

Mediante un for con un contador row se podra ir ingresando cada dato a las columnas que se creo posteriormente y con el conn.commit() se enviara todos los datos ingresados.
```py
for row in df.itertuples():
   
                 doc={}
                 doc['Provincia']=row[0],
                 doc['Canton']=row[1],
                 doc['Parroquia']=row[2],
                 doc['Femenino']=row[3],
                 doc['Masculino']=row[4],
                 doc['Textbox17']=row[5],
                 doc['Textbox6']=row[6],
                 doc['Textbox7']=row[7],
                 doc['Textbox18']=row[8],
		 doc['id']=row[9]
		 conn.commit()
```

Puedes encontrar mucho más de cómo utilizar este script en [CSV-a-SQL-server](https://github.com/Miguel-EMC/Proyecto-Final-Analisis-de-datos/blob/main/06_INEC%20to%20SQL%20Server/IMPORT_TO_SQLSERVER.ipynb)

--- 

### SQL-server-a-MongoDB-Atlas

Para realizar una migracion de una base de datos de SQL-SERVER a MongoDB Atlas se debe importar las siguientes librerias las cual nos va a poder ayudar a conectar con los servidores. 

```py
import pyodbc
import sqlite3 as sq
from pymongo import MongoClient
```

Lo primero es establecer las conexiones con los servidores, primero es conectarse con SQL server y es importante seleccionar el nombre de la base de datos para que sea transferida de forma directa al MongoAtlas.

```py
#Conectar con el servidor SQL SERVER
conn = pyodbc.connect('Driver={SQL Server};'
                      'Server=DESKTOP-QTJIJML;'
                      'Database=estudiantes;'
                      'Trusted_Connection=yes;')

cursor = conn.cursor()
```

Se bebe crear una variable en el cual debe contener un cursor directamente desde la conexion de SQL server, una vez realizado la conexion con el servidor con el lenguaje en SQL se crea una variable en el cual se selecciona la tabla de la base de datos y finalemente con una variable se alamacena.
```py
mycursor = conn.cursor()
mysql = "SELECT * FROM estudiantes"
mycursor.execute(mysql)
myresult = mycursor.fetchall()
```

Se declara una variavle en el cual va a conetener el url de la conexion a mongoDB, luego se crea una base de datos y despues una nueva coleccion.
```py
client = MongoClient("mongodb+srv://miguel:miguel@cluster0.ed8kj.mongodb.net/test")

DBS = client.get_database('estudiantes')
db = DBS.sql
```

Mediante un for y con un contador se debe colocar el nombre de todas las colummnas que van hacer transferidas, y con try  - except se verificara si cada una de las filas y columnas son alamcenadas con exito en MongoDB Atlas

```py
for row in myresult:
    doc={}
    doc['Provincia']=row[0],
    doc['Canton']=row[1],
    doc['Parroquia']=row[2],
    doc['Femenino']=row[3],
    doc['Masculino']=row[4],
    doc['Textbox17']=row[5],
    doc['Textbox6']=row[6],
    doc['Textbox7']=row[7],
    doc['Textbox18']=row[8],
    try:
       print(doc)
       db.insert_one(doc)
       print("Migracion exitosa")
    except Exception as ex:
        print(ex)
```
Puedes encontrar mucho más de cómo utilizar este script en [SQL-server-a-MongoDB-Atlas](https://github.com/Miguel-EMC/Proyecto-Final-Analisis-de-datos/blob/main/06_INEC%20to%20SQL%20Server/SQL_SERVER_TO_MONGO.ipynb)


### Analisis PowerBI

En el análisis de datos sobre los estudiantes de bachilleratos registrados en el periodo 2012 – 2013, se ha podido determinar que la mayoría de los estudiantes son de la provincia del Guayas donde también existe la mayoría de la población en la provincia, después le sigue la provincia de pichincha y donde existe una menor cantidad de estudiantes de igual manera son en las provincias menos pobladas que lo es galápagos y las provincias de la amazonia.

![image](https://user-images.githubusercontent.com/74844624/155896381-e63a4613-5db6-44f3-8685-680e32e5dc3c.png)


## WebScraping to PostgreSQL

* [Importar un archivo CSV a PostgreSQL]()
* [Migrar un database en PostgreSQL a MongoDB Atlas]()
* [Analisis PowerBI]()

- Importar las librerías necesarias para establecer una conexión con la base PostgreSQL y las librerías de BeautifulSoup para extraer los datos de una pagina web
```py
##Librerias
from bs4 import BeautifulSoup
import requests
import pandas as pd
import psycopg2
```
- Establecer la conexión con la base de datos con sus resectivas credenciales 
```py
###Conexion####
conn = psycopg2.connect(host="localhost", database="webscraping", user="postgres", password="1234", port="5432")
conn.autocommit = True 
cur = conn.cursor()
```
- Mediante una instruccion sql enviamos un query que cree la table Noticias_Scraping con sus respectivos atributos
```py
##Query
cur.execute('''CREATE TABLE Noticias_Scraping(N_Id int NOT NULL,\
Titulo text,\
Descripcion text,\
Autor varchar(50),Fuente varchar(50), Fecha varchar(50));''')
conn.commit()
```
- Inicializar variables que se usaran mas adelante
```py
i=1
count = 2
tablelist=[]
url='https://www.bbc.com/mundo/topics/c2lej05epw5t'
```
- Con el while se puede definar cuantas paginas se desea extraer , ademas de buscar las debidas etiquetas en el código html ara poder extraer todos los datos deseados. Existen condicionales if que verifican que esa etiqueta tenga texto, caso contrario establecerá su variable como nulo
```py
while count <=50 :
    req = requests.get(url)
    soup = BeautifulSoup(req.text, 'html.parser')
    league = soup.find('ol',class_ = 'gs-u-m0 gs-u-p0 lx-stream__feed qa-stream')
    for team in league.find_all('li', class_= 'lx-stream__post-container'):
        num = team.find('a', class_ = 'qa-heading-link lx-stream-post__header-link').text.strip()
        t = team.find('p', class_ = 'lx-stream-related-story--summary qa-story-summary')
        if t is not None:
            nombre= t.text.strip()
        else:
            nombre =None
        t2 = team.find('p', class_ = 'qa-contributor-name lx-stream-post__contributor-name gel-long-primer gs-u-m0')
        if t2 is not None:
            Tipo = t2.text.strip()
        else:
            Tipo = None
        t3 = team.find('p', class_ = 'qa-contributor-role lx-stream-post__contributor-description gel-brevier gs-u-m0')
        if t3 is not None:
            fuente=t3.text.strip()
        else :
            fuente = None
        t4 = team.find('span', class_ = 'gs-u-vh qa-visually-hidden-meta')
        if t4 is not None:
            fecha=t4.text.strip()
        else:
            fecha = None
```
- Se envían los datos mediante una instrucción query con los respectivos valores extraídos en el paso anterior
```py
        cur.execute("INSERT INTO Noticias_Scraping VALUES (%s,%s,%s,%s,%s,%s)",(i,num,nombre,Tipo,fuente,fecha))
```
- Se crea un archivo formato json para almacenar los datos y posterior a eso enviar estos datos a una lista para que mediante la librería pandas se pueda crear un data frame y por consecuente un archivo csv. Por ultimo cerramos la conexión con la base de datos

```py
        json ={
            "Titulo": num,
            "Descripcion": nombre,
            "Autor": Tipo,
            "Fuente": fuente,
            "Fecha": fecha
        }
        tablelist.append(json)
        i+=1
    subS = 'https://www.bbc.com/mundo/topics/c2lej05epw5t/page/'+ str(count)
    url = subS
    count+=1

df= pd.DataFrame(tablelist)
df.to_csv('Noticias.csv')
   
conn.close()
```
- Verificamos que los datos se hayan enviado correctamente hacia PostreSQL
![image](https://user-images.githubusercontent.com/74793607/155899278-5fc1bbcd-e4b7-4e5b-b46f-cf6add6abf67.png)

Puedes encontrar mucho más de cómo utilizar este script en [Web Scraping (Noticias) a PostgreSQL (Base SQL)]()


### Envio de datos hacia MongoDB
- Importar las librerías para establecer una conexión tanto con PostgreSQL y MongoDB`

```py
import psycopg2
import pymongo
from pymongo import MongoClient
from pymongo.errors import ConnectionFailure
```
- Establecer conexión con la base de datos MongoDB con las respectivas credenciales
```py
cliente = MongoClient('localhost',27017)
db = cliente["Noticias"]
Noticias = db.noticias
```
- Establecer conexión con la base de datos PostgreSQL con las respectivas credenciales 
```py
conn = psycopg2.connect(host="localhost", database="webscraping", user="postgres", password="1234", port="5432")
cur = conn.cursor()
```
- Con una instrucción SQL extraemos todos los datos de la base de datos PostgreSQL
```py
Query = "Select * from noticias_scraping "
cur.execute(Query)
```
- Con la función .fetchall() organizamos todos los datos estableciendo sus cabezeras para que estos se puedan exportar de una manera adecuada a la base de datos MongoDB
```py
scraping= cur.fetchall()
```
- Con el uso de un for guardamos todos los datos en archivo tipo json con sus respectivas cabeceras.
```py
for row in scraping:
    teamingLeague = [{
        "Id" : row[0],
        "Titulo" : row [1],
        "Descripcion" : row[2],
        "Autor" : row[3],
        "Fuente" : row[4],
        "Fecha" : row[5]
    }]
```
- Se envían los datos recopilados a la base de datos mongoDB y por ultimo cerramos la conexión con la base de datos PostgreSQL
```py
    Noticias.insert_many(teamingLeague)
conn.close()
```
- Se comprueba que los datos se hayan enviado correctamente hacia MongoDB
![image](https://user-images.githubusercontent.com/74793607/155899480-3751e588-ddbe-494c-80b5-d1754c9e23fb.png)

Puedes encontrar mucho más de cómo utilizar este script en [Envio de datos hacia MongoDB]()

### Analisis 
- Para el analisis  del dataset extraido mediante webscraping se utiliza herramientas que solo se relacionen con texto, ya que como el tema principal son noticias, es muy dificil poder ponderar estos datos y convertirlos en graficos estadisticos.
![image](https://user-images.githubusercontent.com/74793607/155899661-3e63dad8-e69f-4577-abc2-a9be8d27b290.png)

- En el siguiente ejemplo se puede observar como mediante un filtro de palabras y fuente  se puede visualizar las noticias que cumplan con todos estos filtros que hemnos establecido, Ademas que el grafico inferior se pueden observar las palabras que mas se repiten.
![image](https://user-images.githubusercontent.com/74793607/155899777-6677dce3-e7a8-4a73-9b4a-ef476bb7b708.png)


## Datos abiertos to MySQL

* [Importar un archivo CSV a MySQL]()
* [Migrar un database en MySQL a MongoDB Atlas]()
* [Analisis PowerBI]()

Extraeremos el archivo estático desde la página del gobierno “DATOS ABIERTOS”, específicamente el tema de “personas perdidas”. 
[Datos abiertos](https://datosabiertos.gob.ec/)

![image](https://user-images.githubusercontent.com/74982150/155870656-476c702c-dd07-4462-831d-73d24416778a.png)

- Procedimiento

Importaremos algunas librerías para poder realizar tanto la conexión para la base de datos MYSQL y poder leer el archivo que vamos a extraer de las páginas de archivos estáticos.

```py
import mysql.connector as msql
import pandas as pd
from sqlalchemy import create_engine
```

Establecemos el nombre del host, el usuario y la contraseña de nuestro servidor de MYSQL, y posteriormente realizaremos esta conexión mediante un if, identificaremos si dicha conexión es exitosa o no, además de crear una variable para poder realizar las operaciones en lenguaje SQL en Python.

```py
connections = msql.connect(host = 'localhost', user = 'root', password='123456')
if connections.is_connected():
    cursor = connections.cursor()
    print("Conexión Exitosa")
else:
    print("Conexión Rechazada")
```

Con la variable antes mencionada, crearemos mediante lenguaje SQL, una nueva base de datos dentro de MYSQL con la siguiente línea:

```py
cursor.execute("CREATE DATABASE PersonasPerdidas;")
```

Crearemos una consulta para poder demostrar que la base de datos “PersonasPerdidas” se haya creado dentro de la base de datos de MYSQL.

```py
consulta = pd.read_sql("show databases;",connections)
consulta
```

Estableceremos la conexión hacia MYSQL desde Python, añadiendo el usuario, contraseña y por ultimo la base de datos que vamos a utilizar en este caso “PersonasPerdidas”

```py
engine = create_engine('mysql+mysqldb://root:123456@localhost:3306/PersonasPerdidas')
consulta
```

Cargaremos a la variable “df” gracias a la librería de pandas, el documento que extrajimos de la página de archivos estáticos mediante la extensión csv, también para poder leer este archivo hemos necesitado declarar el tipo de separador que utiliza nuestro archivo, caso contrario las columnas al momento de extraer se unen, adicionalmente utilizaremos ecoding para poder leer este archivo y para que no existan errores dentro de la lectura del archivo.

```py
df = pd.read_csv("mdg_personasdesaparecidas_pm_2021_enero_diciembre.csv", sep=";" ,encoding='latin-1')
```

Como último paso, añadiremos la variable que ya contiene el archivo, crearemos la tabla que va ir en la base de datos, en este caso con el nombre de “información”, añadiremos la conexión previamente creada y pasaremos toda la información del archivo CSV  a la base de datos de MYSQL.

```py
try:
    df .to_sql('información', con=engine, if_exists = 'replace', index = False)
    print("creación y almacenamiento completados")
except Exception as e:
    print(e)
```

![image](https://user-images.githubusercontent.com/74982150/155870977-b0c469a5-9d8e-4f3b-a454-8634b177adf5.png)

![image](https://user-images.githubusercontent.com/74982150/155870981-8567f4e5-61fe-419d-ba3b-c550f0a16c32.png)

Puedes encontrar mucho más de cómo utilizar este script en [ARCHIVO ESTÁTICO A MYSQL](https://github.com/Miguel-EMC/Proyecto-Final-Analisis-de-datos/blob/main/08_Datos%20abiertos%20to%20MySQL/Import_csv_to_mysql.ipynb)

---

### MYSQL A MONGODB-ATLAS

Utilizaremos las siguientes librerías para poder realizar esta transición entre base de datos.

```py
from argparse import ArgumentParser
from pymongo import MongoClient
from pymongo.errors import ConnectionFailure
import mysql.connector as msql
import pandas as pd
from sqlalchemy import create_engine
import certifi
import numpy as np
```

Crearemos la conexión hacia MONGODB ya establecido como conectador de datos, añadiendo que en este caso se va a tratar de MONGODB -ATLAS, para esto utilizaremos el clouster en el MONGODB en la nube, comprobaremos el éxito de esta conexión, y adicionalmente crearemos el nombre de la base de datos y colección para MONGODB y guardándolos en distintas variables.

```py
try:
    ca = certifi.where()
    client = MongoClient('mongodb+srv://miguel:miguel@cluster0.ed8kj.mongodb.net/test', tlsCAFile=ca )

    client.server_info()
    print("Conexion exitosa")
    client.close
except pymongo.errors.ServerSelectionTimeoutError as errorTiempo:
    print("Conexión rechazada")
dbm = client['Mysql_to_Mongodb']
cole = dbm['Datos_de_SQL']
```

Volveremos a establecer la conexión hacia MYSQL.

```py
engine = create_engine('mysql+mysqldb://root:123456casa@localhost:3306/PersonasPerdidas')
```

```py
connections = msql.connect(host = 'localhost', user = 'root', password='123456', database ='PersonasPerdidas')
if connections.is_connected():
    cursor = connections.cursor()
    cursor.execute("select database();")
    record = cursor.fetchone()
    print("Se conectó a la base de datos: ", record)
```

Crearemos el dataframe para poder pasar hacer la trasición de MYSQL hacia MONGODB, almacenaremos todo esto en una lista, para posteriormente mediante append para ir almacenando los múltiples datos y pasarlos hacia MONGODB-ATLAS.

```py
def createDocsFromDF(documento, collection = None, insertToDB=False):
    docs = []
    fields = [col for col in documento.columns]
    for i in range(len(documento)):
        doc = {col:documento[col][i] for col in documento.columns if col != 'index'}
        for key, val in doc.items():
            if type(val) == np.int64:
                doc[key] = int(val)
            if type(val) == np.float64:
                doc[key] = float(val)
            if type(val) == np.bool_:
                doc[key] = bool(val)
        docs.append(doc) 
    if isinstance(docs, list): 
        cole.insert_many(docs)   
    else: 
        cole.insert_one(docs)
    print("guardado exitosamente")    
    return docs 
```


```py
createDocsFromDF(documento)
```

```py
guardado exitosamente
Output exceeds the size limit. Open the full output data in a text editor

[{'Provincia': 'PICHINCHA',
  'Latitud': '-0,156852339',
  'Longitud': '-78,47783944',
  'Edad Aprox.': 29,
  'Sexo': 'HOMBRE',
  'Motivo Desaparción': 'PROBLEMAS SOCIALES',
  'Motivo Desaparción Obs.': 'INFLUENCIA DE AMISTADES',
  'Fecha Desaparición': '6/8/2021',
  'Situación Actual': 'ENCONTRADO',
  'Fecha Localización': '8/8/2021',
  '_id': ObjectId('621713c7f07d4a11cc5add7e')},
 {'Provincia': 'MORONA SANTIAGO',
  'Latitud': '-2,0021974',
  'Longitud': '-77,9967043',
  'Edad Aprox.': 15,
  'Sexo': 'MUJER',
  'Motivo Desaparción': 'PROBLEMAS SOCIALES',
  'Motivo Desaparción Obs.': 'INFLUENCIA DE AMISTADES',
  'Fecha Desaparición': '15/7/2021',
  'Situación Actual': 'ENCONTRADO',
  'Fecha Localización': '9/8/2021',
  '_id': ObjectId('621713c7f07d4a11cc5add7f')},
 {'Provincia': 'AZUAY',
  'Latitud': '-2,882362',
  'Longitud': '-79,0589399',
  'Motivo Desaparción Obs.': 'FAMILIA DISFUNSIONAL',
  'Fecha Desaparición': '13/6/2021',
  'Situación Actual': 'ENCONTRADO',
  'Fecha Localización': '16/6/2021',
  '_id': ObjectId('621713c7f07d4a11cc5ae165')},
 ...]
```

Puedes encontrar mucho más de cómo utilizar este script en nuestra [MYSQL A MONGODB-ATLAS](https://github.com/Miguel-EMC/Proyecto-Final-Analisis-de-datos/blob/main/08_Datos%20abiertos%20to%20MySQL/MySQL_to_MongoDB.ipynb)

--- 

### ANÁLISIS EN POWERBI
Se realizó en el análisis del tema seleccionado “personas desaparecidas”, analizando primero la cantidad de personas desaparecidas por provincia, destacando en ella que las principales provincias que tienen un mayor número de casos son las del Guayas y Pichincha, esto se debe a que son provincias muy pobladas y por ende el número siempre va a ser alto a diferencia de otras provincias, otro punto a destacar es la provincia de Galápagos, que al ser una zona netamente turística tiene un gran control por lo no tiene mucha probabilidad de que una persona se pierda.

![image](https://user-images.githubusercontent.com/74982150/155871162-bdef92bf-0fd5-44d4-9056-879fb6ccecab.png)

Tendremos un segundo análisis sobre la cantidad de personas desaparecidas, mediante su tipo de género, en este caso, tendremos una gran diferencia entre hombres y mujeres, siendo así la cantidad de mujeres que desaparecen superó por mas de un 50% a los hombres durante el año 2021 en todas las provincias del Ecuador, siguiendo con el análisis tendremos la fecha en la cuál las personas desaparecen igualmente por provincias, y por último tendremos la razón por la cuál se da esta situación, destacando dos que son las que tienen más porcentaje, estos serían problemas familiares y problemas sociales, seguidos de otro porcentaje alto en gente que no se pudo reportar el motivo. 

![image](https://user-images.githubusercontent.com/74982150/155871184-daf57eec-c10e-4759-851c-370cf333bd9f.png)


En conclusión las personas tienden a desaparecer por motivos financieros, problemas sociales pero principalmente por problemas familiares, dentro de estos casos tenemos que las mujeres suelen ser las que tienen una mayor taza de desaparición, por otro lado tenemos una gran cantidad de estas que han sido encontradas y es un punto positivo teniendo un porcentaje muy bajo en personas que aún no han sido encontradas y aún menor en personas fallecidas.

![image](https://user-images.githubusercontent.com/74982150/155871191-548461b8-edb3-4390-a87b-9b2a0416b285.png)

![image](https://user-images.githubusercontent.com/74982150/155871199-de41546a-ac27-49db-95d5-a4ef4de24128.png)


## Video de Youtube 📌

En el siguiente enlace se podra visualizar todos los procedimiento que se realizo [SemVer](http://semver.org/)



