---
title: "DTC de clúster para grupos de disponibilidad de SQL Server 2016 | Microsoft Docs"
ms.custom: 
ms.date: 08/30/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a47c5005-20e3-4880-945c-9f78d311af7a
caps.latest.revision: 3
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: bf3445a7f28bc53b844946f66bc86712931d82e2
ms.contentlocale: es-es
ms.lasthandoff: 09/27/2017

---
# <a name="cluster-dtc-for-sql-server-2016-availability-groups"></a>DTC de clúster para grupos de disponibilidad de SQL Server 2016
En este tema se describen los requisitos y los pasos para agrupar en clústeres el servicio Microsoft DTC (Coordinador de transacciones distribuidas) para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Para obtener más información sobre las transacciones distribuidas y [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [Transacciones entre bases de datos y transacciones distribuidas para la creación de reflejo de la base de datos o grupos de disponibilidad AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md).

 ## <a name="checklist-preliminary-requirements"></a>Lista de comprobación: requisitos preliminares
||Tarea|Referencia|  
|------|-----------------|----------|  
|![Casilla](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Asegúrese de que todos los nodos, servicios y el grupo de disponibilidad se han configurado correctamente.|[Requisitos previos, restricciones y recomendaciones para Grupos de disponibilidad AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)|
|![Casilla](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Asegúrese de que se han cumplido los requisitos de DTC del grupo de disponibilidad.|[Transacciones entre bases de datos y transacciones distribuidas para la creación de reflejo de la base de datos o grupos de disponibilidad AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md)

## <a name="checklist-clustered-dtc-resource-dependencies"></a>Lista de comprobación: dependencias de recursos de DTC en clúster
||Tarea|Referencia|  
|------|-----------------|----------|  
|![Casilla](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Una unidad de almacenamiento compartido.|[Configuración de la unidad de almacenamiento compartido](https://msdn.microsoft.com/library/cc982358(v=bts.10).aspx). Considere la posibilidad de usar la letra de unidad **M**.|
|![Casilla](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Un recurso de nombre de red del DTC único.  El nombre se registrará como objeto de equipo del clúster en Active Directory.<br /><br />Asegúrese de que se cumple alguna de las siguientes condiciones:<br /><br />• El usuario que crea el recurso de nombre de red del DTC tiene el permiso para crear objetos de equipo en la unidad organizativa o el contenedor donde residirá el recurso de nombre de red del DTC.<br /><br />• Si el usuario no tiene el permiso para crear objetos de equipo, pida a un administrador de dominio que preconfigure un objeto de equipo del clúster para el recurso de nombre de red del DTC.|[Preconfiguración de objetos de equipo del clúster en Active Directory Domain Services](https://technet.microsoft.com/library/dn466519(v=ws.11).aspx)|
|![Casilla](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Una dirección IP estática disponible válida y la máscara de subred adecuada para esa dirección IP.||

## <a name="cluster-the-dtc-resource"></a>Agrupar en clústeres el recurso del DTC
Una vez que haya creado el recurso de grupo de disponibilidad, cree un recurso DTC agrupado y agréguelo al grupo de disponibilidad.  Encontrará un script de ejemplo en [Crear un DTC agrupado para un grupo de disponibilidad AlwaysOn](../../../database-engine/availability-groups/windows/create-clustered-dtc-for-an-always-on-availability-group.md).


## <a name="checklist-post-clustered-dtc-resource-configurations"></a>Lista de comprobación: publicación de configuraciones del recurso del DTC
||Tarea|Referencia|  
|------|-----------------|----------|  
|![Casilla](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Habilite el acceso de red de forma segura para el recurso del DTC en clúster.|[Habilitar el acceso de red de forma segura para MS DTC](https://technet.microsoft.com/library/cc753620(v=ws.10).aspx)|
|![Casilla](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Detenga y deshabilite el servicio DTC local.|[Configurar la forma en que se inicia un servicio](https://technet.microsoft.com/library/cc755249(v=ws.11).aspx)|
|![Casilla](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Reinicie el servicio SQL Server para cada instancia del grupo de disponibilidad.  Conmute por error el grupo de disponibilidad según sea necesario.|[Realizar una conmutación por error manual planeada de un grupo de disponibilidad (SQL Server)](../../../database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)<br /><br />[Iniciar, detener, pausar, reanudar y reiniciar el motor de base de datos, Agente SQL Server o el Servicio SQL Server Browser](../../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)|

- Si el servidor es Windows Server 2012 R2, el sistema operativo debe tener aplicado [KB 3030373](http://support.microsoft.com/kb/3090973) .

- Prepare los servidores de los grupos de disponibilidad conforme a las listas de comprobación de [Requisitos previos, restricciones y recomendaciones para grupos de disponibilidad AlwaysOn](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).

- Configure las instancias del servidor para [**grupos de disponibilidad AlwaysOn**](../../../database-engine/availability-groups/windows/configuration-of-a-server-instance-for-always-on-availability-groups-sql-server.md).

### <a name="resources"></a>RECURSOS


[Más información sobre la prueba de DTC en grupos de disponibilidad:](https://blogs.technet.microsoft.com/dataplatform/2016/01/25/sql-server-2016-dtc-support-in-availability-groups/)

[Supervisar grupos de disponibilidad (Transact-SQL)](monitor-availability-groups-transact-sql.md)

[Crear un grupo de disponibilidad (Transact-SQL)](create-an-availability-group-transact-sql.md)


[SQL Server 2016 DTC Support in Availability Groups](http://blogs.technet.microsoft.com/dataplatform/2016/01/25/sql-server-2016-dtc-support-in-availability-groups/) (Compatibilidad con SQL Server 2016 DTC en grupos de disponibilidad) 

[Vínculo externo a un artículo sobre cómo configurar DTC para una instancia agrupada de SQL Server con Windows Server 2008 R2](http://sqlha.com/2013/03/12/how-to-properly-configure-dtc-for-clustered-instances-of-sql-server-with-windows-server-2008-r2/)

