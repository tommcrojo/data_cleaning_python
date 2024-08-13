# Limpieza de Datos con Pandas

## Introducción
En este proyecto, se nos ha solicitado limpiar una tabla de clientes para que el equipo de ventas pueda contactarlos de manera eficiente. El objetivo principal es hacer que esta tabla sea lo más legible posible, permitiendo que nuestros compañeros del sector de ventas realicen su trabajo de manera óptima. Además, solo incluiremos los contactos que son aptos para recibir llamadas.

## Objetivos
- **Claridad:** Asegurar que la tabla de clientes sea fácil de leer y entender.
- **Filtrado:** Incluir únicamente los contactos a los que se les puede llamar.

## Herramientas y Librerías Usadas
- **Python:** Lenguaje de programación principal utilizado en este proyecto.
- **Pandas:** Librería utilizada para la manipulación y análisis de datos.

## Procedimiento

### 1. Importación de Librerías
Primero, importamos la librería Pandas que utilizaremos a lo largo del proyecto.

```python
import pandas as pd
```

### 2. Carga de Datos
A continuación, cargamos los datos desde un archivo de Excel y realizamos una primera inspección para ver con qué estamos trabajando.

```python
df = pd.read_excel('data_cleaning_python/input/Customer Call List.xlsx')
df.head()
```

### 3. Revisión Inicial de la Tabla
Observamos la estructura y el contenido de la tabla. Esto nos ayuda a identificar posibles problemas, como datos faltantes, columnas innecesarias o inconsistencias.

```python
print(df.info())
print(df.describe())
```

### 4. Limpieza de Datos
En esta sección nos enfocamos en la limpieza de los datos. Esto incluye la eliminación de columnas innecesarias, el tratamiento de valores nulos, y la normalización de los datos.

#### 4.1 Eliminación de Columnas Innecesarias
Eliminamos cualquier columna que no aporte valor al análisis o que no sea relevante para el equipo de ventas.

```python
df = df.drop(['Not_Useful_Column'], axis=1)
```

#### 4.2 Tratamiento de Valores Nulos
Revisamos las columnas críticas para asegurarnos de que no contengan valores nulos que puedan afectar el análisis. Es crucial asegurarse de que los datos clave, como los números de teléfono y nombres, estén completos y correctos.

```python
df = df.dropna(subset=['Phone_Number', 'First_Name'])
```



#### 4.3 Normalización de Datos
Nos aseguramos de que los datos estén en un formato coherente, especialmente en las columnas que afectan el contacto con los clientes.

```python
df['Phone_Number'] = df['Phone_Number'].str.replace(r'\D', '', regex=True)
```

### 5. Filtrado de Clientes
Finalmente, filtramos los clientes que no deben ser contactados. Aquí nos aseguramos de que solo estamos incluyendo a los clientes que realmente interesan a nuestro equipo de ventas.

```python
df_final = df[(df['Do_Not_Contact'] == 'N')]
```
### 6. Exportación en formato Excel
Exportamos la nueva tabla en un formato útil para los compañeros de ventas

```python
df.to_excel("clientes.xlsx",
            sheet_name="Contactar Clientes",
            index=True
           )
```

## Aplicación Práctica en el Análisis de Datos
Este proyecto demuestra cómo un proceso riguroso de limpieza de datos puede facilitar la toma de decisiones dentro de una empresa. En este caso, la limpieza y filtrado de la tabla de clientes permite que el equipo de ventas pueda enfocarse únicamente en los clientes relevantes, mejorando la eficiencia y efectividad de su trabajo.
