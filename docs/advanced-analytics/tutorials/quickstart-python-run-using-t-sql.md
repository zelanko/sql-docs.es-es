---
title: 'Ejecución en T-SQL: SQL Server Machine Learning de código de inicio rápido para un Python básico "Hola mundo"'
description: Guía de inicio rápido para script de Python en SQL Server. Obtenga información sobre los conceptos básicos de llamar al script de Python con el procedimiento almacenado del sistema sp_execute_external_script en un ejercicio de hello world.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/10/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 6d8da3ce90e915344f2380d4cd5cc866db6715ef
ms.sourcegitcommit: 57f7e5f25161dbb4cc446e751ea74b1ac5f86165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/10/2019
ms.locfileid: "59476640"
---
# <a name="quickstart-hello-world-python-script-in-sql-server"></a>Inicio rápido: Script de Python "Hello world" en SQL Server 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este tutorial, obtendrá información sobre los conceptos clave mediante la ejecución de un "Hello World" de Python script SQL de inT, una introducción a la **sp_execute_external_script** procedimiento almacenado del sistema. 

## <a name="prerequisites"></a>Requisitos previos

Un tutorial anterior, [Python Compruebe que existe en SQL Server](quickstart-python-verify.md), proporciona información y vínculos para configurar el entorno de Python necesario para este inicio rápido.

## <a name="basic-python-interaction"></a>Interacción básica de Python

Hay dos maneras de ejecutar código de Python en SQL Server:

+ Agregar un script de Python como un argumento de procedimiento almacenado del sistema, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

+ Desde un [cliente Python remoto](../python/setup-python-client-tools-sql.md), conectarse a SQL Server y ejecutar código con el servidor SQL Server como contexto de proceso. Esto requiere [revoscalepy](../python/ref-py-revoscalepy.md).

El siguiente ejercicio se centra en el primer modelo de interacción: cómo pasar de código de Python a un procedimiento almacenado.

1. Ejecutar cierto código simple para ver cómo se pasan los datos y hacia atrás entre SQL Server y Python.

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    a = 1
    b = 2
    c = a/b
    d = a*b
    print(c, d)
    '
    ```

2. Suponiendo que tiene todo está configurado correctamente y Python y SQL Server se comunican entre sí, se calcula el resultado correcto y la versión de Python `print` función devuelve el resultado a la **mensajes** windows.

    **Resultado**

    ```text
    STDOUT message(s) from external script: 
    0.5 2
    ```

    Al obtener **stdout** mensajes es útil al probar el código, más a menudo es necesario devolver los resultados en formato tabular, para que pueda usarlo en una aplicación o escribirlo en una tabla.

Por ahora, recuerde estas reglas:

+ Todos los elementos de la `@script` el argumento debe ser código Python válido. 
+ El código debe seguir todas las reglas de Python con respecto a la sangría, los nombres de variable y así sucesivamente. Cuando se produce un error, compruebe el espacio en blanco y mayúsculas y minúsculas.
+ Los lenguajes de programación, Python es uno de los más flexible con respecto a las comillas simples y comillas dobles; son prácticamente intercambiables. Sin embargo, T-SQL usa comillas simples solo determinadas acciones y el `@script` argumento usa comillas simples para delimitar el código de Python como una cadena Unicode. Por lo tanto, deberá revisar el código de Python y cambie algunos comillas simples por comillas dobles.
+ Si usa las bibliotecas que no se cargan de forma predeterminada, debe usar una instrucción de importación al principio de la secuencia de comandos para cargarlas. SQL Server agrega varias bibliotecas específicas de cada producto. Para obtener más información, consulte [bibliotecas de Python](../python/python-libraries-and-data-types.md).
+ Si la biblioteca no está ya instalada, detenga e instale el paquete de Python fuera de SQL Server, como se describe aquí: [Instalación de paquetes de Python adicionales en SQL Server](../python/install-additional-python-packages-on-sql-server.md)

## <a name="run-a-hello-world-script"></a>Ejecutar un script Hello World

El siguiente ejercicio ejecuta otra sencillos scripts de Python.

```sql
EXEC sp_execute_external_script
@language =N'Python',
@script=N'OutputDataSet = InputDataSet',
@input_data_1 =N'SELECT 1 AS hello'
WITH RESULT SETS (([Hello World] int));
GO
```

Entradas de este procedimiento almacenado se incluyen:

+ *@language* parámetro define la extensión del lenguaje para llamar, en este caso, Python.
+ *@script* parámetro define los comandos que se pasan al tiempo de ejecución de Python. El script de Python completo debe incluirse en este argumento, como texto Unicode. También puede agregar texto a una variable de tipo **nvarchar** y, después, llamar a la variable.
+ *@input_data_1* se devuelven datos por la consulta, que se pasa al runtime de Python, que devuelve los datos a SQL Server como una trama de datos.
+ CON conjuntos de resultados cláusula define el esquema de la tabla de datos devueltos para SQL Server, agregar "Hello World" como nombre de columna, **int** para el tipo de datos.

**Resultado**

| Hello World |
|-------------|
| 1 |

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha ejecutado un par de scripts de Python sencillo, eche un vistazo más de cerca en estructurar las entradas y salidas.

> [!div class="nextstepaction"]
> [Inicio rápido: Control de entradas y salidas](quickstart-python-inputs-and-outputs.md)
