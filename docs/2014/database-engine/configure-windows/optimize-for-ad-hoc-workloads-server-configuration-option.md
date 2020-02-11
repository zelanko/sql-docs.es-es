---
title: optimize for ad hoc workloads (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- optimize for ad hoc workloads option
ms.assetid: 0972e028-3a8e-454b-a186-e814a1d431f2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7edf279b49374823c9083005be9b8d047b003f62
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62781441"
---
# <a name="optimize-for-ad-hoc-workloads-server-configuration-option"></a>optimize for ad hoc workloads (opción de configuración del servidor)
  La opción **Optimizar para cargas de trabajo ad hoc** se utiliza para mejorar la eficiencia de la memoria caché del plan para cargas de trabajo que contienen muchos lotes ad hoc de uso único. Cuando esta opción está establecida en 1, [!INCLUDE[ssDE](../../includes/ssde-md.md)] almacena un pequeño código auxiliar del plan compilado en la memoria caché del plan al compilar un lote por primera vez, en lugar del plan compilado completo. Esto ayuda a disminuir la demanda de memoria al impedir que la memoria caché del plan se llene de planes compilados que no se reutilizan.  
  
 El código auxiliar del plan compilado permite que [!INCLUDE[ssDE](../../includes/ssde-md.md)] reconozca que este lote ad hoc se ha compilado antes, pero que solo se ha almacenado un código auxiliar del plan compilado, de modo que cuando se invoca de nuevo este lote (compilado o ejecutado), [!INCLUDE[ssDE](../../includes/ssde-md.md)] compila el lote, quita de la memoria caché del plan el código auxiliar del plan compilado y agrega el plan compilado completo a la memoria caché del plan.  
  
 Establecer la opción **Optimizar para cargas de trabajo ad hoc** en 1 afecta solo a los planes nuevos; los planes que ya están en la memoria caché del plan no resultan afectados.  
  
 El código auxiliar del plan compilado es uno de los elementos cacheobjtypes mostrados por la vista de catálogo sys.dm_exec_cached_plans. Tiene un identificador de sql e identificador del plan único. El código auxiliar del plan compilado no tiene un plan de ejecución asociado a él por lo que, al consultar el identificador del plan, no se devolverá un plan de presentación XML.  
  
 La marca de seguimiento 8032 revierte los parámetros de límite de la memoria caché al valor [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] de RTM que en general permite que las memorias caché sean mayores. Use esta opción cuando las entradas de caché reutilizadas con frecuencia no quepan en la caché y cuando la *opción de configuración del servidor optimizar para cargas de trabajo ad hoc* no haya podido resolver el problema con la caché del plan.  
  
> [!WARNING]  
>  La marca de seguimiento 8032 puede ocasionar la degradación del rendimiento si las memorias caché grandes suponen que haya menos memoria disponible para otros consumidores de memoria, como el grupo de búferes.  
  
## <a name="see-also"></a>Consulte también  
 [sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)  
  
  
