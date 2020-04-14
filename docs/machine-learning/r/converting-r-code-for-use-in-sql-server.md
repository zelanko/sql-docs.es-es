---
title: Conversión de código de R para SQL Server
description: Migre el código de R a un procedimiento almacenado de SQL Server para la implementación de la solución y el acceso a datos relacionales en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 97bb0a54181f88703363bfbe598af26ede58ebf8
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/04/2020
ms.locfileid: "81117718"
---
# <a name="convert-r-code-for-execution-in-sql-server-in-database-instances"></a>Conversión de código de R para ejecutarlo en instancias de SQL Server (en la base de datos)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En este artículo se explica de manera general cómo modificar el código de R para que funcione en SQL Server. 

Al trasladar código de R desde R Studio u otro entorno a SQL Server, la mayoría de las veces el código funciona sin que sea necesario modificarlo: por ejemplo, si el código es simple, como una función que toma algunas entradas y devuelve un valor. También es más fácil portar soluciones que usen los paquetes **RevoScaleR** o **MicrosoftML**, que admiten la ejecución en distintos contextos de ejecución con el mínimo de cambios.

Aún así, es posible que tenga que realizar cambios importantes en el código si se da cualquiera de estas condiciones:

+ Se usan bibliotecas de R que tienen acceso a la red o que no se pueden instalar en SQL Server.
+ El código realiza llamadas independientes a orígenes de datos fuera de SQL Server, como hojas de cálculo de Excel, archivos en recursos compartidos y otras bases de datos. 
+ Quiere ejecutar el código en el parámetro *\@script* de [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) y también parametrizar el procedimiento almacenado.
+ La solución original incluye varios pasos que podrían ser más eficaces en un entorno de producción si se ejecutan de forma independiente, como la preparación de datos o la ingeniería de características, frente al entrenamiento del modelo, la puntuación o la creación de informes.
+ Puede mejorar el rendimiento si cambia las bibliotecas, usa la ejecución en paralelo o descarga algún procesamiento para SQL Server. 

## <a name="step-1-plan-requirements-and-resources"></a>Paso 1. Planear requisitos y recursos

**Paquetes**

+ Determine qué paquetes se necesitan y asegúrese de que funcionan en SQL Server.
 
+ Instale los paquetes con antelación en la biblioteca de paquetes predeterminada que usa Machine Learning Services. No se admiten las bibliotecas de usuarios.

**Orígenes de datos** 

