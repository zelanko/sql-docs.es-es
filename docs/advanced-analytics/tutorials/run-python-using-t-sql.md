---
title: Ejecutar Python mediante T-SQL | Documentos de Microsoft
ms.custom: 
ms.date: 09/19/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: Python
caps.latest.revision: "2"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: f2eba50d5c5e57025462c46b38fc0ddbfc947ea0
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="run-python-using-t-sql"></a>Ejecución de Python mediante T-SQL

Este ejemplo muestra cómo puede ejecutar un script de Python simple en SQL Server, mediante el procedimiento almacenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)

## <a name="step-1-create-the-test-data-table"></a>Paso 1. Crear la tabla de datos de prueba

En primer lugar, creará algunos datos adicionales, que se utilizará al asignar los nombres de los días de la semana a los datos de origen. Ejecute la siguiente instrucción de T-SQL para crear la tabla.

```SQL
CREATE TABLE PythonTest (
    [DayOfWeek] varchar(10) NOT NULL,
    [Amount] float NOT NULL
    )
GO

INSERT INTO PythonTest VALUES
('Sunday', 10.0),
('Monday', 11.1),
('Tuesday', 12.2),
('Wednesday', 13.3),
('Thursday', 14.4),
('Friday', 15.5),
('Saturday', 16.6),
('Friday', 17.7),
('Monday', 18.8),
('Sunday', 19.9)
GO
```

## <a name="step-2-run-the-hello-world-script"></a>Paso 2. Ejecute el script de "Hello World"

El código siguiente carga el archivo ejecutable de Python, pasa los datos de entrada y para cada fila de datos de entrada, actualiza el nombre de día de la tabla con un número que representa el índice del día de la semana.

Tome nota del parámetro  *@RowsPerRead* . Este parámetro especifica el número de filas que se pasan al tiempo de ejecución de Python de SQL Server.

La biblioteca de análisis de datos de Python, conocido como **pandas**, es necesario para pasar datos a SQL Server y se incluye de forma predeterminada con los servicios de aprendizaje de máquina.

```sql
DECLARE @ParamINT INT = 1234567
DECLARE @ParamCharN VARCHAR(6) = 'INPUT '

print '------------------------------------------------------------------------'
print 'Output parameters (before):'
print FORMATMESSAGE('ParamINT=%d', @ParamINT)
print FORMATMESSAGE('ParamCharN=%s', @ParamCharN)

print 'Dataset (before):'
SELECT * FROM PythonTest

print '------------------------------------------------------------------------'
print 'Dataset (after):'
DECLARE @RowsPerRead INT = 5

execute sp_execute_external_script 
@language = N'Python',
@script = N'
import sys
import os
print("*******************************")
print(sys.version)
print("Hello World")
print(os.getcwd())
print("*******************************")
if ParamINT == 1234567:
       ParamINT = 1
else:
       ParamINT += 1

ParamCharN="OUTPUT"
OutputDataSet = InputDataSet

global daysMap

daysMap = {
       "Monday" : 1,
       "Tuesday" : 2,
       "Wednesday" : 3,
       "Thursday" : 4,
       "Friday" : 5,
       "Saturday" : 6,
       "Sunday" : 7
       }

OutputDataSet["DayOfWeek"] = pandas.Series([daysMap[i] for i in OutputDataSet["DayOfWeek"]], index = OutputDataSet.index, dtype = "int32")
', 
@input_data_1 = N'SELECT * FROM PythonTest', 
@params = N'@r_rowsPerRead INT, @ParamINT INT OUTPUT, @ParamCharN CHAR(6) OUTPUT',
@r_rowsPerRead = @RowsPerRead,
@paramINT = @ParamINT OUTPUT,
@paramCharN = @ParamCharN OUTPUT
with result sets (("DayOfWeek" int null, "Amount" float null))

print 'Output parameters (after):'
print FORMATMESSAGE('ParamINT=%d', @ParamINT)
print FORMATMESSAGE('ParamCharN=%s', @ParamCharN)
GO
```

> [!TIP]
> Los parámetros para este procedimiento almacenado se describen con más detalle en este tutorial rápido: [código de uso de R en T-SQL](rtsql-using-r-code-in-transact-sql-quickstart.md).

