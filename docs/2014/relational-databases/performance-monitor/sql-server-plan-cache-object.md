---
title: Plan Cache (objeto de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Plan Cache object
- SQLServer:Plan Cache
ms.assetid: 225e2b02-8d2f-4f29-9eba-f5847c36ea99
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e24c072897a46d8a5b3add713f94a84e12a642b7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48190795"
---
# <a name="sql-server-plan-cache-object"></a>Plan Cache (objeto de SQL Server)
  El objeto **Plan Cache** proporciona contadores para supervisar la forma en que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza la memoria para almacenar objetos tales como procedimientos almacenados, instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] ad hoc y preparadas, y desencadenadores. Se pueden supervisar simultáneamente múltiples instancias del objeto **Plan Cache** ; cada instancia representa un tipo distinto de plan para supervisar.  
  
 En esta tabla se describen los contadores de **SQLServer:Plan Cache**.  
  
|Contadores de Plan Cache de SQL Server|Descripción|  
|------------------------------------|-----------------|  
|**Frecuencia de aciertos de caché**|Proporción entre los aciertos de caché y las búsquedas.|  
|**Recuentos de objetos de caché**|Número de objetos de caché que hay en la caché.|  
|**Páginas de caché**|Número de páginas de 8 KB utilizadas por los objetos de caché.|  
|**Objetos de caché en uso**|Número de objetos de caché que se están utilizando.|  
  
 Cada contador del objeto contiene las instancias siguientes:  
  
|Instancia de Plan Cache|Descripción|  
|-------------------------|-----------------|  
|**_Total**|Información para todos los tipos de instancias de caché.|  
|**Planes Sql**|Planes de consultas creados a partir de consultas [!INCLUDE[tsql](../../includes/tsql-md.md)] ad hoc, incluidas las consultas con parámetros, o a partir de instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] preparadas mediante **sp_prepare** o **sp_cursorprepare**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] almacena en caché los planes para las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] ad hoc para su uso posterior si la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] idéntica se ejecuta más tarde. Las consultas con parámetros de usuario (aunque no se hayan preparado de manera explícita) también se supervisan como planes SQL preparados.|  
|**Planes de objeto**|Planes de consultas que se generan al crear un procedimiento almacenado, una función o un desencadenador.|  
|**Árboles enlazados**|Árboles normalizados de vistas, reglas, columnas calculadas y restricciones de comprobación.|  
|**Procedimientos almacenados extendidos**|Información de catálogo para los procedimientos almacenados extendidos.|  
|**Tablas temporales y variables de tabla**|Información de caché relacionada con las tablas temporales y las variables de tabla.|  
  
## <a name="see-also"></a>Vea también  
 [Opciones de configuración de memoria del servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md)   
 [Buffer Manager (objeto de SQL Server)](sql-server-buffer-manager-object.md)   
 [Supervisar el uso de recursos&#40;Monitor de sistema&#41;](monitor-resource-usage-system-monitor.md)  
  
  
