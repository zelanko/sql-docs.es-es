---
title: SQL Statistics (objeto de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:SQL Statistics
- SQL Statistics object
ms.assetid: da7dbb4b-f632-45a0-b1ab-c35cc2695c86
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 783c20de7f1ea23f41dcbc4fb645644bdaf5ad7d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63183079"
---
# <a name="sql-server-sql-statistics-object"></a>SQL Statistics (objeto de SQL Server)
  El objeto **SQLServer:SQL Statistics** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona contadores para supervisar la compilación y el tipo de solicitudes que se envían a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La supervisión del número de compilaciones y recompilaciones de consultas y el número de lotes que recibe una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona información acerca de la rapidez con la que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] procesa las consultas de usuarios y la eficacia con la que el optimizador de consultas las procesa.  
  
 La compilación constituye una parte significativa del intervalo de respuesta de una consulta. Para guardar el costo de compilación, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] guarda el plan de consulta compilado en una caché de consultas. El objetivo de la memoria caché es reducir la compilación al almacenar consultas compiladas para volver a utilizarlas posteriormente, lo que elimina la necesidad de volver a compilar las consultas cuando se ejecuten después. No obstante, se debe compilar cada consulta única al menos una vez. Las recompilaciones de consultas pueden deberse a los siguientes factores:  
  
-   Cambios de esquema, incluidos cambios básicos como agregar columnas o índices a una tabla, o bien cambios estadísticos como insertar o eliminar un número significativo de filas de una tabla.  
  
-   Cambios en el entorno (instrucción SET). Los cambios en la configuración de la sesión como ANSI_PADDING o ANSI_NULLS pueden hacer que se vuelva a compilar una consulta.  
  
 Para obtener más información sobre la parametrización simple y forzada, vea [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql).  
  
 Estos son los contadores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **SQL Statistics** .  
  
|Contadores de SQLServer:SQL Statistics|Descripción|  
|----------------------------------------|-----------------|  
|**Intentos de parametrización automática/seg.**|Número de intentos de parametrización automática por segundo. El número total deber ser la suma de las parametrizaciones automáticas seguras, no seguras y con errores. La parametrización automática tiene lugar cuando una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intenta parametrizar una solicitud de [!INCLUDE[tsql](../../../includes/tsql-md.md)] reemplazando algunos literales por parámetros, de forma que se posibilita la reutilización del plan de ejecución almacenado en caché resultante en varias solicitudes parecidas. Tenga en cuenta que las parametrizaciones automáticas también se denominan parametrizaciones simples en las versiones más recientes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Este contador no incluye las parametrizaciones forzadas.|  
|**Solicitudes de lotes/seg.**|Número de lotes de comandos de [!INCLUDE[tsql](../../../includes/tsql-md.md)] recibidos por segundo. Esta estadística se ve afectada por todas las restricciones (como E/S, número de usuarios, tamaño de la memoria caché, complejidad de las solicitudes, etc.). Un número alto de solicitudes de lotes significa un buen rendimiento.|  
|**Parametrizaciones automáticas con error/seg.**|Número de intentos de parametrización automática con error por segundo. Este número debería ser bajo. Tenga en cuenta que las parametrizaciones automáticas también se denominan parametrizaciones simples en versiones posteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**Parametrizaciones forzadas/seg.**|Número de parametrizaciones forzadas logradas por segundo.|  
|**Ejecuciones de planes correctos/seg**|Número de ejecuciones de planes por segundo en los que el plan de consulta se ha generado utilizando una guía de plan.|  
|**Ejecuciones de planes equivocados/seg**|Número de ejecuciones de planes por segundo en los que una guía de plan no se pudo aplicar al generar los planes. Se descartó la guía de plan y se utilizó la compilación normal para generar el plan ejecutado.|  
|**Parametrizaciones automáticas seguras/seg.**|Número de intentos de parametrización automática segura por segundo. El término "segura" se refiere a la determinación de que un plan de ejecución almacenado en caché puede compartirse entre varias instrucciones [!INCLUDE[tsql](../../../includes/tsql-md.md)] . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] realiza numerosos intentos de parametrización automática; algunos son seguros y otros no. Tenga en cuenta que las parametrizaciones automáticas también se denominan parametrizaciones simples en versiones posteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esto no incluye las parametrizaciones forzadas.|  
|**Velocidad de atención de SQL**|Número de atenciones por segundo. Una atención es una solicitud del cliente para finalizar la solicitud que se está ejecutando en ese momento.|  
|**Compilaciones SQL/seg.**|Número de compilaciones SQL por segundo. Indica el número de veces que se ha especificado la ruta de acceso al código de compilación. Incluye compilaciones causadas por recompilaciones de instrucciones en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cuando la actividad de usuarios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es estable, este valor permanece fijo.|  
|**Recompilaciones SQL/seg.**|Número de recompilaciones de instrucciones por segundo. Cuenta el número de veces que se desencadenan las recompilaciones de instrucciones. En general, es conveniente que el número de recompilaciones sea bajo.|  
|**Parametrizaciones automáticas no seguras/seg.**|Número de intentos de parametrización automática no segura por segundo. Por ejemplo, la consulta dispone de algunas características que impiden compartir el plan almacenado en caché. Estas parametrizaciones se designan como no seguras. Esta opción no cuenta el número de parametrizaciones forzadas.|  
  
## <a name="see-also"></a>Vea también  
 [Plan Cache (objeto de SQL Server)](sql-server-plan-cache-object.md)   
 [Supervisar el uso de recursos&#40;Monitor de sistema&#41;](monitor-resource-usage-system-monitor.md)  
  
  
