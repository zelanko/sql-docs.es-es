---
title: "Formato de cadena de conexión y los atributos | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connection strings [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], connection strings
ms.assetid: 0c360112-8720-4e54-a1a6-b9b18d943557
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 79d5cabb884262b052429da53cf19c360048dd21
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="connection-string-format-and-attributes"></a>Atributos y el formato de cadena de conexión
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 En lugar de usar un cuadro de diálogo, algunas aplicaciones pueden necesitar una cadena de conexión que especifica la información de conexión del origen de datos. La cadena de conexión se compone de un número de atributos que especifican cómo se conecta un controlador a un origen de datos. Un atributo identifica una parte específica de la información que el controlador necesita saber antes de poder realizar la conexión de origen de datos adecuado. Cada controlador puede tener un conjunto diferente de los atributos, pero el formato de cadena de conexión es siempre el mismo. Una cadena de conexión tiene el formato siguiente:  
  
```  
"DSN=data-source-name[;SERVER=value] [;PWD=value] [;UID=value] [;<Attribute>=<value>]"  
```  
  
> [!NOTE]  
>  El controlador ODBC de Microsoft para Oracle admite el formato de cadena de conexión de la primera versión del controlador, que utiliza `CONNECTSTRING`= en lugar de `SERVER=`.  
  
 Si se conecta a un proveedor de origen de datos que admita la autenticación de Windows, debe especificar `Trusted_Connection=yes` en lugar de la información de identificador y la contraseña de usuario en la cadena de conexión.  
  
 Debe especificar el origen de datos si no especifica el UID, PWD, SERVER (o CONNECTSTRING), el nombre y atributos del controlador. Sin embargo, todos los demás atributos son opcionales. Si no especifica un atributo, dicho atributo tiene como valor predeterminado se especificó en la ficha DSN relevante de la **Administrador de orígenes de datos ODBC** cuadro de diálogo. El valor del atributo podría ser entre mayúsculas y minúsculas.  
  
 Los atributos de la cadena de conexión son los siguientes:  
  
|Attribute|Description|Valor predeterminado|  
|---------------|-----------------|-------------------|  
|DSN|El nombre de origen de datos aparece en la ficha controladores de la **Administrador de orígenes de datos ODBC** cuadro de diálogo.|""|  
|PWD|La contraseña para el servidor de Oracle que desea obtener acceso. Este controlador es compatible con las limitaciones que Oracle aplica a las contraseñas.|""|  
|SERVER|La cadena de conexión para el servidor de Oracle que desea obtener acceso.|""|  
|UID|El nombre de usuario del servidor de Oracle. Dependiendo del sistema, este atributo no puede ser opcional, es decir, ciertas tablas y bases de datos podrían requerir este atributo por motivos de seguridad.<br /><br /> Use "/" usar Oracle instrucciones de la autenticación del sistema.|""|  
|BUFFERSIZE|El tamaño de búfer óptima que se utiliza al recuperar columnas.<br /><br /> El controlador optimiza la recuperación así que una búsqueda desde el servidor Oracle devuelve las filas suficientes para rellenar un búfer de este tamaño. Los valores más grandes tienden a aumentar el rendimiento si captura una gran cantidad de datos.|65535|  
|SYNONYMCOLUMNS|Cuando este valor es true (1), una llamada de API de () SQLColumn devuelve información de columna. En caso contrario, () SQLColumn devuelve solo las columnas de tablas y vistas. El controlador ODBC para Oracle proporciona un acceso más rápido si no se establece este valor.|1|  
|REMARKS|Cuando este valor es true (1), el controlador devuelve columnas de la sección Comentarios para el [SQLColumns](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md) conjunto de resultados. El controlador ODBC para Oracle proporciona un acceso más rápido si no se establece este valor.|0|  
|StdDayOfWeek|Aplica el estándar ODBC para la escala DAYOFWEEK. De forma predeterminada este está activado, pero los usuarios que necesitan la versión localizada pueden cambiar el comportamiento para que utilice cualquier Oracle devuelve.|1|  
|GuessTheColDef|Especifica si el controlador debe devolver un valor distinto de cero para la *cbColDef* argumento de **SQLDescribeCol**. Se aplica únicamente a las columnas donde no hay escala definido de Oracle, como calcular numéricas columnas y columnas definidas como NUMBER sin precisión o escala. A **SQLDescribeCol** llamar devuelve 130 para la precisión cuando Oracle no proporciona dicha información.|0|  
  
 Por ejemplo, podría ser una cadena de conexión que se conecta al origen de datos MyDataSource con el servidor de MyOracleServerOracle y la MyUserID de usuario de Oracle:  
  
```  
"DSN={MyDataSource};UID={MyUserID};PWD={MyPassword};SERVER={MyOracleServer}"  
```  
  
 Una cadena de conexión que se conecta al origen de datos MyOtherDataSource mediante la autenticación de sistema operativo y el servidor de MyOtherOracleServerOracle sería:  
  
```  
"DSN=MyOtherDataSource;UID=/;PWD=;SERVER=MyOtherOracleServer"  
```
