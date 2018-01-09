---
title: "Generar un procedimiento almacenado de R para el código de R con el paquete sqlrutils | Microsoft Docs"
ms.custom: 
ms.date: 02/28/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: d8739f16-ac26-4f69-870c-51c77cf286d3
caps.latest.revision: "8"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7f906136e7e948c7b4cbe2da2f60cc4c488b71e9
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package"></a>Generar un procedimiento almacenado de R para el código de R con el paquete sqlrutils
El paquete **sqlrutils** proporciona un mecanismo para que los usuarios de R inserten sus scripts de R en un procedimiento almacenado de T-SQL, registren dicho procedimiento almacenado en una base de datos y lo ejecuten desde un entorno de desarrollo de R. 

Al convertir el código de R para que se ejecute en un solo procedimiento almacenado, puede hacer un uso más eficaz de SQL Server R Services, que requiere que el script de R se incruste como parámetro en [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). El paquete **sqlrutils** le ayuda a generar este script de R incrustado y a establecer correctamente los parámetros relacionados.

El paquete **sqlrutils** lleva a cabo estas tareas:

- Guarda el script de T-SQL generado como una cadena dentro de una estructura de datos de R;
- opcionalmente, genera un archivo .sql para el script de T-SQL, que puede editar o ejecutar para crear un procedimiento almacenado; y
- registra el procedimiento almacenado recién creado en la instancia de SQL Server desde el entorno de desarrollo de R.

También puede ejecutar el procedimiento almacenado desde un entorno de R pasando los parámetros correctos y procesando los resultados. Asimismo, puede usar el procedimiento almacenado de SQL Server para admitir escenarios de integración de base de datos comunes, como ETL, el entrenamiento del modelo y la puntuación de gran volumen.

  > [!NOTE]
  > Si va a ejecutar el procedimiento almacenado desde un entorno de R llamando a la función *executeStoredProcedure* , debe usar un proveedor ODBC 3.8, como ODBC Driver 13 para SQL Server.  
  
## <a name="functions-provided-in-sqlrutils"></a>Funciones proporcionadas en sqlrutils

En la lista siguiente se proporciona un resumen de las funciones que se pueden llamar desde el paquete **sqlrutils** para desarrollar un procedimiento almacenado y usarlo en SQL Server R Services. Para obtener información detallada sobre los parámetros de cada método o función, consulte la Ayuda de R del paquete:

```R
help(package="sqlrutils") 
```

**Definir parámetros y entradas del procedimiento almacenado**

- `InputData`. Define el origen de los datos de SQL Server que se usarán en la trama de datos de R. Debe especificar el nombre de la trama de datos en la que almacenará los datos de entrada y una consulta para obtener los datos o un valor predeterminado. Solo se admiten las consultas SELECT simples.

- `InputParameter`. Define un parámetro de entrada que se incrustará en el script de T-SQL. Debe proporcionar el nombre del parámetro y el tipo de datos de R.

- `OutputData`. Genera un objeto de datos intermedio que es necesario si la función de R devuelve una lista que contiene data.frame. 
   El objeto *OutputData* se usa para almacenar el nombre de una data.frame obtenida de la lista. 

- `OutputParameter`. Genera un objeto de datos intermedio que es necesario si la función de R devuelve una lista. El objeto *OutputParameter* almacena el nombre y el tipo de datos de un único miembro de la lista, suponiendo que dicho miembro **no** sea una trama de datos. 


**Generar y registrar el procedimiento almacenado**


- `StoredProcedure` es el constructor principal empleado para crear el procedimiento almacenado.  Este constructor genera un objeto de *procedimiento almacenado de SQL Server* y, opcionalmente, crea un archivo de texto que contiene una consulta que puede usarse para generar el procedimiento almacenado mediante un comando de T-SQL. Además, la función *StoredProcedure* también puede registrar el procedimiento almacenado en la instancia y la base de datos especificadas.

   + Use el argumento `func` para especificar una función de R válida. Todas las variables que usa la función deben definirse dentro de la función o deben proporcionarse como parámetros de entrada. Estos parámetros pueden incluir una trama de datos como máximo.
   + La función de R debe devolver una trama de datos, una lista con nombre o un valor NULL. Si la función devuelve una lista, esta puede contener una data.frame como máximo.
   + Utilice el argumento `spName` para especificar el nombre del procedimiento almacenado que quiere crear.
   + Puede pasar parámetros de salida y de entrada opcionales usando los objetos creados por las funciones auxiliares `setInputData`, `setInputParameter`y `setOutputParameter`.
   +  Opcionalmente, use `filePath` para proporcionar la ruta de acceso y el nombre de un archivo .sql que vaya a crear. Puede ejecutar este archivo en la instancia de SQL Server para generar el procedimiento almacenado con T-SQL.
   + Para definir el servidor y la base de datos donde se guardará el procedimiento almacenado, use los argumentos `dbName` y  `connectionString`.
   + Para obtener una lista de los objetos *InputData* e *InputParameter* utilizados para crear un determinado objeto *StoredProcedure* , llame a `getInputParameters`. 
   + Para registrar el procedimiento almacenado en la base de datos especificada, use `registerStoredProcedure`.

   El objeto del procedimiento almacenado no suele tener datos o valores asociados, a menos que se haya especificado un valor predeterminado. No se recuperan datos hasta que se ejecute el procedimiento almacenado. 


**Especificar entradas y ejecutar**

- Utilice `setInputDataQuery` para asignar una consulta a un objeto *InputParameter* . Por ejemplo, si ha creado un objeto de procedimiento almacenado en R, puede usar `setInputDataQuery` para pasar argumentos a la función *StoredProcedure* con el objetivo de ejecutar el procedimiento almacenado con las entradas deseadas.

- Utilice `setInputValue` para asignar valores específicos a un parámetro almacenado como objeto *InputParameter* . Luego, pase el objeto del parámetro y su asignación de valores a la función *StoredProcedure* para ejecutar el procedimiento almacenado con los valores establecidos.

- Utilice `executeStoredProcedure` para ejecutar un procedimiento almacenado definido como objeto *StoredProcedure* . Llame a esta función solo cuando ejecute un procedimiento almacenado desde el código de R. No la use si ejecuta el procedimiento almacenado desde SQL Server mediante T-SQL.

  > [!NOTE]
  > La función *executeStoredProcedure* requiere un proveedor ODBC 3.8, como ODBC Driver 13 for SQL Server.  
  
  



## <a name="see-also"></a>Vea también
[Cómo crear un procedimiento almacenado mediante sqlrutils](../../advanced-analytics/r-services/how-to-create-a-stored-procedure-using-sqlrutils.md)

