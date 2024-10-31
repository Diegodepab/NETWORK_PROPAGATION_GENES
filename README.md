# **Propagación de Redes en Bioinformática**

## **Introducción**

La propagación de redes es una técnica computacional clave en el análisis de estructuras de redes, especialmente en el ámbito de las ciencias biológicas. Su objetivo principal es difundir información o "señales" a través de una red, donde los nodos representan elementos como genes o proteínas, y los bordes reflejan sus relaciones, como interacciones o correlaciones. Este proceso amplifica señales débiles al distribuir datos desde un subconjunto inicial de nodos, permitiendo la identificación de patrones y relaciones que no son evidentes a partir de las interacciones directas.

Los algoritmos de propagación de redes, como Random Walk with Restart (RWR) y Heat Diffusion (HD), utilizan la actualización iterativa de valores en los nodos en función de sus vecinos, logrando un equilibrio entre influencias locales y globales.

En este trabajo se hará uso de las herramientas:

- **DIAMOnD** (Disease Module Detection)
- **GUILD** (Genes Underlying Inheritance Linked Disorders)

### **DIAMOnD**

DIAMOnD se centra en la identificación de módulos de enfermedades dentro de redes de interacción proteína-proteína. Su metodología agrega nodos a conjuntos de genes de enfermedades conocidos en función de su proximidad topológica, construyendo módulos coherentes que probablemente estén involucrados en procesos biológicos relacionados. Aunque DIAMOnD destaca en la priorización de genes asociados a enfermedades, su efectividad puede verse limitada al considerar grandes volúmenes de genes candidatos. En conjunto, tanto GUILD como DIAMOnD ilustran la aplicabilidad de la propagación de redes en el análisis de complejas interacciones biológicas.

Este proyecto incluye código modificado del repositorio [DIAMOnD](https://github.com/dinaghiassian/DIAMOnD), cuya autora intelectual es [Susan Dina Ghiassian](https://github.com/dinaghiassian).


## **Datos de Entrada**

Para aplicar DIAMOnD se necesitarán los siguientes puntos definidos previamente:

1. **network_file** (archivo de red): Este archivo contiene una lista de interacciones entre genes (o nodos de una red). Se espera que esté en formato de lista de aristas (edgelist), donde cada fila tiene dos columnas que representan una interacción entre dos genes (gene1 y gene2).

2. **seed_file** (archivo de genes semilla): Este archivo contiene una lista de genes "semilla", que son los genes iniciales alrededor de los cuales se expandirá la red utilizando DIAMOnD. Para este trabajo se implementó un código capaz de crear un `seed_file` automáticamente basado en el `network_file`.

3. **n** (número de genes DIAMOnD): Este parámetro especifica cuántos genes adicionales se deben agregar a los genes semilla en el proceso de expansión de la red. Un valor común para este parámetro es 200.

4. **alpha** (peso de las semillas, opcional): Es un número entero que indica la importancia o el "peso" que se da a los genes semilla en el algoritmo. El valor predeterminado es 1, lo que significa que se les da un peso normal.

### **Generación de seed_file**

El código para generar el `seed_file` incluye tres métodos de selección de nodos:

1. **Selección basada en grado**: Este método selecciona nodos en función del número de conexiones que tienen. Los nodos con un mayor grado (más conexiones) son más relevantes en la red y se eligen como semillas.

2. **Selección basada en centralidad**: Utiliza la centralidad de intermediación para identificar nodos que actúan como "puentes" entre diferentes módulos. Esto significa que se seleccionan nodos que tienen un papel crucial en conectar otras partes de la red, lo que puede ser útil para la propagación de señales.

3. **Selección aleatoria**: Este método escoge nodos sin un criterio previo, proporcionando una forma simple y rápida de seleccionar genes semilla, aunque puede no ser tan efectiva como los métodos anteriores.

## **Instalación**

Para instalar las dependencias necesarias, asegúrate de tener [Python](https://www.python.org/downloads/) y [pip](https://pip.pypa.io/en/stable/installation/) instalados en tu sistema. Luego, ejecuta:
