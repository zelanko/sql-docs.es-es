---
title: 'Guía de inicio rápido para una ejecución de código de "Hello World" básica R en T-SQL: SQL Server Machine Learning'
description: Guía de inicio rápido para script de R en SQL Server. Obtenga información sobre los conceptos básicos de llamar al script de R mediante el procedimiento almacenado del sistema sp_execute_external_script en un ejercicio de hello world.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 1c3ee703bca46bf46dba8225e1d28da3174dc932
ms.sourcegitcommit: aa4f594ec6d3e85d0a1da6e69fa0c2070d42e1d8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59240173"
---
# <a name="quickstart-hello-world-r-script-in-sql-server"></a>Inicio rápido: Script de R "Hello world" en SQL Server 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este tutorial, obtendrá información sobre los conceptos clave mediante la ejecución de un "Hello World" R script SQL de inT, una introducción a la **sp_execute_external_script** procedimiento almacenado del sistema. 

## <a name="prerequisites"></a>Requisitos previos

Un tutorial anterior, [R Compruebe que existe en SQL Server](quickstart-r-verify.md), proporciona información y vínculos para configurar el entorno de R necesario para este inicio rápido.

## <a name="basic-r-interaction"></a>Interacción básica de R

Hay dos maneras puede ejecutar código R en SQL Database:

+ Agregar script de R como un argumento de procedimiento almacenado del sistema, [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql).
+ Desde un [clientes remotos de R](https://docs.microsoft.com/sql/advanced-analytics/r/set-up-a-data-science-client), conectarse a la base de datos SQL y ejecutar código con la base de datos SQL como el contexto de cálculo.

El siguiente ejercicio se centra en el primer modelo de interacción: cómo pasar código de R a un procedimiento almacenado.

1. Ejecutar un script sencillo para ver cómo se ejecuta un script de R en SQL database.

    ```sql
    EXECUTE sp_execute_external_script
    @language = N'R',
    @script = N'
    a <- 1
    b <- 2
    c <- a/b
    d <- a*b
    print(c(c, d))
    '
    ```

2. Se calcula suponiendo que tiene todo está configurado correctamente el resultado correcto y el R `print` función devuelve el resultado a la **mensajes** ventana.

    **Resultado**

    ```text
    STDOUT message(s) from external script: 
    0.5 2
    ```

    Al obtener **stdout** mensajes es útil al probar el código, más a menudo es necesario devolver los resultados en formato tabular, para que pueda usarlo en una aplicación o escribirlo en una tabla. Consulte [inicio rápido: Identificador de entradas y salidas con R en SQL Server](rtsql-working-with-inputs-and-outputs.md) para obtener más información.

Recuerde, todo dentro de la `@script` el argumento debe ser código R válido.

## <a name="run-a-hello-world-script"></a>Ejecutar un script Hello World

El siguiente ejercicio ejecuta otra scripts de R.

```sql
EXEC sp_execute_external_script
  @language =N'R',
  @script=N'OutputDataSet<-InputDataSet',
  @input_data_1 =N'SELECT 1 AS hello'
  WITH RESULT SETS (([Hello World] int));
GO
```

Entradas de este procedimiento almacenado se incluyen:

+ *@language* parámetro define la extensión del lenguaje para llamar, en este caso, R.
+ *@script* parámetro define los comandos que se pasan al runtime de R. El script de R debe estar todo incluido en este argumento en texto Unicode. También puede agregar texto a una variable de tipo **nvarchar** y, después, llamar a la variable.
+ *@input_data_1* se devuelven datos por la consulta, que se pasa al runtime de R, que devuelve los datos a SQL Server como una trama de datos.
+ CON conjuntos de resultados cláusula define el esquema de la tabla de datos devueltos para SQL Server, agregar "Hello World" como nombre de columna, **int** para el tipo de datos.

**Resultado**

| Hello World |
|-------------|
| 1 |

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha ejecutado un par de scripts de R, eche un vistazo más de cerca en estructurar las entradas y salidas.

> [!div class="nextstepaction"]
> [Inicio rápido: Control de entradas y salidas](quickstart-r-inputs-and-outputs.md)