+ Si tiene previsto insertar el código R en [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), identifique los orígenes de datos principales y secundarios. 

    + Los orígenes de datos **principales** son grandes conjuntos de datos, como los datos de entrenamiento del modelo o los datos de entrada para las predicciones. Planee la asignación del conjunto de datos más grande al parámetro de entrada de [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

    + Los orígenes de datos **secundarios** suelen ser conjuntos de datos más pequeños, como listas de factores o variables de agrupación adicionales. 
    
    Actualmente, sp_execute_external_script solo admite un único conjunto de datos como entrada para el procedimiento almacenado, pero puede agregar varias entradas escalares o binarias.

    Las llamadas al procedimiento almacenado precedidas por EXECUTE no se pueden usar como entrada para [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Puede usar consultas, vistas o cualquier otra instrucción SELECT válida.

+ Determine las salidas que necesita. Si ejecuta código de R mediante sp_execute_external_script, el procedimiento almacenado puede generar una sola trama de datos como resultado. Pero también puede generar varias salidas escalares, como trazados y modelos en formato binario, así como otros valores escalares derivados del código R o de los parámetros SQL.

**Tipos de datos**

+ Haga una lista de comprobación de posibles problemas de tipos de datos.

    SQL Server Machine Learning Services admite todos los tipos de datos de R. En cambio, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite mayor variedad de tipos de datos que R. Por eso se realizan algunas conversiones de tipos de datos implícitas al enviar datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a R y viceversa. También podría necesitar convertir explícitamente algunos datos. 

    Se admiten valores NULL. Aún así, R usa la construcción de datos de `na` para representar los valores que faltan, que son similares a los valores NULL.

+ Considere la posibilidad de eliminar la dependencia de los datos que R no puede usar; por ejemplo, R no puede usar los tipos de datos rowid y GUID de SQL Server y se producen errores.

    Para más información, vea [Bibliotecas de R y tipos de datos](../r/r-libraries-and-data-types.md).

## <a name="step-2-convert-or-repackage-code"></a>Paso 2. Convertir o volver a empaquetar código

La cantidad de código que cambie dependerá de si quiere enviar el código de R desde un cliente remoto para que se ejecute en el contexto de proceso de SQL Server, o si pretende implementar el código como parte de un procedimiento almacenado, lo que puede proporcionar un mejor rendimiento y seguridad de los datos. Ajustar el código en un procedimiento almacenado impone algunos requisitos adicionales. 

+ Defina los datos de entrada principales como una consulta de SQL siempre que sea posible, para evitar el movimiento de datos.

+ Al ejecutar R en un procedimiento almacenado, puede acceder directamente a varias entradas **escalares**. En el caso de parámetros que quiera usar en la salida, agregue la palabra clave **OUTPUT**. 

    Por ejemplo, la siguiente entrada escalar `@model_name` contiene el nombre del modelo, que también se genera en su propia columna en los resultados:

    ```sql
    EXEC sp_execute_external_script @model_name="DefaultModel" OUTPUT, @language=N'R', @script=N'R code here'
    ``` 

+ Cualquier variable que se pase como parámetro del procedimiento almacenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) debe asignarse a las variables en el código de R. De forma predeterminada, las variables se asignan por nombre.

    Todas las columnas del conjunto de datos de entrada deben asignarse también a las variables del script de R.  Por ejemplo, supongamos que el script de R contiene una fórmula como esta:

    ```R
    formula <- ArrDelay ~ CRSDepTime + DayOfWeek + CRSDepHour:DayOfWeek
    ```
    
    Se produce un error si el conjunto de datos de entrada no contiene columnas con los nombres coincidentes ArrDelay, CRSDepTime, DayOfWeek, CRSDepHour y DayOfWeek.

+ En algunos casos, es necesario definir un esquema de salida con antelación para los resultados.

    Por ejemplo, para insertar los datos en una tabla, debe usar la cláusula **WITH RESULT SET** para especificar el esquema.

    También se necesita el esquema de salida si el script de R usa el argumento `@parallel=1`. El motivo es que SQL Server puede crear varios procesos para ejecutar la consulta en paralelo, con los resultados recopilados al final. Por tanto, el esquema de salida debe prepararse antes de que se puedan crear los procesos en paralelo.
    
    En otros casos, se puede omitir el esquema de resultados mediante la opción **WITH RESULT SETS UNDEFINED**. Esta instrucción devuelve el conjunto de datos a partir del script de R sin asignar nombres a las columnas ni especificar los tipos de datos de SQL.

+ Considere la opción de generar datos de seguimiento o de control de tiempo mediante T-SQL en lugar de R.

    Por ejemplo, para pasar la hora del sistema u otra información usada para la auditoría y el almacenamiento, puede agregar una llamada de T-SQL que se pasa a los resultados, en lugar de generar datos similares en el script de R. 

**Mejorar el rendimiento y la seguridad**

+ Evite escribir predicciones o resultados intermedios en un archivo. Es preferible escribir las predicciones en una tabla para evitar el movimiento de datos.

+ Ejecute todas las consultas con antelación y revise los planes de consulta de SQL Server para identificar las tareas que se pueden realizar en paralelo.

    Si la consulta de entrada se puede paralelizar, establezca `@parallel=1` como parte de los argumentos de [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). 

    Por lo general, el procesamiento en paralelo con este indicador es posible siempre que SQL Server pueda trabajar con tablas con particiones o distribuir una consulta entre varios procesos y agregar los resultados al final. Normalmente, el procesamiento en paralelo con este indicador no es posible si entrena modelos mediante algoritmos que requieren que se lean todos los datos o si necesita crear agregados.

+ Revise el código de R para determinar si hay pasos que se pueden realizar independientemente o de una manera más eficiente, mediante una llamada de procedimiento almacenado independiente. Por ejemplo, conseguirá un mejor rendimiento si realiza ingeniería de características o extracción de características por separado y guarda los valores en una tabla.

+ Busque la manera de usar T-SQL en lugar de código de R para computaciones basadas en conjuntos.

    Por ejemplo, esta solución de R muestra cómo las funciones de T-SQL definidas por el usuario y R pueden realizar la misma tarea de ingeniería de características: [Tutorial integral de ciencia de datos](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md).

+ Si es posible, reemplace las funciones de R convencionales por funciones de **ScaleR** que admitan la ejecución distribuida. Para más información, vea [Comparación de funciones de Base R y Scale R](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler-compared-to-base-r).

+ Póngase en contacto con un desarrollador de bases de datos para averiguar cómo mejorar el rendimiento mediante el uso de características de SQL Server, como [memory-optimized tables](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables) o [Resource Governor](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor) (si tiene Enterprise Edition).

    Para más información, vea [Sugerencias y trucos de optimización de SQL Services para servicios de análisis](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services).

### <a name="step-3-prepare-for-deployment"></a>Paso 3. Preparar la implementación

+ Notifique al administrador para que los paquetes se puedan instalar y probar antes de implementar el código. 

    En un entorno de desarrollo, podría ser conveniente instalar paquetes como parte del código, pero esto es una práctica incorrecta en un entorno de producción. 

    No se admiten las bibliotecas de usuario, independientemente de si está usando un procedimiento almacenado o si ejecuta código de R en el contexto de proceso de SQL Server.

**Empaquetar el código de R en un procedimiento almacenado**

+ Si el código es relativamente sencillo, puede insertarlo en una función definida por el usuario de T-SQL sin modificarlo, como se describe en estos ejemplos:

    + [Ingeniería de características mediante T-SQL y R](../tutorials/sqldev-create-data-features-using-t-sql.md)

+ Si el código es más complejo, use el paquete de R **sqlrutils** para convertir el código. Este paquete está diseñado para ayudar a los usuarios de R con experiencia a escribir código de procedimiento almacenado que sea adecuado. 

    El primer paso consiste en volver a escribir el código de R como una sola función con entradas y salidas claramente definidas.

    Después, use el paquete **sqlrutils** para generar la entrada y las salidas en el formato correcto. El paquete **sqlrutils** genera automáticamente el código del procedimiento almacenado completo y también puede registrar el procedimiento almacenado en la base de datos. 

    Para más información y ejemplos, vea [sqlrutils (SQL)](ref-r-sqlrutils.md).

**Integración con otros flujos de trabajo**

+ Aproveche las herramientas de T-SQL y los procesos de ETL. Realice ingeniería de características, extracción de características y limpieza de datos con antelación como parte de los flujos de trabajo de datos.

    Cuando se trabaja en un entorno de desarrollo de R dedicado, como [!INCLUDE[rsql_rtvs_md](../../includes/rsql-rtvs-md.md)] o RStudio, se pueden extraer datos en el equipo, analizar los datos de forma iterativa y, luego, escribir o mostrar los resultados. 
    
    En cambio, cuando se migra código de R independiente a SQL Server, gran parte de este proceso se puede simplificar o delegar a otras herramientas de SQL Server. 

+ Use estrategias de visualización asincrónicas que sean seguras.

    Los usuarios de SQL Server a menudo no pueden acceder a los archivos del servidor y las herramientas de cliente de SQL normalmente no admiten el dispositivo de gráficos de R. Si genera trazados u otros gráficos como parte de la solución, considere la opción de exportar los trazados como datos binarios y guardarlos en una tabla o escribirlos.

+ Ajuste las funciones de predicción y puntuación en procedimientos almacenados para el acceso directo a las aplicaciones.

### <a name="other-resources"></a>Otros recursos

Aquí puede ver ejemplos de cómo se puede implementar una solución de R en SQL Server:

+ [Creación de un modelo predictivo para el negocio de alquiler de esquís mediante R y SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/)

+ [Análisis en base de datos para el desarrollador de SQL](../tutorials/sqldev-in-database-r-for-sql-developers.md) Muestra cómo ajustar el código de R en procedimientos almacenados para que sea más modular.

+ [Solución de ciencia de datos de un extremo a otro](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) Incluye una comparación de la ingeniería de características en R y T-SQL.