## <a name="step-3-view-the-results"></a>Paso 3. Ver los resultados

El procedimiento almacenado obtiene los datos originales, se aplica la secuencia de comandos de Python y, a continuación, devuelve los datos modificados en el **resultados** panel de Management Studio u otra herramienta de consulta SQL.


|DayOfWeek (antes)| Amount|DayOfWeek (después) |
|-----|-----|-----|
|Domingo|10|7|
|Lunes|11.1|1|
|Martes|12.2|2|
|Miércoles|13.3|3|
|Jueves|14.4|4|
|Viernes|15.5|5|
|Sábado|16.6|6|
|Viernes|17.7|5|
|Lunes|18.8|1|
|Domingo|19.9|7|

Mensajes de estado o errores que se devuelven a la consola de Python se devuelven como mensajes en la **consulta** ventana. Este es un extracto de la salida es posible que vea:

*Resultados del ejemplo*

```
Output parameters (before):
ParamINT=1234567
ParamCharN=INPUT 
Dataset (before):

(10 rows affected)

Dataset (after):
STDOUT message(s) from external script: 
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\revoscalepy

3.5.2 |Anaconda 4.2.0 (64-bit)| (default, Jul  5 2016, 11:41:13) [MSC v.1900 64 bit (AMD64)]
Hello World
C:\PROGRA~1\MICROS~2\MSSQL1~1.MSS\MSSQL\EXTENS~1\MSSQLSERVER01\7A70B3FB-FBA2-4C52-96D6-8634DB843229

3.5.2 |Anaconda 4.2.0 (64-bit)| (default, Jul  5 2016, 11:41:13) [MSC v.1900 64 bit (AMD64)]
Hello World
C:\PROGRA~1\MICROS~2\MSSQL1~1.MSS\MSSQL\EXTENS~1\MSSQLSERVER01\7A70B3FB-FBA2-4C52-96D6-8634DB843229

(10 rows affected)
Output parameters (after):
ParamINT=2
ParamCharN=OUTPUT
```

+ El **mensaje** salida incluye el directorio de trabajo que se utiliza para la ejecución de secuencias de comandos. En este ejemplo, MSSQLSERVER01 hace referencia a la cuenta del trabajador asignada por SQL Server para administrar el trabajo. 

    El GUID es el nombre de una carpeta temporal que se crea durante la ejecución del script para almacenar los artefactos de datos y la secuencia de comandos. Estas carpetas temporales están protegidas por SQL Server y se limpian mediante el objeto de trabajo de Windows una vez ha finalizado la secuencia de comandos.

+ La sección que contiene el mensaje "Hello World" imprime dos veces. Esto sucede porque el valor de  *@RowsPerRead*  ha sido establecida en 5 y hay 10 filas en la tabla; por lo tanto, son necesarias dos llamadas a Python para procesar todas las filas de la tabla.

    En las ejecuciones de producción, se recomienda que experimente con valores diferentes para determinar el número máximo de filas que se deben pasar en cada lote. El número óptimo de filas es dependiente de los datos y se ve afectado por el número de columnas del conjunto de datos y el tipo de datos que está pasando.

## <a name="resources"></a>Recursos

Vea estos ejemplos adicionales de Python y tutoriales para obtener sugerencias avanzadas y demostraciones to-end.

+ [Usar revoscalepy de Python para crear un modelo](use-python-revoscalepy-to-create-model.md)
+ [En bases de datos de Python para desarrolladores de SQL](sqldev-in-database-python-for-sql-developers.md)
+ [Crear un modelo de predicción mediante Python y SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)

## <a name="troubleshooting"></a>Solucionar problemas

Si no se puede encontrar el procedimiento almacenado, `sp_execute_external_script`, significa que probablemente no ha terminado de configurar la instancia para admitir la ejecución de scripts externos. Después de ejecutar el programa de instalación de SQL Server 2017 y seleccionar Python como el lenguaje de aprendizaje automático, debe habilitar explícitamente la característica mediante `sp_configure`y, a continuación, reinicie la instancia. Para obtener más información, consulte [programa de instalación de servicios de aprendizaje de máquina con Python](../python/setup-python-machine-learning-services.md).