---
title: Convertir código de R para procedimientos almacenados
description: Migre el código R a un SQL Server procedimiento almacenado para la implementación de la solución y el acceso a datos relacionales en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 713c5cc8de5daecec77ff984a22f85b220ece2a2
ms.sourcegitcommit: c426c7ef99ffaa9e91a93ef653cd6bf3bfd42132
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/10/2019
ms.locfileid: "72251345"
---
# <a name="convert-r-code-for-execution-in-sql-server-in-database-instances"></a>Conversión del código R para su ejecución en instancias de SQL Server (en la base de datos)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En este artículo se proporcionan instrucciones de alto nivel sobre cómo modificar el código de R para que funcione en SQL Server. 

Al trasladar código R desde R Studio u otro entorno a SQL Server, la mayoría de las veces el código funciona sin modificaciones adicionales: por ejemplo, si el código es simple, como una función que toma algunas entradas y devuelve un valor. También es más fácil trasladar las soluciones que usan los paquetes **RevoScaleR** o **MicrosoftML** , que admiten la ejecución en distintos contextos de ejecución con cambios mínimos.

Sin embargo, el código podría requerir cambios sustanciales si se aplica alguna de las siguientes condiciones:

+ Use bibliotecas de R que tengan acceso a la red o que no se puedan instalar en SQL Server.
+ El código realiza llamadas independientes a orígenes de datos fuera de SQL Server, como hojas de cálculo de Excel, archivos de recursos compartidos y otras bases de datos. 
+ Desea ejecutar el código en el parámetro *\@script* de [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) y parametrizar también el procedimiento almacenado.
+ La solución original incluye varios pasos que pueden ser más eficaces en un entorno de producción si se ejecutan de forma independiente, como la preparación de datos o la ingeniería de características, y el entrenamiento del modelo, la puntuación o los informes.
+ Para mejorar el rendimiento, puede cambiar las bibliotecas, usar la ejecución en paralelo o descargar algún procesamiento para SQL Server. 

## <a name="step-1-plan-requirements-and-resources"></a>Paso 1. Planear requisitos y recursos

**Paquetes**

+ Determine qué paquetes son necesarios y asegúrese de que funcionan en SQL Server.
 
+ Instale los paquetes de antemano, en la biblioteca de paquetes predeterminada usada por Machine Learning Services. No se admiten las bibliotecas de usuario.

**Orígenes de datos** 

