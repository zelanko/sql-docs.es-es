---
title: "Cambiar el modo de compatibilidad de la base de datos y usar el almacén de consultas | Microsoft Docs"
ms.custom: 
ms.date: 07/21/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: sql
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- query plans [SQL Server], migrating
- upgrading SQL Server, migrating query plans
- plan guides [SQL Server], migrating query plans
ms.assetid: 7e02a137-6867-4f6a-a45a-2b02674f7e65
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6fa6e9e16be729fba7334b26b130c8e22525e479
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="change-the-database-compatibility-mode-and-use-the-query-store"></a>Cambiar el modo de compatibilidad de la base de datos y usar el almacén de consultas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], algunos cambios solo se habilitan una vez que se ha cambiado el [nivel de compatibilidad de la base de datos](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md). Esto se realiza por varias razones:  
  
- Ya que la actualización es una operación unidireccional (no se puede degradar el formato de archivo), hay un valor en la separación de la habilitación de características nuevas para una operación independiente dentro de la base de datos. Es posible revertir un valor a un nivel de compatibilidad de la base de datos anterior.  El nuevo modelo reduce el número de pasos que hay que realizar durante una ventana de interrupción.  
  
- Los cambios en el procesador de consultas pueden tener efectos complejos. Aun cuando un cambio "bueno" en el sistema puede ser positivo para la mayoría de las cargas de trabajo, para otras podría causar una regresión inaceptable en una consulta importante. Separar esta lógica del proceso de actualización permite que las características, como el Almacén de consultas, mitiguen las regresiones de elección del plan rápidamente o incluso las eviten completamente en servidores de producción.  
  
> [!IMPORTANT]  
> Si el nivel de compatibilidad de una base de datos de usuario era 100 o superior antes de la actualización, permanece igual después de la misma. Si el nivel de compatibilidad de una base de datos de usuario era 90 antes de la actualización, en la base de datos actualizada el nivel de compatibilidad se establece en 100, que es el nivel de compatibilidad mínimo admitido en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Los niveles de compatibilidad de las bases de datos tempdb, model, msdb y Resource quedan establecidos en el nivel de compatibilidad actual después de la actualización.
> La base de datos del sistema maestra conserva el nivel de compatibilidad que tenía antes de la actualización. 
  
El proceso de actualización para habilitar la nueva funcionalidad del procesador de consultas está relacionado con el modelo de servicio posterior a la versión del producto.  Algunas de esas correcciones se publican bajo la [marca de seguimiento 4199](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md#4199).  Los clientes que necesitan correcciones pueden participar en esas correcciones sin causar regresiones inesperadas para otros clientes. El modelo de mantenimiento posterior a la versión para las revisiones del procesador de consultas se documenta [aquí](http://support.microsoft.com/kb/974006). A partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], moverse a un nuevo nivel de compatibilidad implica que ya no se necesita la marca de seguimiento 4199, puesto que esas correcciones ya están habilitadas de forma predeterminada en el nivel de compatibilidad más reciente. Por lo tanto, como parte del proceso de actualización, es importante validar que 4199 no está habilitado una vez que se completa el proceso de actualización.  

> [!NOTE]
> Sin embargo, la marca de seguimiento 4199 sigue resultando necesaria para habilitar cualquier nueva corrección del procesador de consultas publicada después de RTM, si procede.
  
El flujo de trabajo recomendado para actualizar el procesador de consultas a la versión más reciente del código está documentado en la sección [Mantener la estabilidad del rendimiento al actualizar a una versión más reciente de SQL Server de Escenarios de uso del Almacén de consultas](../../relational-databases/performance/query-store-usage-scenarios.md#CEUpgrade), tal y como se muestra abajo.  
  
![consultaDeAlmacénDeUso5](../../relational-databases/performance/media/query-store-usage-5.png "consultaDeAlmacénDeUso5") 
 
## <a name="see-also"></a>Ver también  
 [Ver o cambiar el nivel de compatibilidad de una base de datos](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)  
 [Escenarios de uso del Almacén de consultas](../../relational-databases/performance/query-store-usage-scenarios.md) 
  
