---
title: 'Convertir código de R para procedimientos almacenados: SQL Server Machine Learning Services'
description: Migrar código de R a un procedimiento almacenado de SQL Server para el acceso de implementación y datos de solución para datos relacionales en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: a3348058b03ff1441256cc8298ddc1b5b2216b0d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62642789"
---
# <a name="convert-r-code-for-execution-in-sql-server-in-database-instances"></a>Convertir código de R para su ejecución en instancias de SQL Server (In-Database)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo proporciona orientación de alto nivel sobre cómo modificar el código de R para que funcione en SQL Server. 

Al mover código de R desde R Studio u otro entorno a SQL Server, el código funciona con mayor frecuencia sin modificaciones adicionales: por ejemplo, si el código es sencillo, como una función que toma algunas entradas y devuelve un valor. También es más fácil las soluciones de puerto que utilizan el **RevoScaleR** o **MicrosoftML** paquetes, que admiten la ejecución en contextos de ejecución distintos con cambios mínimos.

Sin embargo, el código puede requerir cambios sustanciales si cualquiera de las condiciones siguientes:

+ Utilizar bibliotecas de R que tienen acceso a la red o que no se puede instalar en SQL Server.
+ El código hace llamadas independientes para los orígenes de datos fuera de SQL Server, como hojas de cálculo de Excel, archivos en recursos compartidos y otras bases de datos. 
+ Desea ejecutar el código de la *@script* parámetro de [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) y también parametrizar el procedimiento almacenado.
+ La solución original incluye varios pasos que pueden resultar más eficaces en un entorno de producción si se ejecuta de forma independiente, como la preparación de datos o ingeniería de características frente al modelo de entrenamiento, puntuación o informes.
+ Desea mejorar optimizar el rendimiento cambiando las bibliotecas, mediante la ejecución en paralelo o descarga algún procesamiento para SQL Server. 

## <a name="step-1-plan-requirements-and-resources"></a>Paso 1. Planear los requisitos y recursos

**Paquetes**

+ Determinar qué paquetes son necesarios y asegurarse de que funcionan en SQL Server.
 
+ Instalar paquetes de antemano, en la biblioteca de paquetes predeterminada usada por servicios Machine Learning. No se admiten las bibliotecas de usuario.

**Orígenes de datos** 

