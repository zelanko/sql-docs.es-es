---
title: Mejora de los grupos de escalado horizontal de PolyBase en Windows | Microsoft Docs
ms.date: 04/23/2019
ms.prod: sql
ms.technology: polybase
ms.topic: tutorial
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: aboke
monikerRange: '>= sql-server-2016 || =sqlallproducts-allversions'
ms.openlocfilehash: eee05e9c9ba129b660048797dd8894c0d611449e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041156"
---
# <a name="improve-polybase-scale-out-groups-on-windows"></a>Mejora de los grupos de escalado horizontal de PolyBase en Windows

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se describe cómo configurar un [grupo de escalado horizontal de PolyBase](polybase-scale-out-groups.md) en Windows. Esto crea un clúster de instancias de SQL Server para procesar grandes conjuntos de datos a partir de orígenes de datos externos, como Hadoop o Azure Blob Storage, en un modo de escalado horizontal para mejorar el rendimiento de las consultas.

## <a name="prerequisites"></a>Prerequisites
  
- Más de una máquina en el mismo dominio  
  
- Una cuenta de usuario de dominio para ejecutar los servicios de PolyBase  
  
## <a name="process-overview"></a>Información general del proceso

Los pasos siguientes resumen el proceso de creación de un grupo de escalado horizontal de PolyBase. La siguiente sección proporciona una descripción más detallada de cada paso.
  
1. Instale la misma versión de SQL Server con PolyBase en cualquier número de máquinas.
  
2. Seleccione una instancia de SQL Server como nodo principal. Solo se puede designar un nodo principal en una instancia de SQL Server Enterprise.
  
3. Agregue las instancias de SQL Server restantes como nodos de ejecución usando [sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md).

4. Supervise los nodos en el grupo con [sys.dm_exec_compute_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md).

5. Opcional. Quite un nodo de ejecución con [sp_polybase_leave_group &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-leave-group.md).

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="example-walk-through"></a>Tutorial de ejemplo

En este tutorial se muestran los pasos necesarios para configurar un grupo de PolyBase con:  
  
1. Dos máquinas en el dominio *PQTH4A* . Los nombres de las máquinas son:  
  
   - PQTH4A-CMP01  
  
   - PQTH4A-CMP02  
  
2. Cuenta de dominio: *PQTH4A\PolyBaseUse*r  

## <a name="install-sql-server-with-polybase-on-all-machines"></a>Instalación de SQL Server con PolyBase en todas las máquinas

1. Ejecute setup.exe.
  
2. En la página Selección de características, elija **PolyBase Query Service for External Data** (Servicio de consultas PolyBase para datos externos).
  
3. En la página Configuración del servidor, use la **cuenta de dominio** PQTH4A\PolyBaseUser para el motor y el servicio de movimiento de datos de SQL Server PolyBase.
  
4. En la página PolyBase Configuration (Configuración de PolyBase), seleccione la opción **Use the SQL Server instance as part of a PolyBase scale-out group**(Usar la instancia de SQL Server como parte de un grupo de escalado horizontal de PolyBase). Se abrirá el firewall para permitir las conexiones entrantes a los servicios de PolyBase.
  
5. Una vez completada la instalación, ejecute **services.msc**. Compruebe que están ejecutando SQL Server, el motor de PolyBase y el servicio de movimiento de datos de PolyBase.
  
   ![Servicios PolyBase](../../relational-databases/polybase/media/polybase-services.png "Servicios PolyBase")  
  
## <a name="select-one-sql-server-as-head-node"></a>Seleccione una instancia de SQL Server como nodo principal.  
  
Una vez completada la instalación, las dos máquinas pueden funcionar como nodos principales del grupo de PolyBase. En este ejemplo, elegiremos "MSSQLSERVER" de PQTH4A-CMP01 como nodo principal.
  
## <a name="add-other-sql-server-instances-as-compute-nodes"></a>Adición de otras instancias de SQL Server como nodos de ejecución  
  
1. Conéctese a SQL Server en PQTH4A-CMP02.
  
2. Ejecute el procedimiento almacenado [sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md).

   ```sql
   -- Enter head node details:
   -- head node machine name, head node dms control channel port, head node sql server name  
    EXEC sp_polybase_join_group 'PQTH4A-CMP01', 16450, 'MSSQLSERVER';
   ```  

3. Ejecute services.msc en el nodo de ejecución (PQTH4A-CMP02).
  
4. Apague el motor de PolyBase y reinicie el servicio de movimiento de datos de PolyBase.
  
## <a name="optional-remove-a-compute-node"></a>Opcional: eliminación de un nodo de ejecución.  
  
1. Conéctese al nodo de ejecución de SQL Server (PQTH4A-CMP02).
  
2. Ejecute el procedimiento almacenado sp_polybase_leave_group.
  
    ```sql  
    EXEC sp_polybase_leave_group;  
    ```  
  
3. Ejecute services.msc en el nodo de ejecución que se va a eliminar (PQTH4A-CMP02).
  
4. Inicie el motor de PolyBase. Reinicie el servicio de movimiento de datos de PolyBase.
  
5. Compruebe que el nodo se ha eliminado ejecutando el DMV sys.dm_exec_compute_nodes en PQTH4A-CMP01. Ahora, PQTH4A-CMP02 funcionará como nodo principal independiente.  
  
## <a name="next-steps"></a>Pasos siguientes  

Para solucionar problemas, consulte [PolyBase troubleshooting with dynamic management views](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80).
  
Para obtener más información sobre PolyBase, consulte la [Guía de PolyBase](../../relational-databases/polybase/polybase-guide.md).
