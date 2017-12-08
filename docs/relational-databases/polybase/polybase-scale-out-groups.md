---
title: Grupos de escalado horizontal de PolyBase | Microsoft Docs
ms.custom: 
ms.date: 05/24/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: polybase
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine-polybase
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- PolyBase
- PolyBase, scale-out groups
- scale-out PolyBase
ms.assetid: c7810135-4d63-4161-93ab-0e75e9d10ab5
caps.latest.revision: "20"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: d235f0af092b5780686abbe2b8d191f04547fd6a
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="polybase-scale-out-groups"></a>Grupos de escalado horizontal de PolyBase
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Una instancia de SQL Server independiente con PolyBase puede convertirse en un cuello de botella de rendimiento cuando se trabaja con grandes conjuntos de datos en Hadoop o Azure Blob Storage. La característica de grupos de PolyBase permite crear un clúster de instancias de SQL Server para procesar grandes conjuntos de datos a partir de orígenes de datos externos, como Hadoop o Almacenamiento de blobs de Azure, en un modo de escalado horizontal para mejorar el rendimiento de las consultas.  
  
 Vea [Introducción a PolyBase](../../relational-databases/polybase/get-started-with-polybase.md) y [Guía de PolyBase](../../relational-databases/polybase/polybase-guide.md).  
  
 ![Grupos de escalado horizontal de PolyBase](../../relational-databases/polybase/media/polybase-scale-out-groups.png "Grupos de escalado horizontal de PolyBase")  
  
## <a name="overview"></a>Información general  
  
### <a name="head-node"></a>Nodo principal  
 El nodo principal contiene la instancia de SQL Server a la que se envían las consultas PolyBase. Cada grupo de PolyBase solo puede tener un nodo principal. Un nodo principal es un grupo lógico del motor de base de datos de SQL, el motor de PolyBase y el servicio de movimiento de datos de PolyBase de la instancia de SQL Server.  
  
### <a name="compute-node"></a>Nodo de ejecución  
 Un nodo de ejecución contiene la instancia de SQL Server que ayuda a escalar horizontalmente el procesamiento de las consultas de los datos externos. Un nodo de ejecución es un grupo lógico de SQL Server y el servicio de movimiento de datos de PolyBase de la instancia de SQL Server. Un grupo de PolyBase puede tener varios nodos de ejecución.  
  
### <a name="distributed-query-processing"></a>Procesamiento de consultas distribuidas  
 Las consultas de PolyBase se envían a SQL Server en el nodo principal. La parte de la consulta que hace referencia a las tablas externas se entregan al motor de PolyBase.  
  
 El motor de PolyBase es el componente principal que está detrás de las consultas de PolyBase. Analiza la consulta en los datos externos, genera el plan de consulta y distribuye el trabajo al servicio de movimiento de datos de los nodos de ejecución para ejecutarlos. Tras finalizar el trabajo, recibe los resultados de los nodos de ejecución y los envía a SQL Server para procesarlos y devolverlos al cliente.  
  
 El servicio de movimiento de datos de PolyBase recibe instrucciones del motor de PolyBase y transfiere los datos entre HDFS y SQL Server, y entre las instancias de SQL Server de los nodos principal y de ejecución.  
  
### <a name="editions-availability"></a>Disponibilidad de ediciones  
 Después de instalar SQL Server, la instancia puede designarse como nodo principal o de ejecución.  La elección dependerá de qué versión de SQL Server PolyBase se esté ejecutando. En una instalación de Enterprise Edition, la instancia se puede designar como nodo principal o de ejecución. En Standard Edition, la instancia solo puede designarse como nodo de ejecución.  
  
## <a name="to-configure-a-polybase-group"></a>Pasos para configurar un grupo de PolyBase  
  
### <a name="prerequisites"></a>Requisitos previos  
  
-   Cualquier número de máquinas en el mismo dominio  
  
-   Una cuenta de usuario de dominio para ejecutar los servicios de PolyBase  
  
### <a name="steps"></a>Pasos  
  
1.  Instale SQL Server con PolyBase en cualquier número de máquinas.  
  
2.  Seleccione una instancia de SQL Server como nodo principal. Solo se puede designar un nodo principal en una instancia de SQL Server Enterprise.  
  
3.  Agregue las instancias de SQL Server restantes como nodos de ejecución usando [sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md).  
  
