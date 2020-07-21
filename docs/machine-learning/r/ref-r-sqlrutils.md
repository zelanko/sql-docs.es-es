---
title: Funciones auxiliares de sqlrutils
description: Use la biblioteca de funciones sqlrutils en SQL Server 2016 R Services y SQL Server Machine Learning Services con R para generar procedimientos almacenados que contengan scripts de R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3de8d438691afb7ebf1aabe15265227b7876b837
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/04/2020
ms.locfileid: "81117398"
---
# <a name="sqlrutils-r-library-in-sql-server"></a>sqlrutils (biblioteca de R en SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

El paquete **sqlrutils** proporciona un mecanismo para que los usuarios de R inserten sus scripts de R en un procedimiento almacenado de T-SQL, registren dicho procedimiento almacenado en una base de datos y lo ejecuten desde un entorno de desarrollo de R. 

Al convertir el código de R para que se ejecute en un solo procedimiento almacenado, puede hacer un uso más eficaz de SQL Server R Services, que requiere que el script de R se incruste como parámetro en [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). El paquete **sqlrutils** le ayuda a generar este script de R incrustado y a establecer correctamente los parámetros relacionados.

El paquete **sqlrutils** lleva a cabo estas tareas:

- Guarda el script de T-SQL generado como una cadena dentro de una estructura de datos de R;
- opcionalmente, genera un archivo .sql para el script de T-SQL, que puede editar o ejecutar para crear un procedimiento almacenado; y
- registra el procedimiento almacenado recién creado en la instancia de SQL Server desde el entorno de desarrollo de R.

También puede ejecutar el procedimiento almacenado desde un entorno de R pasando los parámetros correctos y procesando los resultados. Asimismo, puede usar el procedimiento almacenado de SQL Server para admitir escenarios de integración de base de datos comunes, como ETL, el entrenamiento del modelo y la puntuación de gran volumen.

  > [!NOTE]
  > Si va a ejecutar el procedimiento almacenado desde un entorno de R llamando a la función *executeStoredProcedure* , debe usar un proveedor ODBC 3.8, como ODBC Driver 13 para SQL Server.  
  
## <a name="full-reference-documentation"></a>Documentación de referencia completa

La biblioteca de **sqlrutils** se distribuye en varios productos de Microsoft, pero el uso es el mismo, se obtenga la biblioteca en SQL Server o en otro producto. Dado que las funciones son las mismas, la [documentación de las funciones individuales de sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) se publica en una sola ubicación en la [referencia de R](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) para Microsoft Machine Learning Server. Si existe algún comportamiento específico del producto, las discrepancias se anotarán en la página de ayuda de la función.

## <a name="functions-list"></a>Lista de funciones

En la sección siguiente se proporciona un resumen de las funciones que se pueden llamar desde el paquete **sqlrutils** para desarrollar un procedimiento almacenado que contenga un código de R incrustado. Para obtener información detallada sobre los parámetros de cada método o función, consulte la Ayuda de R del paquete: `help(package="sqlrutils")`

|Función | Descripción |
|------|-------------|
|[executeStoredProcedure](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/executestoredprocedure)| Ejecuta un procedimiento almacenado de SQL.|
|[getInputParameters](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/getinputparameters)| Obtiene una lista de parámetros de entrada para el procedimiento almacenado.| 
|[InputData](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/inputdata)| Define el origen de los datos de SQL Server que se usarán en la trama de datos de R. Debe especificar el nombre de la trama de datos en la que almacenará los datos de entrada y una consulta para obtener los datos o un valor predeterminado. Solo se admiten las consultas SELECT simples. | 
|[InputParameter](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/inputparameter)| Define un parámetro de entrada que se incrustará en el script de T-SQL. Debe proporcionar el nombre del parámetro y el tipo de datos de R.| 
|[OutputData](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/outputdata)| Genera un objeto de datos intermedio que es necesario si la función de R devuelve una lista que contiene data.frame. El objeto *OutputData* se usa para almacenar el nombre de una data.frame obtenida de la lista.| 
|[OutputParameter](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/outputparameter) | Genera un objeto de datos intermedio que es necesario si la función de R devuelve una lista. El objeto *OutputParameter* almacena el nombre y el tipo de datos de un único miembro de la lista, suponiendo que dicho miembro **no** sea una trama de datos. |
|[registerStoredProcedure](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/registerstoredprocedure) | Registra el procedimiento almacenado en una base de datos.|
|[setInputDataQuery](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/setinputdataquery)| Asigna una consulta a un parámetro de datos de entrada del procedimiento almacenado.| 
|[setInputParameterValue](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/setinputparametervalue)| Asigna un valor a un parámetro de entrada del procedimiento almacenado.| 
|[StoredProcedure](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/storedprocedure)| Objeto de procedimiento almacenado.|


