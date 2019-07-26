---
title: Guía de inicio rápido para la ejecución de código básico de R "Hola mundo" en T-SQL
description: Inicio rápido de script de R en SQL Server. Conozca los aspectos básicos de la llamada al script de R mediante el procedimiento almacenado del sistema sp_execute_external_script en un ejercicio de Hola a todos.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: ab73e0231f462504652e0e1af62fed80c706f061
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469038"
---
# <a name="quickstart-hello-world-r-script-in-sql-server"></a>Inicio rápido: Script R "Hello World" en SQL Server 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En esta guía de inicio rápido, aprenderá conceptos clave mediante la ejecución de un script R "Hola mundo" de R inT-SQL, con una introducción al procedimiento almacenado del sistema **sp_execute_external_script** . 

## <a name="prerequisites"></a>Requisitos previos

En una guía de inicio rápido anterior, [Verify r existe en SQL Server](quickstart-r-verify.md), se proporciona información y vínculos para configurar el entorno de r necesario para esta guía de inicio rápido.

## <a name="basic-r-interaction"></a>Interacción básica de R

Hay dos maneras de ejecutar código R en SQL Database:

+ Agregue el script de R como argumento del procedimiento almacenado del sistema, [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql).
+ Desde un [cliente remoto de R](https://docs.microsoft.com/sql/advanced-analytics/r/set-up-a-data-science-client), conéctese a la base de datos SQL y ejecute el código mediante el SQL Database como el contexto de cálculo.

El siguiente ejercicio se centra en el primer modelo de interacción: Cómo pasar código R a un procedimiento almacenado.

1. Ejecute un script simple para ver cómo se ejecuta un script de R en la base de datos SQL.

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

2. Suponiendo que todo está configurado correctamente, se calcula el resultado correcto y la función R `print` devuelve el resultado a la ventana **mensajes** .

    **Resultado**

    ```text
    STDOUT message(s) from external script: 
    0.5 2
    ```

    Aunque la obtención de mensajes **stdout** es útil cuando se prueba el código, a menudo es necesario devolver los resultados en formato tabular, de modo que pueda usarlos en una aplicación o escribirlos en una tabla. Consulte [Quickstart: Controle las entradas y salidas mediante R](rtsql-working-with-inputs-and-outputs.md) en SQL Server para obtener más información.

Recuerde que todo lo que `@script` se encuentra dentro del argumento debe ser un código de R válido.

## <a name="run-a-hello-world-script"></a>Ejecutar un script de Hola mundo

En el ejercicio siguiente se ejecutan otros sencillos scripts de R.

```sql
EXEC sp_execute_external_script
  @language =N'R',
  @script=N'OutputDataSet<-InputDataSet',
  @input_data_1 =N'SELECT 1 AS hello'
  WITH RESULT SETS (([Hello World] int));
GO
```

Entre las entradas de este procedimiento almacenado se incluyen:

+ *@language* define la extensión del lenguaje para llamar, en este caso, R.
+ *@script* define los comandos que se pasan al tiempo de ejecución de R. El script de R debe estar todo incluido en este argumento en texto Unicode. También puede agregar texto a una variable de tipo **nvarchar** y, después, llamar a la variable.
+ *@input_data_1* son los datos devueltos por la consulta, que se pasan al tiempo de ejecución de R, que devuelve los datos que se van a SQL Server como una trama de datos.
+ La cláusula WITH RESULT SETS define el esquema de la tabla de datos devuelta para SQL Server, agregando "Hola mundo" como nombre de columna, **int** para el tipo de datos.

**Resultado**

| Hola mundo |
|-------------|
| 1 |

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha ejecutado un par de scripts sencillos de R, eche un vistazo más de cerca a las entradas y salidas de estructura.

> [!div class="nextstepaction"]
> [Inicio rápido: Controlar entradas y salidas](quickstart-r-inputs-and-outputs.md)
