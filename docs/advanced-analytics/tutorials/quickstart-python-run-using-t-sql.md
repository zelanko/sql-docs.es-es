---
title: Guía de inicio rápido para una ejecución de código de Python básica "Hola mundo" en T-SQL
description: Inicio rápido de script de Python en SQL Server. Conozca los aspectos básicos de la llamada al script de Python mediante el procedimiento almacenado del sistema sp_execute_external_script en un ejercicio de Hola a todos.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/10/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a170bd2ee3e893a83ebb9d3201ee117321e7562b
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714821"
---
# <a name="quickstart-hello-world-python-script-in-sql-server"></a>Inicio rápido: Script de Python "Hello World" en SQL Server 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En esta guía de inicio rápido, aprenderá conceptos clave mediante la ejecución de un script de Python "Hola mundo" inT-SQL, con una introducción al procedimiento almacenado del sistema **sp_execute_external_script** . 

## <a name="prerequisites"></a>Requisitos previos

En una guía de inicio rápido anterior, [Compruebe que Python existe en SQL Server](quickstart-python-verify.md), proporciona información y vínculos para configurar el entorno de Python necesario para esta guía de inicio rápido.

## <a name="basic-python-interaction"></a>Interacción básica de Python

Hay dos maneras de ejecutar el código de Python en SQL Server:

+ Agregue un script de Python como argumento del procedimiento almacenado del sistema, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

+ Desde un [cliente remoto de Python](../python/setup-python-client-tools-sql.md), conéctese a SQL Server y ejecute el código utilizando el SQL Server como el contexto de cálculo. Esto requiere [revoscalepy](../python/ref-py-revoscalepy.md).

El siguiente ejercicio se centra en el primer modelo de interacción: Cómo pasar código Python a un procedimiento almacenado.

1. Ejecute código simple para ver cómo se pasan los datos entre SQL Server y Python.

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

2. Suponiendo que todo está configurado correctamente y que Python y SQL Server están hablando entre sí, se calcula el resultado correcto y la función de Python `print` devuelve el resultado a las ventanas **mensajes** .

    **Resultado**

    ```text
    STDOUT message(s) from external script: 
    0.5 2
    ```

    Aunque la obtención de mensajes **stdout** es útil cuando se prueba el código, a menudo es necesario devolver los resultados en formato tabular, de modo que pueda usarlos en una aplicación o escribirlos en una tabla.

Por ahora, recuerde estas reglas:

+ Todo lo que `@script` se encuentra dentro del argumento debe ser un código Python válido. 
+ El código debe seguir todas las reglas de Python relacionadas con la sangría, los nombres de variables, etc. Cuando reciba un error, compruebe el espacio en blanco y el uso de mayúsculas y minúsculas.
+ Entre los lenguajes de programación, Python es uno de los más flexibles con respecto a las comillas simples frente a comillas dobles; son bastante intercambiables. Sin embargo, T-SQL usa comillas simples solo para determinadas cosas, `@script` y el argumento usa comillas simples para incluir el código de Python como una cadena Unicode. Por lo tanto, es posible que necesite revisar el código de Python y cambiar algunas comillas simples por comillas dobles.
+ Si usa bibliotecas que no se cargan de forma predeterminada, debe usar una instrucción de importación al principio del script para cargarlas. SQL Server agrega varias bibliotecas específicas del producto. Para obtener más información, consulte [bibliotecas de Python](../python/python-libraries-and-data-types.md).
+ Si la biblioteca aún no está instalada, detenga e instale el paquete de Python fuera de SQL Server, como se describe aquí: [Instalación de paquetes de Python adicionales en SQL Server](../python/install-additional-python-packages-on-sql-server.md)

## <a name="run-a-hello-world-script"></a>Ejecutar un script de Hola mundo

En el ejercicio siguiente se ejecutan otros scripts de Python sencillos.

```sql
EXEC sp_execute_external_script
@language =N'Python',
@script=N'OutputDataSet = InputDataSet',
@input_data_1 =N'SELECT 1 AS hello'
WITH RESULT SETS (([Hello World] int));
GO
```

Entre las entradas de este procedimiento almacenado se incluyen:

+ *@language* define la extensión del lenguaje para llamar, en este caso, Python.
+ *@script* define los comandos que se pasan al tiempo de ejecución de Python. Todo el script de Python debe incluirse en este argumento, como texto Unicode. También puede agregar texto a una variable de tipo **nvarchar** y, después, llamar a la variable.
+ *@input_data_1* son los datos devueltos por la consulta, que se pasan al tiempo de ejecución de Python, que devuelve los datos que se van a SQL Server como una trama de datos.
+ La cláusula WITH RESULT SETS define el esquema de la tabla de datos devuelta para SQL Server, agregando "Hola mundo" como nombre de columna, **int** para el tipo de datos.

**Resultado**

| Hola mundo |
|-------------|
| 1 |

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha ejecutado un par de scripts de Python sencillos, eche un vistazo más de cerca a las entradas y salidas de estructura.

> [!div class="nextstepaction"]
> [Inicio rápido: Controlar entradas y salidas](quickstart-python-inputs-and-outputs.md)
