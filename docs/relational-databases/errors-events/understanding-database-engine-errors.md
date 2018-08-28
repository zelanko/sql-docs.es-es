---
title: Descripción de errores del motor de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [SQL Server], about errors
- errors [SQL Server], Database Engine
- errors [SQL Server]
- Database Engine [SQL Server], errors
ms.assetid: ddaca9d3-956f-46a5-8cd3-a7a15ec75878
caps.latest.revision: 27
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8f7326aab9deb664b439f32407c725b9a32c5fa8
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43071906"
---
# <a name="understanding-database-engine-errors"></a>Descripción de errores del motor de base de datos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  En la tabla siguiente se describen los atributos de los errores mostrados por [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] .  
  
|Attribute|Descripción|  
|---------------|-----------------|  
|Número de error|Cada mensaje de error tiene un número de error único.|  
|Cadena de mensaje de error|El mensaje de error contiene información de diagnóstico acerca de la causa del error. Muchos mensajes de error tienen variables de sustitución en las que se inserta información como, por ejemplo, el nombre del objeto que genera el error.|  
|Severity|La gravedad indica la importancia del error. Los errores que tienen una gravedad baja, como 1 o 2, son mensajes informativos o advertencias de bajo nivel. Los errores que tienen una gravedad alta indican problemas que deben ser atendidos tan pronto como sea posible. Para obtener más información sobre los niveles de gravedad, vea [Niveles de gravedad de error del motor de base de datos](../../relational-databases/errors-events/database-engine-error-severities.md).|  
|State|Algunos mensajes de error se pueden generar en varios puntos del código de [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Por ejemplo, el error 1105 se puede generar bajo diferentes condiciones. Cada condición específica bajo la que se genera un error asigna un código de estado único.<br /><br /> Cuando vea bases de datos que contengan información sobre problemas conocidos como, por ejemplo, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Knowledge Base, puede utilizar el número de estado para determinar si el problema registrado es el mismo que el error con el que se ha encontrado. Por ejemplo, si un artículo de Knowledge Base describe un error 1105 que tiene un estado 2 y el mensaje de error 1105 que ha recibido tenía un estado 3, el error tendrá probablemente una causa diferente a la explicada en el artículo.<br /><br /> Un ingeniero de soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] también puede utilizar el código de estado de un error para localizar la ubicación del código fuente donde se ha generado el código de error. Esta información puede proporcionar ideas adicionales sobre cómo diagnosticar el problema.|  
|Nombre del procedimiento|Nombre del procedimiento almacenado o desencadenador en que se ha producido el error.|  
|Número de línea|Indica qué instrucción de un lote, procedimiento almacenado, desencadenador o función ha generado el error.|  
  
 Todos los mensajes de error (del sistema o definidos por el usuario) de una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] se encuentran en la vista de catálogo **sys.messages** . Puede utilizar la instrucción RAISERROR para devolver a una aplicación errores definidos por el usuario.  
  
 Todas las API de base de datos, como el espacio de nombres [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] **SQLClient** , Objetos de datos ActiveX (ADO), OLE DB y Conectividad abierta de bases de datos (ODBC), notifican los atributos de error básicos. Esta información incluye el número de error y la cadena del mensaje. No obstante, no todas las API informan de los demás atributos de error.  
  
 La información sobre un error que se produce en el ámbito del bloque TRY de una construcción TRY…CATCH se puede obtener en código [!INCLUDE[tsql](../../includes/tsql-md.md)] utilizando funciones como ERROR_LINE, ERROR_MESSAGE, ERROR_NUMBER, ERROR_PROCEDURE, ERROR_SEVERITY y ERROR_STATE en el ámbito del bloque CATCH asociado. Para obtener más información, vea [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md).  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se envía una consulta a la vista de catálogo `sys.messages` en la que se solicita que devuelva una lista de todos los mensajes de error del sistema y definidos por el usuario en [!INCLUDE[ssDE](../../includes/ssde-md.md)] que tengan texto en inglés (`1033`).  
  
```  
SELECT  
    message_id,  
    language_id,  
    severity,  
    is_event_logged,  
    text  
  FROM sys.messages  
  WHERE language_id = 1033;  
```  
  
 Para obtener más información, vea [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md).  
  
## <a name="see-also"></a>Ver también  
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR &#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)   
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [ERROR_LINE &#40;Transact-SQL&#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_NUMBER &#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY &#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE &#40;Transact-SQL&#41;](../../t-sql/functions/error-state-transact-sql.md)  
  
  