## <a name="how-to-use-sqlrutils"></a>Cómo usar sqlrutils

Las funciones de la biblioteca de **sqlrutils** deben ejecutarse en un equipo que tenga SQL Server Machine Learning con R. Si está trabajando en una estación de trabajo cliente, establezca un contexto de cálculo remoto para que la ejecución cambie a SQL Server. El flujo de trabajo para usar este paquete incluye los pasos siguientes:

+ Definir los parámetros de los procedimientos almacenados (entradas, salidas o ambos) 
+ Generar y registrar el procedimiento almacenado    
+ Ejecutar el procedimiento almacenado  

En una sesión de R, cargue **sqlrutils** desde la línea de comandos escribiendo `library(sqlrutils)`.

> [!Note]
> Puede cargar esta biblioteca en un equipo que no tiene SQL Server (por ejemplo, en una instancia de cliente de R) si cambia el contexto de cálculo a SQL Server y ejecuta el código en ese contexto de cálculo.


### <a name="define-stored-procedure-parameters-and-inputs"></a>Definición de parámetros y entradas del procedimiento almacenado

`StoredProcedure` es el constructor principal empleado para crear el procedimiento almacenado. Este constructor genera un objeto de *procedimiento almacenado de SQL Server* y, opcionalmente, crea un archivo de texto que contiene una consulta que puede usarse para generar el procedimiento almacenado mediante un comando de T-SQL. 

Además, la función *StoredProcedure* también puede registrar el procedimiento almacenado en la instancia y la base de datos especificadas.

+ Use el argumento `func` para especificar una función de R válida. Todas las variables que usa la función deben definirse dentro de la función o deben proporcionarse como parámetros de entrada. Estos parámetros pueden incluir una trama de datos como máximo.

+ La función de R debe devolver una trama de datos, una lista con nombre o un valor NULL. Si la función devuelve una lista, esta puede contener una data.frame como máximo.

+ Utilice el argumento `spName` para especificar el nombre del procedimiento almacenado que quiere crear.

+ Puede pasar parámetros de salida y de entrada opcionales usando los objetos creados por las funciones del asistente `setInputData`, `setInputParameter` y `setOutputParameter`.

+  Opcionalmente, use `filePath` para proporcionar la ruta de acceso y el nombre de un archivo .sql que vaya a crear. Puede ejecutar este archivo en la instancia de SQL Server para generar el procedimiento almacenado con T-SQL.

+ Para definir el servidor y la base de datos donde se guardará el procedimiento almacenado, use los argumentos `dbName` y  `connectionString`.

+ Para obtener una lista de los objetos *InputData* e *InputParameter* utilizados para crear un determinado objeto *StoredProcedure* , llame a `getInputParameters`. 

+ Para registrar el procedimiento almacenado en la base de datos especificada, use `registerStoredProcedure`.

El objeto del procedimiento almacenado no suele tener datos o valores asociados, a menos que se haya especificado un valor predeterminado. No se recuperan datos hasta que se ejecute el procedimiento almacenado. 

### <a name="specify-inputs-and-execute"></a>Especificación de entradas y ejecución

+ Utilice `setInputDataQuery` para asignar una consulta a un objeto *InputParameter* . Por ejemplo, si ha creado un objeto de procedimiento almacenado en R, puede usar `setInputDataQuery` para pasar argumentos a la función *StoredProcedure* con el objetivo de ejecutar el procedimiento almacenado con las entradas deseadas.

+ Utilice `setInputValue` para asignar valores específicos a un parámetro almacenado como objeto *InputParameter* . Luego, pase el objeto del parámetro y su asignación de valores a la función *StoredProcedure* para ejecutar el procedimiento almacenado con los valores establecidos.

+ Utilice `executeStoredProcedure` para ejecutar un procedimiento almacenado definido como objeto *StoredProcedure* . Llame a esta función solo cuando ejecute un procedimiento almacenado desde el código de R. No la use si ejecuta el procedimiento almacenado desde SQL Server mediante T-SQL.

> [!NOTE]
> La función *executeStoredProcedure* requiere un proveedor ODBC 3.8, como ODBC Driver 13 for SQL Server.  

## <a name="see-also"></a>Consulte también

[Cómo crear un procedimiento almacenado mediante sqlrutils](how-to-create-a-stored-procedure-using-sqlrutils.md)