+ Si va a insertar el código de R en [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), identifique los orígenes de datos principal y secundaria. 

    + **Principal** orígenes de datos son grandes conjuntos de datos, como datos de entrenamiento del modelo o datos de entrada para las predicciones. Plan asignar el conjunto de datos más grande para el parámetro de entrada de [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

    + **Secundaria** orígenes de datos son normalmente más pequeños conjuntos de datos, como las listas de factores o variables adicionales de agrupación. 
    
    Actualmente, sp_execute_external_script admite un único conjunto de datos como entrada para el procedimiento almacenado. Sin embargo, puede agregar varias entradas escalares o binarias.

    Las llamadas de procedimiento almacenado precedidas por EXECUTE no se puede usar como entrada para [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Puede usar las consultas, vistas o cualquier otra instrucción SELECT válida.

+ Determinar los resultados que necesita. Si ejecuta código de R con sp_execute_external_script, el procedimiento almacenado puede generar como resultado una sola trama de datos. Sin embargo, también pueden generar varias salidas escalares, incluidos los gráficos y modelos en formato binario, así como otros valores escalares derivan el código de R o SQL parámetros.

**Tipos de datos**

+ Haga una lista de comprobación de posibles problemas de tipos de datos.

    Todos los tipos de datos de R son compatibles con SQL Server machine Learning Services. Sin embargo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite una gran variedad de tipos de datos de r. Por lo tanto, algunas conversiones de tipos de datos implícitas se realizan al enviar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos a R y viceversa. Es posible que deba convertir explícitamente o convertir algunos datos. 

    Se admiten valores NULL. Sin embargo, se usa R el `na` construcción de datos para representar un valor que falta, que es similar a un valor null.

+ Considere la eliminación de dependencia en los datos que no se puede usar por R: rowid por ejemplo, y los tipos de datos GUID de SQL Server no pueden usarse en R y generan errores.

    Para obtener más información, consulte [bibliotecas de R y tipos de datos](../r/r-libraries-and-data-types.md).

## <a name="step-2-convert-or-repackage-code"></a>Paso 2. Convertir o volver a empaquetar código

¿Cuánto cambia el código depende de si va a enviar el código de R desde un cliente remoto se ejecuten en el contexto de cálculo de SQL Server, o va a implementar el código como parte de un procedimiento almacenado, que puede proporcionar un mejor rendimiento y seguridad de los datos. Ajuste el código en un procedimiento almacenado impone algunos requisitos adicionales. 

+ Definir los datos de entrada principales como una consulta SQL siempre que sea posible, para evitar el movimiento de datos.

+ Cuando se ejecuta R en un procedimiento almacenado, puede pasar a través de varios **escalares** entradas. Para los parámetros que se va a usar en la salida, agregue el **salida** palabra clave. 

    Por ejemplo, la siguiente entrada escalar `@model_name` contiene el nombre del modelo, que también es la salida en su propia columna en los resultados:

    ```sql
    EXEC sp_execute_external_script @model_name="DefaultModel" OUTPUT, @language=N'R', @script=N'R code here'
    ``` 

+ Las variables que se pasen como parámetros del procedimiento almacenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) debe asignarse a las variables en el código de R. De forma predeterminada, las variables se asignan por nombre.

    Todas las columnas del conjunto de datos de entrada también deben asignarse a las variables del script de R.  Por ejemplo, suponga que el script de R contiene una fórmula como esta:

    ```R
    formula <- ArrDelay ~ CRSDepTime + DayOfWeek + CRSDepHour:DayOfWeek
    ```
    
    Se produce un error si el conjunto de datos de entrada no contiene columnas con los nombres coincidentes ArrDelay, CRSDepTime, DayOfWeek, CRSDepHour y DayOfWeek.

+ En algunos casos, un esquema de salida debe definirse de antemano para obtener los resultados.

    Por ejemplo, para insertar los datos en una tabla, debe usar el **con conjunto de resultados** cláusula para especificar el esquema.

    El esquema de salida también es necesario si el script de R usa el argumento `@parallel=1`. El motivo es que SQL Server puede crear varios procesos para ejecutar la consulta en paralelo, con los resultados recopilados al final. Por lo tanto, el esquema de salida debe estar preparado antes de que se pueden crear los procesos en paralelo.
    
    En otros casos, puede omitir el esquema de resultados mediante la opción **WITH RESULT SETS UNDEFINED**. Esta instrucción devuelve el conjunto de datos desde el script de R sin asignar las columnas o especificar los tipos de datos SQL.

+ Considere la posibilidad de generar datos de seguimiento o de tiempo mediante Transact-SQL en lugar de R.

    Por ejemplo, podría pasar la hora del sistema o la información que se utiliza para la auditoría y el almacenamiento mediante la adición de una llamada de Transact-SQL que se pasa a los resultados, en lugar de generar datos similares en el script de R. 

**Mejorar el rendimiento y seguridad**

+ Evitar la escritura de predicciones o los resultados intermedios en el archivo. Escribir las predicciones en una tabla en su lugar, para evitar el movimiento de datos.

+ Ejecute todas las consultas de antemano y revise los planes de consulta de SQL Server para identificar las tareas que pueden realizarse en paralelo.

    Si la consulta de entrada se puede paralelizar, establezca `@parallel=1` como parte de los argumentos de [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). 

    Por lo general, el procesamiento en paralelo con este indicador es posible siempre que SQL Server pueda trabajar con tablas con particiones o distribuir una consulta entre varios procesos y agregar los resultados al final. Normalmente, el procesamiento en paralelo con este indicador no es posible si entrena modelos mediante algoritmos que requieren que se lean todos los datos o si necesita crear agregados.

+ Revise el código de R para determinar si hay pasos que se pueden realizar independientemente o de una manera más eficiente, mediante una llamada de procedimiento almacenado independiente. Por ejemplo, podría obtener un mejor rendimiento, realizar ingeniería de características o extracción de características por separado y guardar los valores en una tabla.

+ Buscar formas de usar Transact-SQL en lugar de código de R para computaciones basadas en conjuntos.

    Por ejemplo, esta solución de R muestra cómo definido por el usuario las funciones de Transact-SQL y R puede realizar la misma tarea de ingeniería de características: [Tutorial de extremo a otro de ciencia de datos](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md).

+ Si es posible, reemplace las funciones de R convencionales con **ScaleR** funciones que admiten la ejecución distribuida. Para obtener más información, consulte [comparación de Base de R y funciones de R de escala](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler-compared-to-base-r).

+ Póngase en contacto con un desarrollador de la base de datos para determinar maneras de mejorar el rendimiento mediante características de SQL Server, como [tablas optimizadas para memoria](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables), o bien, si tiene licencias Enterprise Edition, [del regulador de recursos](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor)).

    Para obtener más información, consulte [sugerencias de optimización de SQL Server y trucos para los servicios de análisis](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

### <a name="step-3-prepare-for-deployment"></a>Paso 3. Preparación para la implementación

+ Notifique al administrador para que los paquetes se puedan instalar y probar antes de implementar el código. 

    En un entorno de desarrollo, podría ser conveniente instalar paquetes como parte del código, pero esto es una práctica incorrecta en un entorno de producción. 

    No se admiten las bibliotecas de usuario, independientemente de si está utilizando un procedimiento almacenado o ejecuta código R en el contexto de cálculo de SQL Server.

**Empaquete el código de R en un procedimiento almacenado**

+ Si el código es relativamente sencillo, puede insertarlo en una función definida por el usuario de Transact-SQL sin modificaciones, como se describe en estos ejemplos:

    + [Creación de una función de R que se ejecuta en rxExec](../tutorials/deepdive-create-a-simple-simulation.md)
    + [Ingeniería de características con Transact-SQL y R](../tutorials/sqldev-create-data-features-using-t-sql.md)

+ Si el código es más compleja, use el paquete de R **sqlrutils** para convertir el código. Este paquete está diseñado para ayudar a los usuarios experimentados de R a escribir código de procedimiento almacenado buena. 

    El primer paso es volver a escribir el código de R como una sola función con claramente definidas entradas y salidas.

    A continuación, utilice el **sqlrutils** paquete para generar las entradas y salidas en el formato correcto. El **sqlrutils** paquete genera el código de procedimiento almacenado completo para usted y también se puede registrar el procedimiento almacenado en la base de datos. 

    Para obtener más información y ejemplos, vea [sqlrutils (SQL)](ref-r-sqlrutils.md).

**Integrar con otros flujos de trabajo**

+ Aproveche las herramientas de Transact-SQL y procesos ETL. Realizar ingeniería de características, la extracción de características y la limpieza de datos de antemano como parte de los flujos de trabajo de datos.

    Cuando se trabaja en un entorno de desarrollo de R dedicado, como [!INCLUDE[rsql_rtvs_md](../../includes/rsql-rtvs-md.md)] o RStudio, usted podría extraer los datos en el equipo, analizar los datos de forma iterativa y, a continuación, escribir o mostrar los resultados. 
    
    Sin embargo, cuando se migra código de R independiente a SQL Server, gran parte de este proceso puede simplificar o delegar a otras herramientas de SQL Server. 

+ Utilice estrategias de visualización segura, asincrónica.

    Los usuarios de SQL Server a menudo no pueden obtener acceso a archivos en el servidor y herramientas de cliente SQL normalmente no admiten el dispositivo de gráficos de R. Si genera los trazados u otros gráficos como parte de la solución, considere la posibilidad de exportar los trazados como datos binarios y guardar en una tabla o escribir.

+ Ajustar la predicción y funciones de puntuación en los procedimientos almacenados para el acceso directo por las aplicaciones.

### <a name="other-resources"></a>Otros recursos

Para ver ejemplos de cómo se puede implementar una solución de R en SQL Server, vea estos ejemplos:

+ [Crear un modelo predictivo para la empresa de alquiler de esquís mediante R y SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/)

+ [Análisis en bases de datos para los desarrolladores de SQL](../tutorials/sqldev-in-database-r-for-sql-developers.md) muestra cómo puede hacer que el código de R más modular incluyéndolo en procedimientos almacenados

+ [Solución de ciencia de datos-to-End](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) incluye una comparación de ingeniería de características en R y T-SQL
