---
title: Convertir código de R para su uso en servicios de aprendizaje de máquina de SQL Server | Documentos de Microsoft"
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: bf3d272bd4b5c1227aa8a1969727ea17f5b65596
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="convert-r-code-for-execution-in-sql-server-in-database-instances"></a>Convertir código de R para la ejecución en instancias de SQL Server (In-Database)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo proporciona orientación de alto nivel acerca de cómo modificar el código de R en SQL Server. 

Cuando mueve el código de R de R Studio o con otro entorno a SQL Server, el código funciona con mayor frecuencia sin modificaciones adicionales: por ejemplo, si el código es sencillo, como una función que toma algunas entradas y devuelve un valor. También es más fácil a las soluciones de puerto que usen la **RevoScaleR** o **MicrosoftML** paquetes, que admiten la ejecución en contextos de ejecución distintos con cambios mínimos.

Sin embargo, el código puede requerir cambios sustanciales si cualquiera de los casos siguientes:

+ Utilizar bibliotecas de R que acceder a la red o que no se puede instalar en SQL Server.
+ El código realiza las llamadas independientes a orígenes de datos fuera de SQL Server, como las hojas de cálculo de Excel, archivos en recursos compartidos y otras bases de datos. 
+ Desea ejecutar el código de la *@script* parámetro de [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) y también parametrizar el procedimiento almacenado.
+ La solución original incluye varios pasos que podrían ser más eficaces en un entorno de producción si ejecuta de forma independiente, como la preparación de datos o de ingeniería de característica frente a modelo de entrenamiento, la puntuación o informes.
+ Desea mejorar optimizar el rendimiento cambiando las bibliotecas, mediante la ejecución en paralelo, o descargar algunos procesamientos a SQL Server. 

## <a name="step-1-plan-requirements-and-resources"></a>Paso 1. Requisitos del plan y recursos

**Paquetes**

+ Determinar qué paquetes son necesarios y asegurarse de que funcionan en SQL Server.
 
+ Instalar paquetes de antemano, en la biblioteca de paquete predeterminado utilizada por servicios de aprendizaje de máquina. No se admiten las bibliotecas de usuario.

**Orígenes de datos** 

