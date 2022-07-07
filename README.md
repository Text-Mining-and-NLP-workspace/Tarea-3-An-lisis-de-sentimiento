<a href="https://www.uvg.edu.gt/"><img align="left" src="https://www.uvg.edu.gt/wp-content/uploads/socialshare-logo.jpg" width="90" height="90"></a>
**_Corporate Master in Applied Data Science_**<br/>
**_Text Mining & Natural Language Processing_**<br/>
**_Catedratico: Pedro Alberto Aguilar Nuñez_**<br/>
<br/>

Integrantes:
- Aldo Montenegro Margnoni
- Gabriel Fernando Montenero Ortiz
- Axel Adolfo Muralles Carranza
- German Antonio Oliva Muralles

# Tarea 3 Analisis de Sentimiento

- [Descripcion](#descripcion)
- [Requerimientos](#requerimientos)
- [Instrucciones](#instrucciones)
- [Metodologia y Resultados](#metodologia-y-resultados)
- [Contribuciones](#contribuciones)



## Descripcion:
La tarea numero 3 consiste en la elaboaracion de la creacion de funciones para predecir y evaluar un modelo de Naive Bayes ára analisis de sentimiento, tambien cuenta con la integracion del pipeline de preprocesamiento y se realiza una seleccion de mejor modelo a partir de la iteracion de los valores de hyperparametros.

## Requerimientos:
- Requiere instalacion de [Anaconda Distribution](https://www.anaconda.com/products/distribution) o [miniconda](https://docs.conda.io/en/latest/miniconda.html)

## Instrucciones:

clonamos este repositorio en el directorio deseado desde una terminal, para windows podemos utilizar [Git Bash](https://gitforwindows.org/) 
```
git clone https://github.com/Text-Mining-and-NLP-workspace/Tarea-3-Analisis-de-sentimiento.git
```
Desde la terminal o anaconda prompt (windows) creamos un ambiente virtual con conda (reemplazar my_enviroment con el nombre deseado)
```
conda create -n my_enviroment
```
cuando conda pregunte por la confirmacion responder con _y_
```
proceed ([y]/n)?
```
una vez creado el ambiente virtual, proceder a activarlo
```
conda activate my_enviroment
```
instalamos los siguientes paquetes en nuestro ambiente:
```
pip install jupyter
pip install notebook
pip install "spacy[lookups]"
python -m spacy download en_core_web_trf
```
nos cambiamos hacia el path en donde se clono el repositorio
```
cd Tarea-3-Analisis-de-sentimiento
```
ejecutamos nuestro notebook
```
jupyter notebook "sentiment analysis.ipynb"
```

## Metodologia y Resultados:
Para nuestro modelo clasificador de analisis de sentimiento, contamos con una clase llamada NB_sentiment_analysis, que cuenta con tres metodos: fit, predict y val_test. esta clase acepta como parametros los hyperparametros del modelo (la definicion de los hyperparametros lemmatization y stopwords se utilizan unicamente para el metodo predict, para el metodo fit y val_test los datos tokenizados de entrada deben estar previamente preprocesados) 


el metodo fit toma como entrada dos sets de datos tokenizados el primero de la clase positiva y el segundo de la clase negativa, estos sets tokenizaods pueden estar lemmatizados o no, y pueden contener stopwords o no, esto lo tomaremos como un hyperparametro para el procesamiento, por lo cual generamos 4 datasets resultante de la combinacion de los posibles valores de estos dos hyperparametros




![results_best_model](https://user-images.githubusercontent.com/70925688/177268184-00c3f1ee-3f1b-4832-a707-1ca9e5f5f11c.JPG)

## Contribuciones

- Aldo Montenegro Margnoni
	- Tokenizacion y preparacion de data
	- metodo de prueba de hyperparametros 
<br/>

- Gabriel Fernando Montenero Ortiz
	- Optimizacion en metodo para remover stopwords
	- organizacion de funciones en pipeline
    
<br/>

- Axel Adolfo Muralles Carranza
	- Elaboracion de clase para modelo, metodos fit, predict y val_test
	- seleccion de Hyperparametros

<br/>

- German Antonio Oliva Muralles
	- Pruebas para obtener mejor modelo
	- Sanity Check

<br/>
