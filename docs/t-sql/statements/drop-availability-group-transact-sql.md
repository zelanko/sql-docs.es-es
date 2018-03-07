---
title: Quitar grupo de disponibilidad (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_AVAILABILITY_GROUP_TSQL
- DROP AVAILABILITY GROUP
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], removing
- Availability Groups [SQL Server], Transact-SQL statements
- DROP AVAILABILITY GROUP statement
- Availability Groups [SQL Server], dropping
ms.assetid: c1600289-c990-454a-b279-dba0ebd5d63e
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 82fdb4b104a0be0aa0d6469ccdd23f361f55618b
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="drop-availability-group-transact-sql"></a>DROP AVAILABILITY GROUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Quita el grupo de disponibilidad especificado y todas sus réplicas. Si una instancia del servidor que hospeda una de las réplicas de disponibilidad está sin conexión al eliminar un grupo de disponibilidad, después de ponerse en línea, la instancia del servidor quitará la réplica de disponibilidad local. La acción de quitar un grupo de disponibilidad también elimina el agente de escucha del grupo de disponibilidad asociado, si hay alguno.  
  
> [!IMPORTANT]  
>  Si es posible, quite el grupo de disponibilidad solo mientras esté conectado a la instancia de servidor que hospeda la réplica principal. Cuando el grupo de disponibilidad se quita de la réplica principal, se permiten cambios en las bases de datos principales anteriores (sin protección de alta disponibilidad). Eliminar un grupo de disponibilidad de una réplica secundaria deja la réplica principal en el **RESTORING** estado y los cambios no se permiten en las bases de datos.  
  
 Para obtener información sobre las formas alternativas para quitar un grupo de disponibilidad, consulte [quitar un grupo de disponibilidad &#40; SQL Server &#41; ](../../database-engine/availability-groups/windows/remove-an-availability-group-sql-server.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DROP AVAILABILITY GROUP group_name   
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *group_name*  
 Especifica el nombre del grupo de disponibilidad que se va a quitar.  
  
## <a name="limitations-and-recommendations"></a>Limitaciones y recomendaciones  
  
-   Ejecutar **DROP AVAILABILITY GROUP** requiere que la característica de grupos de disponibilidad AlwaysOn está habilitada en la instancia del servidor. Para obtener más información, vea [Habilitar y deshabilitar grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md).  
  
-   **DROP AVAILABILITY GROUP** no se puede ejecutar como parte de los lotes o dentro de las transacciones. Además, no se admiten expresiones ni variables.  
  
-   Puede quitar un grupo de disponibilidad de cualquier nodo de clústeres de conmutación por error de Windows Server (WSFC) que posea las credenciales de seguridad correctas para el grupo de disponibilidad. Esto permite eliminar un grupo de disponibilidad cuando ninguna de sus réplicas de disponibilidad permanece.  
  
    > [!IMPORTANT]  
    >  Evite quitar un grupo de disponibilidad cuando el clúster de Clústeres de conmutación por error de Windows Server (WSFC) no tiene quórum. Si debe quitar un grupo de disponibilidad mientras el clúster no tiene quórum, el grupo de disponibilidad de metadatos que se almacena en el clúster no se quita. Cuando el clúster recupere el quórum, necesitará volver a quitar el grupo de disponibilidad para quitarlo del clúster de WSFC.  
  
-   En una réplica secundaria, **DROP AVAILABILITY GROUP** solo debe usarse en caso de emergencia. Esto se debe a que al quitar un grupo de disponibilidad este se queda sin conexión. Si quita el grupo de disponibilidad de una réplica secundaria, la réplica principal no puede determinar si la **sin conexión** estado se ha producido debido a la pérdida de quórum, una conmutación por error forzada, o un **DROP AVAILABILITY GROUP**comando. La réplica principal pasa a la **RESTORING** para evitar una posible situación de cerebro dividida. Para obtener más información, vea [How It Works: DROP AVAILABILITY GROUP Behaviors (Cómo funciona: comportamientos de DROP AVAILABILITY GROUP)](http://blogs.msdn.com/b/psssql/archive/2012/06/13/how-it-works-drop-availability-group-behaviors.aspx) (blog de los ingenieros de SQL Server de CSS).  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permissions  
 Requiere **ALTER AVAILABILITY GROUP** permiso en el grupo de disponibilidad, **CONTROL AVAILABILITY GROUP** permiso, **ALTER ANY AVAILABILITY GROUP** permiso, o **CONTROL SERVER** permiso. Para quitar un grupo de disponibilidad que no está hospedado por la instancia del servidor local debe **CONTROL SERVER** permiso o **CONTROL** permiso en ese grupo de disponibilidad.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se quita el grupo de disponibilidad `AccountsAG`.  
  
```  
DROP AVAILABILITY GROUP AccountsAG;  
```  
  
##  <a name="RelatedContent"></a> Contenido relacionado  
  
-   [How It Works: DROP AVAILABILITY GROUP Behaviors (Cómo funciona: comportamientos de DROP AVAILABILITY GROUP)](http://blogs.msdn.com/b/psssql/archive/2012/06/13/how-it-works-drop-availability-group-behaviors.aspx) (blog de los ingenieros de SQL Server de CSS)  
  
## <a name="see-also"></a>Vea también  
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)   
 [Crear grupo de disponibilidad &#40; Transact-SQL &#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [Quitar un grupo de disponibilidad &#40; SQL Server &#41;](../../database-engine/availability-groups/windows/remove-an-availability-group-sql-server.md)  
  
  