4.  Supervise los nodos en el grupo con [sys.dm_exec_compute_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md).  
  
5.  Opcional. Quite un nodo de ejecución con [sp_polybase_leave_group &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-leave-group.md).  
  
## <a name="example-walk-through"></a>Tutorial de ejemplo  
 En este tutorial se muestran los pasos necesarios para configurar un grupo de PolyBase con:  
  
1.  Dos máquinas en el dominio *PQTH4A* . Los nombres de las máquinas son:  
  
    -   PQTH4A-CMP01  
  
    -   PQTH4A-CMP02  
  
2.  Cuenta de dominio: *PQTH4A\PolybaseUse*r  
  
#### <a name="step-1-install-sql-server-with-polybase-on-all-machines"></a>Paso 1: instalación de SQL Server con PolyBase en todas las máquinas  
  
1.  Ejecute setup.exe.  
  
2.  En la página Selección de características, elija **PolyBase Query Service for External Data**(Servicio de consultas PolyBase para datos externos).  
  
3.  En la página Configuración del servidor, use la **cuenta de dominio** PQTH4A\PolybaseUser para el motor y el servicio de movimiento de datos de SQL Server PolyBase.  
  
4.  En la página PolyBase Configuration (Configuración de PolyBase), seleccione la opción **Use the SQL Server instance as part of a PolyBase scale-out group**(Usar la instancia de SQL Server como parte de un grupo de escalado horizontal de PolyBase). Se abrirá el firewall para permitir las conexiones entrantes a los servicios de PolyBase.  
  
5.  Una vez completada la instalación, ejecute **services.msc**. Compruebe que están ejecutando SQL Server, el motor de PolyBase y el servicio de movimiento de datos de PolyBase.  
  
     ![Servicios PolyBase](../../relational-databases/polybase/media/polybase-services.png "Servicios PolyBase")  
  
#### <a name="step-2-select-one-sql-server-as-head-node"></a>Paso 2: selección de una instancia de SQL Server como nodo principal  
  
-   Una vez completada la instalación, las dos máquinas pueden funcionar como nodos principales del grupo de PolyBase. En este ejemplo, elegiremos "MSSQLSERVER" de PQTH4A-CMP01 como nodo principal.  
  
#### <a name="step-3-add-other-sql-server-instances-as-compute-nodes"></a>Paso 3: adición de otras instancias de SQL Server como nodos de ejecución  
  
1.  Conéctese a SQL Server en PQTH4A-CMP02.  
  
2.  Ejecute el procedimiento almacenado [sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md).  
  
    ```  
    -- Enter head node details:   
    -- head node machine name, head node dms control channel port, head node sql server name  
    EXEC sp_polybase_join_group 'PQTH4A-CMP01', 16450, 'MSSQLSERVER';  
  
    ```  
  
3.  Ejecute services.msc en el nodo de ejecución (PQTH4A-CMP02).  
  
4.  Apague el motor de PolyBase y reinicie el servicio de movimiento de datos de PolyBase.  
  
#### <a name="optional-remove-a-compute-node"></a>Opcional: eliminación un nodo de ejecución  
  
1.  Conéctese al nodo de ejecución de SQL Server (PQTH4A-CMP02).  
  
2.  Ejecute el procedimiento almacenado sp_polybase_leave_group.  
  
    ```  
    EXEC sp_polybase_leave_group;  
    ```  
  
3.  Ejecute services.msc en el nodo de ejecución que se va a eliminar (PQTH4A-CMP02).  
  
4.  Inicie el motor de PolyBase. Reinicie el servicio de movimiento de datos de PolyBase.  
  
5.  Compruebe que el nodo se ha eliminado ejecutando el DMV sys.dm_exec_compute_nodes en PQTH4A-CMP01. Ahora, PQTH4A-CMP02 funcionará como nodo principal independiente.  
  
## <a name="next-steps"></a>Pasos siguientes  
 Para solucionar problemas, consulte [PolyBase troubleshooting with dynamic management views](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80).  
  
## <a name="see-also"></a>Vea también  
 [Introducción a PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)   
 [Guía de PolyBase](../../relational-databases/polybase/polybase-guide.md)   
 [Configuración de PolyBase &#40;Transact-SQL&#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)  
  
  
