---
title: Procesar resultados (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC], about result sets
- SQLRowCount function
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- COMPUTE clause
- result sets [ODBC]
- COMPUTE BY clause
ms.assetid: 61a8db19-6571-47dd-84e8-fcc97cb60b45
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 761f74a56fd846361ca98dd8f2746a01b53106ec
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82699317"
---
# <a name="processing-results-odbc"></a>Procesar los resultados (ODBC)
  Después de que una aplicación envía una instrucción SQL, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve los datos resultantes como uno o varios conjuntos de resultados. Un conjunto de resultados es un conjunto de filas y columnas que coinciden con los criterios de la consulta. Las instrucciones SELECT, las funciones de catálogo y algunos procedimientos almacenados generan un conjunto de resultados que quedan disponibles para las aplicaciones en formato tabular. Si la instrucción SQL ejecutada es un procedimiento almacenado, un lote que contiene varios comandos o una instrucción SELECT que contiene palabras clave, habrá varios conjuntos de resultados que procesar.  
  
 Las funciones de catálogo de ODBC también pueden recuperar los datos. Por ejemplo, [SQLColumns](../native-client-odbc-api/sqlcolumns.md) recupera datos acerca de las columnas del origen de datos. Estos conjuntos de resultados pueden contener ninguna o más filas.  
  
 Otras instrucciones SQL, como GRANT o REVOKE, no devuelven conjuntos de resultados. En estas instrucciones, el código de retorno de **SQLExecute** o **SQLExecDirect** suele ser la única indicación de que la instrucción se ha realizado correctamente.  
  
 Cada instrucción INSERT, UPDATE y DELETE devuelve un conjunto de resultados que contiene solamente el número de filas afectado por la modificación. Este recuento está disponible cuando la aplicación llama a [SQLRowCount](../native-client-odbc-api/sqlrowcount.md). ODBC 3. las aplicaciones *x* deben llamar a **SQLRowCount** para recuperar el conjunto de resultados o [SQLMoreResults](../native-client-odbc-api/sqlmoreresults.md) para cancelarlo. Cuando una aplicación ejecuta un proceso por lotes o un procedimiento almacenado que contiene varias instrucciones INSERT, UPDATE o DELETE, el conjunto de resultados de cada instrucción de modificación debe procesarse mediante **SQLRowCount** o cancelarse mediante **SQLMoreResults**. Estos recuentos se pueden cancelar incluyendo una instrucción SET NOCOUNT ON en el lote o procedimiento almacenado.  
  
 Transact-SQL incluye la instrucción SET NOCOUNT. Cuando la opción NOCOUNT está establecida en ON, SQL Server no devuelve los recuentos de las filas afectadas por una instrucción y **SQLRowCount** devuelve 0. La [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versión del controlador ODBC de Native Client introduce una opción [SQLGetStmtAttr](../native-client-odbc-api/sqlgetstmtattr.md) específica del controlador, SQL_SOPT_SS_NOCOUNT_STATUS, para notificar si la opción NOCOUNT está activada o desactivada. Cada vez que **SQLRowCount** devuelve 0, la aplicación debe probar SQL_SOPT_SS_NOCOUNT_STATUS. Si se devuelve SQL_NC_ON, el valor 0 de **SQLRowCount** solo indica que SQL Server no ha devuelto un recuento de filas. Si se devuelve SQL_NC_OFF, significa que NOCOUNT es OFF y el valor 0 de **SQLRowCount** indica que la instrucción no afectó a ninguna fila. Las aplicaciones no deben mostrar el valor de **SQLRowCount** cuando se SQL_NC_OFF SQL_SOPT_SS_NOCOUNT_STATUS. Los procedimientos almacenados o lotes de gran tamaño pueden contener varias instrucciones SET NOCOUNT de modo que los programadores no puedan suponer que SQL_SOPT_SS_NOCOUNT_STATUS sigue siendo constante. La opción se debe probar cada vez que **SQLRowCount** devuelve 0.  
  
 Otras instrucciones Transact-SQL devuelven los datos en mensajes, en lugar de en conjuntos de resultados. Cuando el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client recibe estos mensajes, devuelve SQL_SUCCESS_WITH_INFO para que la aplicación sepa que los mensajes informativos están disponibles. A continuación, la aplicación puede llamar a **SQLGetDiagRec** para recuperar estos mensajes. Las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] que funcionan de esta manera son:  
  
-   DBCC  
  
-   SET SHOWPLAN (disponible con versiones anteriores de SQL Server)  
  
-   SET STATISTICS  
  
-   PRINT  
  
-   RAISERROR  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client devuelve SQL_ERROR en RAISERROR con una gravedad de 11 o superior. Si la gravedad del RAISERROR es 19 o superior, se interrumpe además la conexión.  
  
 Para procesar los conjuntos de resultados de una instrucción SQL, la aplicación:  
  
-   Determina las características del conjunto de resultados.  
  
-   Enlaza las columnas a variables de programa.  
  
-   Recupera un valor único, una fila completa de valores o varias filas de valores.  
  
-   Comprueba si hay más conjuntos de resultados y, en caso afirmativo, recorre de nuevo el bucle para determinar las características del nuevo conjunto de resultados.  
  
 El proceso de recuperar filas del origen de datos y devolverlas a la aplicación se denomina captura.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Determinar las características de un conjunto de resultados &#40;ODBC&#41;](determining-the-characteristics-of-a-result-set-odbc.md)  
  
-   [Asignar almacenamiento](assigning-storage.md)  
  
-   [Capturar datos de resultados](fetching-result-data.md)  
  
-   [Asignar tipos de datos &#40;&#41;ODBC](mapping-data-types-odbc.md)  
  
-   [Uso de tipos de datos](data-type-usage.md)  
  
-   [Traducción automática de datos de caracteres](autotranslation-of-character-data.md)  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server Native Client &#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)   
 [Temas de procedimientos de procesamiento de resultados &#40;ODBC&#41;](../../database-engine/dev-guide/processing-results-how-to-topics-odbc.md)  
  
  
