---
title: Requisitos previos para la migración desde el trasvase de registros a Grupos de disponibilidad AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: 2738ce65-205e-4682-92d8-dc7e37c58b2b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 865e8d720e9977f582ac5ae8a0e75d995fc82629
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62789560"
---
# <a name="prerequisites-for-migrating-from-log-shipping-to-alwayson-availability-groups-sql-server"></a>Requisitos previos para migrar desde grupos de trasvase de registros a grupos de disponibilidad AlwaysOn (SQL Server)
  En este tema se describen los requisitos previos para convertir una base de datos principal de trasvase de registros junto con una o varias de sus bases de datos secundarias en una base de datos principal AlwaysOn y una o varias bases de datos secundarias.  
  
> [!NOTE]  
>  Puede configurar cualquier base de datos principal o secundaria (posiblemente legible) de un grupo de disponibilidad como una base de datos principal de trasvase de registros.  
  
 **En este tema:**  
  
-   [Requisitos previos de los grupos de disponibilidad](#AGPrereqsRealAddress)  
  
-   [Requisitos previos del trasvase de registros](#LogShipPrereqs)  
  
-   [Tareas relacionadas](#RelatedTasks)  
  
-   [Contenido relacionado](#RelatedContent)  
  
##  <a name="AGPrereqsRealAddress"></a>Requisitos previos de los grupos de disponibilidad  
 Para permitir los trabajos de copia de seguridad para ejecutarse en la réplica principal del grupo de disponibilidad, use las siguientes opciones de copia de seguridad de los grupos de disponibilidad AlwaysOn:  
  
|Propiedad|Configuración|  
|--------------|-------------|  
|Preferencia de la copia de seguridad automatizada del grupo de disponibilidad|Solo en la réplica principal|  
|Prioridad de copia de seguridad de la réplica principal.|>0|  
  
 **Para obtener más información:**  
  
 [Ver las propiedades del grupo de disponibilidad &#40;SQL Server&#41;](view-availability-group-properties-sql-server.md)  
  
 [Configurar la copia de seguridad en réplicas de disponibilidad &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)  
  
##  <a name="LogShipPrereqs"></a>Requisitos previos del trasvase de registros  
  
-   La base de datos principal del trasvase de registros debe residir en la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospeda la réplica principal actual o inicial del grupo de disponibilidad.  
  
-   Para que una base de datos secundaria de trasvase de registros dada se convierta en una base de datos secundaria AlwaysOn, debe:  
  
    -   Usar el mismo nombre que la base de datos principal.  
  
    -   Residir en una instancia del servidor que hospeda una réplica secundaria para el grupo de disponibilidad.  
  
 Una vez que el trabajo de copia de seguridad se ejecute en la base de datos principal, deshabilite el trabajo de copia de seguridad y, una vez que el trabajo de restauración se haya ejecutado en una base de datos secundaria, deshabilite el trabajo de restauración.  
  
 Después de crear todas las bases de datos secundarias para el grupo de disponibilidad, si desea realizar copias de seguridad en las réplicas secundarias, debe configurar de nuevo la preferencia de copia de seguridad automatizada del grupo de disponibilidad.  
  
 **Para obtener más información:**  
  
 [Conversión de una configuración de trasvase en un grupo de disponibilidad](https://blogs.msdn.com/b/sqlalwayson/archive/2012/01/09/converting-a-logshipping-configuration-to-availability-group.aspx) (un blog SQL Server)  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
 **Trasvase de registros**  
  
-   [Actualizar el trasvase de registros a SQL Server 2014 &#40;Transact-SQL&#41;](../../log-shipping/upgrading-log-shipping-to-sql-server-2016-transact-sql.md)  
  
-   [Quitar el trasvase de registros &#40;SQL Server&#41;](../../log-shipping/remove-log-shipping-sql-server.md)  
  
 **Grupos de disponibilidad AlwaysOn**  
  
-   [Usar el Asistente para grupo de disponibilidad &#40;SQL Server Management Studio&#41;](use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Usar el cuadro de diálogo Nuevo grupo de disponibilidad &#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Crear un grupo de disponibilidad &#40;Transact-SQL&#41;](create-an-availability-group-transact-sql.md)  
  
-   [Crear un grupo de disponibilidad &#40;SQL Server PowerShell&#41;](../../../powershell/sql-server-powershell.md)  
  
-   [Combinar una base de datos secundaria con un grupo de disponibilidad &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [Configurar la copia de seguridad en réplicas de disponibilidad &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)  
  
##  <a name="RelatedContent"></a> Contenido relacionado  
  
-   **Blogs:**  
  
     [Convertir una configuración de trasvase en un grupo de disponibilidad](https://blogs.msdn.com/b/sqlalwayson/archive/2012/01/09/converting-a-logshipping-configuration-to-availability-group.aspx)  
  
     [Agregar una base de datos principal y una base de datos secundaria de trasvase de registros a un grupo de disponibilidad existente](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/01/use-log-shipping-to-prepare-secondary-databases-for-an-existing-availability-group.aspx)  
  
     [Blogs del equipo de AlwaysOn de SQL Server: el blog oficial del equipo de AlwaysOn de SQL Server](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [Blogs de los ingenieros de SQL Server de CSS](https://blogs.msdn.com/b/psssql/)  
  
-   **Notas del producto:**  
  
     [Guía de migración: migrar a grupos de disponibilidad AlwaysOn desde implementaciones anteriores que combinan creación de reflejo de la base de datos y trasvase de registros](https://msdn.microsoft.com/library/jj635217)  
  
     [Notas del producto de Microsoft para SQL Server 2012](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [Notas del producto del equipo de asesoramiento al cliente de SQL Server](http://sqlcat.com/)  
  
## <a name="see-also"></a>Consulte también  
 [Acerca del trasvase de registros &#40;SQL Server&#41;](../../log-shipping/about-log-shipping-sql-server.md)   
 [Información general de Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Supervisión de los grupos de disponibilidad &#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)  
  
  