+ Si piensa insertar el código R en [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), identifique los orígenes de datos principal y secundario. 

    + Los orígenes de datos **principales** son conjuntos de datos grandes, como datos de entrenamiento del modelo o datos de entrada para predicciones. Planear la asignación del conjunto de datos más grande al parámetro de entrada de [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

    + Los orígenes de datos **secundarios** suelen ser conjuntos de datos más pequeños, como listas de factores o variables de agrupación adicionales. 
    
    Actualmente, sp_execute_external_script solo admite un único conjunto de datos como entrada para el procedimiento almacenado. Sin embargo, puede agregar varias entradas escalares o binarias.

    Las llamadas a procedimientos almacenados precedidas por EXECUTe no se pueden usar como entrada para [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Puede usar consultas, vistas o cualquier otra instrucción SELECT válida.

+ Determine las salidas que necesita. Si ejecuta código R con sp_execute_external_script, el procedimiento almacenado puede generar una sola trama de datos como resultado. Sin embargo, también puede generar varias salidas escalares, como trazados y modelos en formato binario, así como otros valores escalares derivados del código R o de los parámetros SQL.

**Tipos de datos**

+ Haga una lista de comprobación de posibles problemas de tipos de datos.

    SQL Server Machine Learning Services admiten todos los tipos de datos de R. Sin embargo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite una mayor variedad de tipos de datos que R. Por lo tanto, se realizan algunas conversiones implícitas de tipos de datos al enviar datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a R y viceversa. Es posible que tenga que convertir explícitamente algunos datos. 

    Se admiten valores NULL. Sin embargo, R utiliza la construcción de datos `na` para representar un valor que falta, que es similar a un valor null.

+ Considere la posibilidad de eliminar la dependencia de los datos que R no puede usar; por ejemplo, los tipos de datos ROWID y GUID de SQL Server no pueden ser consumidos por R y generar errores.

    Para obtener más información, consulte [bibliotecas y tipos de datos de R](../r/r-libraries-and-data-types.md).

## <a name="step-2-convert-or-repackage-code"></a>Paso 2. Convertir o volver a empaquetar código

El modo en que cambie el código dependerá de si desea enviar el código de R desde un cliente remoto para que se ejecute en el contexto de proceso de SQL Server, o si pretende implementar el código como parte de un procedimiento almacenado, lo que puede proporcionar un mejor rendimiento y seguridad de los datos. El ajuste del código en un procedimiento almacenado impone algunos requisitos adicionales. 

+ Defina los datos de entrada principales como una consulta SQL siempre que sea posible, para evitar el movimiento de datos.

+ Al ejecutar R en un procedimiento almacenado, puede pasar por varias entradas **escalares** . Para los parámetros que desee usar en la salida, agregue la palabra clave **Output** . 

    Por ejemplo, la entrada escalar siguiente `@model_name` contiene el nombre del modelo, que también se genera en su propia columna en los resultados:

    ```sql
    EXEC sp_execute_external_script @model_name="DefaultModel" OUTPUT, @language=N'R', @script=N'R code here'
    ``` 

+ Cualquier variable que se pase como parámetros del procedimiento almacenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) debe estar asignada a variables en el código de R. De forma predeterminada, las variables se asignan por nombre.

    Todas las columnas del conjunto de datos de entrada también se deben asignar a las variables del script de R.  Por ejemplo, supongamos que el script de R contiene una fórmula como esta:

    ```R
    formula <- ArrDelay ~ CRSDepTime + DayOfWeek + CRSDepHour:DayOfWeek
    ```
    
    Se produce un error si el conjunto de datos de entrada no contiene columnas con los nombres coincidentes ArrDelay, CRSDepTime, DayOfWeek, CRSDepHour y DayOfWeek.

+ En algunos casos, un esquema de salida debe definirse de antemano para los resultados.

    Por ejemplo, para insertar los datos en una tabla, debe usar la cláusula **with Result Set** para especificar el esquema.

    También se requiere el esquema de salida si el script de R usa el argumento `@parallel=1`. El motivo es que SQL Server puede crear varios procesos para ejecutar la consulta en paralelo, con los resultados recopilados al final. Por lo tanto, el esquema de salida debe estar preparado antes de que se puedan crear los procesos paralelos.
    
    En otros casos, puede omitir el esquema de resultados mediante la opción **con conjuntos de resultados sin definir**. Esta instrucción devuelve el DataSet desde el script de R sin asignar un nombre a las columnas ni especificar los tipos de datos de SQL.

+ Considere la posibilidad de generar datos de seguimiento o de control de tiempo mediante T-SQL en lugar de R.

    Por ejemplo, puede pasar la hora del sistema u otra información usada para la auditoría y el almacenamiento agregando una llamada de T-SQL que se pasa a los resultados, en lugar de generar datos similares en el script de R. 

**Mejorar el rendimiento y la seguridad**

+ Evite escribir predicciones o resultados intermedios en un archivo. En su lugar, escriba predicciones en una tabla para evitar el movimiento de datos.

+ Ejecute todas las consultas de antemano y revise los planes de consulta de SQL Server para identificar las tareas que se pueden realizar en paralelo.

    Si la consulta de entrada puede ejecutarse en paralelo, establezca `@parallel=1` como parte de los argumentos en [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). 

    Por lo general, el procesamiento en paralelo con este indicador es posible siempre que SQL Server pueda trabajar con tablas con particiones o distribuir una consulta entre varios procesos y agregar los resultados al final. Normalmente, el procesamiento en paralelo con este indicador no es posible si entrena modelos mediante algoritmos que requieren que se lean todos los datos o si necesita crear agregados.

+ Revise el código de R para determinar si hay pasos que se pueden realizar independientemente o de una manera más eficiente, mediante una llamada de procedimiento almacenado independiente. Por ejemplo, puede obtener un mejor rendimiento si realiza ingeniería de características o extracción de características por separado y guarda los valores en una tabla.

+ Busque formas de usar T-SQL en lugar de código R para los cálculos basados en conjuntos.

    Por ejemplo, esta solución de R muestra cómo las funciones T-SQL definidas por el usuario y R pueden realizar la misma tarea de ingeniería de características: [Tutorial integral de ciencia de datos](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md).

+ Si es posible, reemplace las funciones de R convencionales por las funciones de **ScaleR** que admiten la ejecución distribuida. Para obtener más información, consulte [comparación de las funciones base r y escala r](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler-compared-to-base-r).

+ Póngase en contacto con un desarrollador de bases de datos para determinar las maneras de mejorar el rendimiento mediante el uso de SQL Server características como [las tablas optimizadas para memoria](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables), o bien, si tiene la edición Enterprise [Resource Governor](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor)).

    Para obtener más información, consulte [SQL Server sugerencias y trucos para la optimización de los servicios de análisis](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services) .

