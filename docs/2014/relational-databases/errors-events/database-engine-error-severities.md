---
title: Gravedad de los errores del Motor de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- user-defined error messages [SQL Server]
- severity levels [SQL Server]
- retrieving error severity
- errors [SQL Server], severity
- TRY...CATCH [SQL Server]
ms.assetid: 3e7f5925-6edd-42e1-bf17-f7deb03993a7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9de758c6a54ca1993efc8873a02293331a129b33
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62870983"
---
# <a name="database-engine-error-severities"></a>Niveles de gravedad de error del motor de base de datos
  Cuando el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]muestra un error, la gravedad del error indica el tipo de problema detectado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="levels-of-severity"></a>Niveles de gravedad  
 En la siguiente tabla se enumeran y describen los niveles de gravedad de los errores mostrados por el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
|Nivel de gravedad|Descripción|  
|--------------------|-----------------|  
|0-9|Mensajes informativos que devuelven información de estado o informan sobre errores que no son graves. El [!INCLUDE[ssDE](../../includes/ssde-md.md)] no muestra errores del sistema con gravedades de 0 a 9.|  
|10|Mensajes informativos que devuelven información de estado o informan sobre errores que no son graves. Por razones de compatibilidad, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] convierte la gravedad 10 en gravedad 0 antes de devolver la información de errores a la aplicación que hace la llamada.|  
|11-16|Indica errores que pueden ser corregidos por el usuario.|  
|11|Indica que un objeto o una entidad determinados no existen.|  
|12|Una gravedad especial para consultas que no utilizan bloqueo debido a sugerencias de consulta especiales. En algunos casos, las operaciones de lectura realizadas por estas instrucciones podrían producir datos incoherentes, ya que no se adoptan bloqueos para garantizar la coherencia.|  
|13|Indica errores de interbloqueo de transacciones.|  
|14|Indica errores relacionados con la seguridad, como es el caso de permisos denegados.|  
|15|Indica errores de sintaxis en el comando [!INCLUDE[tsql](../../includes/tsql-md.md)] .|  
|16|Indica errores generales que pueden ser corregidos por el usuario.|  
|17-19|Indica errores de software que no pueden ser corregidos por el usuario. Informe al administrador del sistema sobre el problema.|  
|17|Indica que la instrucción ha hecho que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se quede sin recursos (como, por ejemplo, memoria, bloqueos o espacio en disco para la base de datos) o ha superado alguno de los límites establecidos por el administrador del sistema.|  
|18|Indica un problema en el software de [!INCLUDE[ssDE](../../includes/ssde-md.md)] pero la instrucción completa su ejecución y la conexión con la instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] se mantiene. El administrador del sistema debe ser informado cada vez que se produce un mensaje con un nivel de gravedad 18.|  
|19|Indica que se ha superado un límite de [!INCLUDE[ssDE](../../includes/ssde-md.md)] no configurable y el proceso por lotes actual ha finalizado. Los mensajes de error con nivel de gravedad 19 o superior detienen la ejecución del lote actual. Los errores de nivel de gravedad 19 son poco frecuentes y deben ser corregidos por el administrador del sistema o por el proveedor principal de asistencia técnica. Póngase en contacto con el administrador del sistema cuando se produzca un mensaje con nivel de gravedad 19. Los mensajes de error con nivel de gravedad entre 19 y 25 se escriben en el registro de errores.|  
|20-24|Indica problemas del sistema y son errores irrecuperables, lo que significa que ya no está en ejecución la tarea de [!INCLUDE[ssDE](../../includes/ssde-md.md)] que esté ejecutando una instrucción o lote. La tarea registra información sobre lo acontecido y, a continuación, finaliza. En la mayoría de los casos, puede que también finalice la conexión de la aplicación a la instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Si esto ocurre, dependiendo del problema, la aplicación podría no conseguir volver a conectarse.<br /><br /> Los mensajes de error incluidos en este intervalo pueden afectar a todos los procesos que tienen acceso a los datos de la misma base de datos y pueden indicar que una base de datos u objeto está dañado. Los mensajes de error con nivel de gravedad entre 19 y 24 se escriben en el registro de errores.|  
|20|Indica que una instrucción ha encontrado un problema. Puesto que el problema ha afectado solo a la tarea actual, no es probable que la propia base de datos haya sido dañada.|  
|21|Indica que se ha encontrado un problema que afecta a todas las tareas de la base de datos actual, pero es poco probable que se haya dañado la base de datos.|  
|22|Indica que la tabla o índice especificado en el mensaje ha sido dañado por un problema de software o hardware.<br /><br /> Los errores de nivel de gravedad 22 se producen en raras ocasiones. Si se produce uno de ellos, ejecute DBCC CHECKDB para determinar si hay otros objetos de la base de datos dañados. Es posible que el problema se encuentre solo en la caché del búfer y no en el propio disco. Si es así, al reiniciar la instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] se corregirá el problema. Para seguir trabajando, deberá volver a conectarse a la instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)]; en caso contrario, utilice DBCC para solucionar el problema. En algunas ocasiones, puede que tenga que restaurar la base de datos.<br /><br /> Si al reiniciar la instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] no se corrige el problema, el problema estará en el disco. Algunas veces se puede resolver si se destruye el objeto especificado en el mensaje de error. Por ejemplo, si el mensaje le indica que la instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] ha encontrado una fila con longitud 0 en un índice no clúster, elimine el índice y vuelva a generarlo.|  
|23|Indica que se sospecha de la integridad de toda la base de datos debido al daño causado por un problema de hardware o software.<br /><br /> Los errores de nivel de gravedad 23 se producen en raras ocasiones. Si se produce alguno, ejecute DBCC CHECKDB para determinar la magnitud de los daños. Es posible que el problema se encuentre solo en la caché y no en el propio disco. Si es así, al reiniciar la instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] se corregirá el problema. Para seguir trabajando, deberá volver a conectarse a la instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)]; en caso contrario, utilice DBCC para solucionar el problema. En algunas ocasiones, puede que tenga que restaurar la base de datos.|  
|24|Indica un error en los medios. Puede que el administrador del sistema tenga que restaurar la base de datos. Puede que también tenga que llamar al distribuidor de hardware.|  
  
