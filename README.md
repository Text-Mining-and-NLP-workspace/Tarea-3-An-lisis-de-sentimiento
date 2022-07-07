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
La tarea numero 3 consiste en la elaboaracion de la creacion de funciones para predecir y evaluar un modelo de Naive Bayes para analisis de sentimiento, tambien cuenta con la integracion del pipeline de preprocesamiento y se realiza una seleccion de mejor modelo a partir de la iteracion de los valores de hyperparametros.

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

```
model=NB_sentiment_analysis(stopwords=True,lemmatization=True,ngrams=True,n=2,ngrams_mincount=5,ngrams_th=10)
```
El metodo fit toma como entrada dos sets de datos tokenizados el primero de la clase positiva y el segundo de la clase negativa, estos sets tokenizaods pueden estar lemmatizados o no, y pueden contener stopwords o no, esto lo tomaremos como un hyperparametro para el procesamiento, por lo cual generamos 4 datasets resultante de la combinacion de los posibles valores de estos dos hyperparametros.

```
model.fit(positive_class_tokenized_train_dataset,negative_class_tokenized_train_dataset)
```

metodo predict lo podemos utilizar para clasificar documentos individuales de la siguiente manera, la entrada de este metodo es el documento crudo, es decir sin tokenizar ni preprocesar, como prerequisito se requiere haber llamado el metdo fit.
```
sentence='the hotel was very nice, but dirty'
model.predict(sentence)
```

El metodo val_test se utiliza para validar/probar nuestro modelo entrenado, tiene por entrada los datasets tokenizados de validacion o prueba para las clases positiva y negativa, es necesario haber llamado el metodo fit como prerequisito. las metricas reultado de este metodo se pueden consultar con la variable self.metrics

```
model.fit(positive['train'],negative['train'])
model.val_test(positive['validation'],negative['validation'])
print('Validation Metrics')
print(model.metrics)
```

Para la seleccion de nuestro mejor modelo, procedemos a probar valores de nuestros hyperarametros, con el fin de poder realizar esta iteracion con mayor agilidad, se generaron 4 sets de datos con los posibles valores de lemmatization, stopwords, y sus respectivas clases positiva y negativa, estos datasets se encuentran dentro de la carpeta data/interim guardados como archivos pkl, para poderlos cargar rapidamente a nuestro notebook.

despues se realiza un bucle sobre estos cuatro datasets y el hyperparametro ngrams=False, ya que este valor anula los otros hyperparametros, y por ultimo se realiza el bucle completo sobre los siguientes 3 hyperparametros con el valor ngrams=True y los 4 sets de datos. esto nos da como resultado 196 posibles modelos, los cuales son entranados, evaluados y sus metricas almacenadas dentro de un dataframe para poder realizar al comparacion posteriormente.

![metrics](https://user-images.githubusercontent.com/70925688/177722218-acf92863-0140-4447-af5d-801917415959.JPG)

Seleccionamos F1 como nuestra metrica principal ya que buscamos minimizar tanto los falsos posiitvos como los falsos negativos para poder clasificar con la mayor certeza ambas clases, por lo cual observamos cual es nuestro modelo con F1 mas alto

![results_best_model](https://user-images.githubusercontent.com/70925688/177268184-00c3f1ee-3f1b-4832-a707-1ca9e5f5f11c.JPG)

De lo anterior observamos que 98 de nuestros modelos cuentan con un F1 del 100%, por lo cual escogeremos el cual nos es mas facil y rapido de entrenar y poner en produccion, podemos observar que ese seria el que tiene por hyperparametros, que no se ejecute Lemmatizacion, no se quiten stopwords y no se generen ngrams. debido a que los documentos unicamente pasan por un preprocesamiento simple antes de ser entrenado el modelo, esto toma 2 segundos de realizar en nuestros documentos y toma menos de un segundo entrenar nuestro modelo

![prepro](https://user-images.githubusercontent.com/70925688/177723553-313f6fbf-0da1-4785-9cef-290b164371b7.JPG)
![tiempos](https://user-images.githubusercontent.com/70925688/177723186-b7dcf22a-a55c-4bae-9a5e-f4bc6e8a6e05.JPG)

con este modelo entrenado, obtenemos las siguientes metricas para validacion y prueba, respectivamente

![val_met](https://user-images.githubusercontent.com/70925688/177724014-25a191c0-182d-49ad-9439-22d3572c3d00.JPG)
![test_met](https://user-images.githubusercontent.com/70925688/177724075-47cedfe9-487c-4528-a736-bfcfd0808f7b.JPG)



## Contribuciones

- Aldo Montenegro Margnoni
	- Tokenizacion y preparacion de data
	- Metodo de prueba de hyperparametros 
<br/>

- Gabriel Fernando Montenero Ortiz
	- Optimizacion en metodo para remover stopwords
	- Organizacion de funciones en pipeline
    
<br/>

- Axel Adolfo Muralles Carranza
	- Elaboracion de clase para modelo, metodos fit, predict y val_test
	- seleccion de Hyperparametros

<br/>

- German Antonio Oliva Muralles
	- Pruebas para obtener mejor modelo
	- Sanity Check

<br/>