### <a name="step-3-prepare-for-deployment"></a>Paso 3. Preparación para la implementación

+ Notifique al administrador para que los paquetes se puedan instalar y probar antes de implementar el código. 

    En un entorno de desarrollo, podría ser adecuado instalar paquetes como parte del código, pero esto es una práctica incorrecta en un entorno de producción. 

    No se admiten las bibliotecas de usuario, independientemente de si está usando un procedimiento almacenado o ejecuta código R en el contexto de proceso de SQL Server.

**Empaquetar el código de R en un procedimiento almacenado**

+ Si el código es relativamente sencillo, puede incrustarlo en una función definida por el usuario de T-SQL sin modificaciones, como se describe en estos ejemplos:

    + [Crear una función de R que se ejecute en rxExec](../tutorials/deepdive-create-a-simple-simulation.md)
    + [Ingeniería de características con T-SQL y R](../tutorials/sqldev-create-data-features-using-t-sql.md)

+ Si el código es más complejo, use el paquete de R **sqlrutils** para convertir el código. Este paquete está diseñado para ayudar a los usuarios de R con experiencia a escribir código de procedimiento almacenado adecuado. 

    El primer paso consiste en volver a escribir el código de R como una sola función con entradas y salidas claramente definidas.

    A continuación, use el paquete **sqlrutils** para generar la entrada y las salidas en el formato correcto. El paquete **sqlrutils** genera automáticamente el código de procedimiento almacenado completo y también puede registrar el procedimiento almacenado en la base de datos. 

    Para obtener más información y ejemplos, vea [sqlrutils (SQL)](ref-r-sqlrutils.md).

**Integración con otros flujos de trabajo**

+ Aproveche las herramientas de T-SQL y los procesos ETL. Realice ingeniería de características, extracción de características y limpieza de datos de antemano como parte de los flujos de trabajo de datos.

    Cuando trabaje en un entorno de desarrollo de R dedicado como [!INCLUDE[rsql_rtvs_md](../../includes/rsql-rtvs-md.md)] o RStudio, puede extraer datos en el equipo, analizar los datos de manera iterativa y, a continuación, escribir o mostrar los resultados. 
    
    Sin embargo, cuando se migra código R independiente a SQL Server, gran parte de este proceso se puede simplificar o delegar a otras herramientas de SQL Server. 

+ Use estrategias de visualización asincrónicas seguras.

    Los usuarios de SQL Server a menudo no pueden tener acceso a los archivos del servidor y las herramientas de cliente de SQL normalmente no admiten el dispositivo de gráficos de R. Si genera trazados u otros gráficos como parte de la solución, considere la posibilidad de exportar los trazados como datos binarios y guardarlos en una tabla o escribirlos.

+ Ajuste las funciones de predicción y puntuación en procedimientos almacenados para el acceso directo a las aplicaciones.

### <a name="other-resources"></a>Otros recursos

Para ver ejemplos de cómo se puede implementar una solución de R en SQL Server, consulte estos ejemplos:

+ [Cree un modelo predictivo para el negocio de alquiler de esquí mediante R y SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/)

+ [Análisis en base de datos para el desarrollador de SQL](../tutorials/sqldev-in-database-r-for-sql-developers.md) Muestra cómo puede hacer que el código de R sea más modular si lo ajusta en procedimientos almacenados.

+ [Solución de ciencia de datos de un extremo a otro](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) Incluye una comparación de la ingeniería de características en R y T-SQL