+ Si desea incrustar el código de R en [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), identifique los orígenes de datos principal y secundaria. 

    + **Principal** orígenes de datos son grandes conjuntos de datos, por ejemplo, datos de entrenamiento del modelo y datos de entrada para las predicciones. Plan asignar el conjunto de datos más grande para el parámetro de entrada de [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

    + **Secundaria** orígenes de datos son normalmente más pequeños conjuntos de datos, como listas de factores o variables de agrupación adicional. 
    
    Actualmente, sp_execute_external_script admite un único conjunto de datos como entrada para el procedimiento almacenado. Sin embargo, puede agregar varias entradas escalares o binarias.

    Llamadas a procedimientos almacenados precedidas de la ejecución no se puede usar como entrada para [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Puede usar las consultas, vistas o cualquier otra instrucción SELECT válida.

+ Determinar los resultados que necesita. Si ejecuta código de R mediante sp_execute_external_script, el procedimiento almacenado puede generar como resultado un solo marco de datos. Sin embargo, también puede generar varias salidas escalares, incluidos los gráficos y modelos en formato binario, así como otros valores escalares derivan de SQL o código R parámetros.

**Tipos de datos**

+ Haga una lista de comprobación de posibles problemas de tipos de datos.

    Todos los tipos de datos de R son compatibles con servicios de aprendizaje de máquina de SQL Server. Sin embargo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es compatible con una gran variedad de tipos de datos de r. Por lo tanto, algunas conversiones de tipos de datos implícitas se realizan al enviar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos a R y viceversa. Deberá convertir explícitamente o convertir algunos datos. 

    Se admiten valores NULL. Sin embargo, se usa R el `na` construcción de datos para representar un valor que falta, que es similar a un valor null.

+ Tenga en cuenta lo que elimina la dependencia de datos que no se puede usar por R: rowid por ejemplo como GUID tipos de datos de SQL Server no pueden utilizarse en R y generan errores.

    Para obtener más información, consulte [tipos de datos y bibliotecas de R](../r/r-libraries-and-data-types.md).

## <a name="step-2-convert-or-repackage-code"></a>Paso 2. Convertir o volver a empaquetar código

¿Cuánto cambiará el código depende de si va a enviar el código de R desde un cliente remoto para que se ejecute en el contexto de proceso de SQL Server, o va a implementar el código como parte de un procedimiento almacenado, lo que puede proporcionar un mejor rendimiento y seguridad de los datos. Ajustar el código en un procedimiento almacenado, impone algunos requisitos adicionales. 

+ Definir los datos de entrada principales como una consulta SQL siempre que sea posible, para evitar el movimiento de datos.

+ Al ejecutar código R en un procedimiento almacenado, también puede pasar a través de varios **escalares** entradas. Para los parámetros que desea utilizar en la salida, agregue el **salida** palabra clave. 

    Por ejemplo, la siguiente entrada escalar `@model_name` contiene el nombre del modelo, que también es la salida en su propia columna en los resultados:

    ```SQL
    EXEC sp_execute_external_script @model_name="DefaultModel" OUTPUT, @language=N'R', @script=N'R code here'
    ``` 

+ Las variables que se pasan como parámetros del procedimiento almacenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) deben asignarse a variables en el código de R. De forma predeterminada, las variables se asignan por nombre.

    Todas las columnas del conjunto de datos de entrada también deben asignarse a variables en el script de R.  Por ejemplo, suponga que el script de R contiene una fórmula como esta:

    ```R
    formula <- ArrDelay ~ CRSDepTime + DayOfWeek + CRSDepHour:DayOfWeek
    ```
    
    Se produce un error si el conjunto de datos de entrada no contiene columnas con los nombres coincidentes ArrDelay, CRSDepTime, DayOfWeek, CRSDepHour y DayOfWeek.

+ En algunos casos, un esquema de salida debe definirse de antemano para obtener los resultados.

    Por ejemplo, para insertar los datos en una tabla, debe utilizar el **con conjunto de resultados** cláusula para especificar el esquema.

    El esquema de salida también es necesario si el script de R utiliza el argumento `@parallel=1`. El motivo es que SQL Server puede crear varios procesos para ejecutar la consulta en paralelo, con los resultados recopilados al final. Por lo tanto, el esquema de salida debe estar preparado para pueden crear los procesos en paralelo.
    
    En otros casos, puede omitir el esquema de resultados mediante la opción **con RESULT SETS UNDEFINED**. Esta instrucción devuelve el conjunto de datos de la secuencia de comandos de R sin nombres de las columnas o especificar los tipos de datos SQL.

+ Puede ser conveniente generar tiempo o hacer un seguimiento de los datos mediante T-SQL, en lugar de R.

    Por ejemplo, podría pasar la hora del sistema o la información que se utiliza para la auditoría y el almacenamiento mediante la adición de una llamada de T-SQL que se pasa a los resultados, en lugar de generar datos similares en el script de R. 

**Mejorar el rendimiento y seguridad**

+ Evite escribir predicciones o resultados intermedios en el archivo. Escribir las predicciones en una tabla en su lugar, para evitar el movimiento de datos.

+ Ejecutar todas las consultas de antemano y revisar los planes de consulta de SQL Server para identificar las tareas que pueden realizarse en paralelo.

    Si la consulta de entrada se puede ejecutar en paralelo, establezca `@parallel=1` como parte de los argumentos a [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). 

    Por lo general, el procesamiento en paralelo con este indicador es posible siempre que SQL Server pueda trabajar con tablas con particiones o distribuir una consulta entre varios procesos y agregar los resultados al final. Normalmente, el procesamiento en paralelo con este indicador no es posible si entrena modelos mediante algoritmos que requieren que se lean todos los datos o si necesita crear agregados.

+ Revise el código de R para determinar si hay pasos que se pueden realizar independientemente o de una manera más eficiente, mediante una llamada de procedimiento almacenado independiente. Por ejemplo, podría obtener un mejor rendimiento realizando ingeniería característica o extracción de características por separado, y guardar los valores en una tabla.

+ Buscar formas de usar T-SQL en lugar del código de R para realizar cálculos basados en conjuntos.

    Por ejemplo, esta solución R muestra cómo definido por el usuario funciones de T-SQL y R puede realizar la misma tarea de ingeniería de característica: [tutorial de ciencia de datos-to-End](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md).

+ Si es posible, reemplace las funciones de R convencionales con **ScaleR** funciones que admite la ejecución distribuida. Para obtener más información, consulte [comparación de Base de R y funciones de R de escala](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler-compared-to-base-r).

+ Consulte con un programador de la base de datos para determinar maneras de mejorar el rendimiento mediante las características de SQL Server como [tablas optimizadas en memoria](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables), o bien, si dispone de Enterprise Edition, [regulador de recursos](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor)).

    Para obtener más información, vea [sugerencias de optimización de SQL Server y trucos para servicios de análisis](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

### <a name="step-3-prepare-for-deployment"></a>Paso 3. Prepararse para la implementación

+ Notifique al administrador para que los paquetes se puedan instalar y probar antes de implementar el código. 

    En un entorno de desarrollo, puede que sea correcto instalar paquetes como parte del código, pero se trata de una práctica incorrecta en un entorno de producción. 

    No se admiten las bibliotecas de usuario, independientemente de si se utiliza un procedimiento almacenado o ejecutar código R en el contexto de proceso de SQL Server.

**Empaquetar el código de R en un procedimiento almacenado**

+ Si el código es relativamente simple, puede incrustar en una función definida por el usuario de T-SQL sin modificaciones, como se describe en estos ejemplos:

    + [Crear una función de R que se ejecuta en rxExec](..\tutorials\deepdive-create-a-simple-simulation.md)
    + [Ingeniería de característica con T-SQL y R](..\tutorials\sqldev-create-data-features-using-t-sql.md)

+ Si el código es más complejo, use el paquete de R **sqlrutils** para convertir el código. Este paquete está diseñado para ayudar a los usuarios experimentados de R a escribir código de procedimiento almacenado buena. 

    El primer paso es escribir el código de R como una sola función con claramente definidas entradas y salidas.

    A continuación, utilice la **sqlrutils** paquete para generar la entrada y las salidas en el formato correcto. El **sqlrutils** paquete genera el código de todo el procedimiento almacenado para usted y también se puede registrar el procedimiento almacenado en la base de datos. 

    Para obtener más información y ejemplos, vea [SqlRUtils](../r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md).

**Integrar con otros flujos de trabajo**

+ Aprovechar las herramientas de T-SQL y procesos ETL. Realizar ingeniería de característica, extracción de características y la limpieza de datos de antemano como parte de los flujos de trabajo de datos.

    Cuando se trabaja en un entorno de desarrollo de R dedicado como [!INCLUDE[rsql_rtvs_md](../../includes/rsql-rtvs-md.md)] o RStudio, puede extraer los datos en el equipo, analizar los datos de forma iterativa y, a continuación, escribir o mostrar los resultados. 
    
    Sin embargo, cuando se migra código independiente para SQL Server, gran parte de este proceso puede simplificado o delegar a otras herramientas de SQL Server. 

+ Use las estrategias de visualización segura, asincrónica.

    Los usuarios de SQL Server a menudo no pueden tener acceso a archivos en el servidor y herramientas de cliente SQL normalmente no admiten el dispositivo de gráficos de R. Si los gráficos u otros gráficos se generan como parte de la solución, considere la posibilidad de exportar los gráficos como datos binarios y guardar en una tabla o escribir.

+ Ajustar la predicción y funciones de puntuación en los procedimientos almacenados para el acceso directo por las aplicaciones.

### <a name="other-resources"></a>Otros recursos

Para ver ejemplos de cómo se puede implementar una solución en R en SQL Server, vea estos ejemplos:

+ [Crear un modelo de predicción para la empresa de alquiler de ski mediante R y SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/)

+ [Análisis de bases de datos para que el programador de SQL](../tutorials/sqldev-in-database-r-for-sql-developers.md) se muestra cómo hacer que el código de R más modular incluyéndolo en procedimientos almacenados

+ [Soluciones de ciencia de datos-to-End](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) incluye una comparación de ingeniería de características en R y T-SQL