## <a name="user-defined-error-message-severity"></a>Gravedad de mensaje de error definida por el usuario  
 **sp_addmessage** se puede usar para agregar a la vista de catálogo **sys.messages** mensajes de error definidos por el usuario con niveles de gravedad de 1 a 25. Estos mensajes de error definidos por el usuario pueden ser utilizados por RAISERROR. Para obtener más información, vea [sp_addmessage &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmessage-transact-sql).  
  
 RAISERROR se puede utilizar para generar los mensajes del error definidos por el usuario con la gravedad comprendida entre 1 y 25. RAISERROR puede hacer referencia a un mensaje de error definido por el usuario almacenado en la vista de catálogo **sys.messages** o puede generar un mensaje dinámicamente. Si se usa el mensaje de error definido por el usuario de **sys.messages** mientras se genera un error, la gravedad especificada por RAISERROR reemplazará a la gravedad especificada en **sys.messages**. Para obtener más información, vea [RAISERROR &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/raiserror-transact-sql).  
  
## <a name="error-severity-and-trycatch"></a>Gravedad de error y TRY...CATCH  
 Una construcción TRY...CATCH detecta todos los errores de ejecución con una gravedad mayor de 10 que no finalizan la conexión de la base de datos.  
  
 Los errores con gravedad de 0 a 10 son mensajes informativos y no hacen que la ejecución salte desde el bloque CATCH de una construcción TRY...CATCH.  
  
 Los errores que finalizan la conexión de la base de datos, normalmente con una gravedad de 20 a 25, no son controlados por el bloque CATCH porque la ejecución se anula al finalizar la conexión.  
  
 Para obtener más información, vea [TRY...CATCH &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/try-catch-transact-sql).  
  
## <a name="retrieving-error-severity"></a>recuperar la gravedad del error  
 Se puede usar la función del sistema ERROR_SEVERITY para recuperar la gravedad del error que ha provocado la ejecución del bloque CATCH de una construcción TRY...CATCH. Si se le llama fuera del ámbito de un bloque CATCH, ERROR_SEVERITY devuelve el valor NULL. Para obtener más información, vea [ERROR_SEVERITY &#40;Transact-SQL&#41;](/sql/t-sql/functions/error-severity-transact-sql).  
  
## <a name="see-also"></a>Consulte también  
 [Descripción de errores del motor de base de datos](../native-client-ole-db-errors/errors.md)   
 [sys.messages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages)   
 [Funciones del sistema &#40;Transact-SQL&#41;](/sql/t-sql/functions/system-functions-transact-sql)   
 [TRY...CATCH &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/try-catch-transact-sql)  
  
  
