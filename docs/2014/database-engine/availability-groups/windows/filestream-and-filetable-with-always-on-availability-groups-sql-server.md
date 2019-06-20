---
title: FILESTREAM y FileTable con grupos de disponibilidad AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], Availability Groups
- FILESTREAM [SQL Server], Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: fdceda9a-a9db-4d1d-8745-345992164a98
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3fa149aa47c99418bd3109829bfffee698ab3f6e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62814147"
---
# <a name="filestream-and-filetable-with-alwayson-availability-groups-sql-server"></a>FILESTREAM y FileTable con grupos de disponibilidad AlwaysOn (SQL Server)
  Este tema contiene información sobre cómo usar las características FILESTREAM y FileTable con [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
 Se admite toda la funcionalidad de FILESTREAM. Después de una conmutación por error, los datos de FILESTREAM son accesibles tanto en las réplicas secundarias legibles como en la nueva réplica principal.  
  
 Se admite parcialmente la funcionalidad de FileTable. Después de una conmutación por error, es posible tener acceso a los datos de FileTable en la réplica principal, pero no en las réplicas secundarias legibles.  
  
 **En este tema:**  
  
-   [Requisitos previos](#Prerequisites)  
  
-   [Usar nombres de red virtual (VNN) para el acceso de FILESTREAM y FileTable](#vnn)  
  
-   [Tareas relacionadas](#RelatedTasks)  
  
-   [Contenido relacionado](#RelatedContent)  
  
##  <a name="Prerequisites"></a> Requisitos previos  
  
-   Para poder agregar una base de datos que utiliza FILESTREAM, con o sin FileTable, a un grupo de disponibilidad, asegúrese de que FILESTREAM está habilitada en cada instancia de servidor que hospeda una replicación de disponibilidad para el grupo de disponibilidad. Para obtener más información, consulte [Enable and Configure FILESTREAM](../../../relational-databases/blob/enable-and-configure-filestream.md).  
  
##  <a name="vnn"></a> Usar nombres de red virtual (VNN) para el acceso de FILESTREAM y FileTable  
 Al habilitar FILESTREAM en una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], se crea un recurso compartido de nivel de instancia para proporcionar acceso a los datos de FILESTREAM. Puede obtener acceso a este recurso compartido mediante el nombre de equipo en el siguiente formato:  
  
 `\\<computer_name>\<filestream_share_name>`  
  
 Sin embargo, en un grupo de disponibilidad AlwaysOn, el nombre del equipo está virtualizado con un nombre de red virtual, o VNN. Si el equipo es la replicación primaria de un grupo de disponibilidad y las bases de datos del grupo de disponibilidad contienen datos de FILESTREAM, también se crea un recurso compartido de ámbito de VNN para proporcionar acceso a los datos de FILESTREAM. Esto no afecta al acceso de Transact-SQL a los datos de FILESTREAM. Sin embargo, las aplicaciones que usan las API del sistema de archivos tienen que utilizar el recurso compartido de ámbito de VNN, que tiene una ruta de acceso con el siguiente formato:  
  
 `\\<VNN>\<filestream_share_name>`  
  
 Se crea este recurso compartido de ámbito de VNN cuando tiene lugar uno de los siguientes eventos.  
  
-   Agrega una base de datos que contiene datos de FILESTREAM a un grupo de disponibilidad AlwaysOn de la replicación primaria. En este caso, el recurso compartido `\\<computer_name>\<filestream_share_name>` ya existe. Se crea el recurso compartido `\\<VNN>\<filestream_share_name>` .  
  
-   Habilita FILESTREAM para el acceso de transmisión por secuencias de E/S de archivo en una replicación primaria que incluye grupos de disponibilidad. Se crean los siguientes recursos compartidos:  
  
    1.  `\\<computer_name>\<filestream_share_name>`  
  
    2.  `\\<VNN1>\<filestream_share_name>` para el grupo de disponibilidad 1.  
  
    3.  `\\<VNN2>\<filestream_share_name>` para el grupo de disponibilidad 2.  
  
 Estos recursos compartidos de ámbito de VNN también se propagan a todas las réplicas secundarias.  
  
 Cuando la base de datos que contiene datos de FILESTREAM o FileTable pertenece a un grupo de disponibilidad AlwaysOn:  
  
-   Las funciones FILESTREAM y FileTable aceptan o devuelven nombres de red virtual (VNN) en lugar de nombres de equipo. Para obtener más información sobre estas funciones, vea [Funciones FILESTREAM y FileTable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/filestream-and-filetable-functions-transact-sql).  
  
-   Todo acceso a los datos de FILESTREAM o FileTable a través de las API del sistema de archivos debe utilizar VNN en lugar de nombres de equipo.  
  
 Si la aplicación intenta tener acceso al recurso compartido mediante el nombre del equipo en formato `\\<computer_name>\<filestream_share_name>` cuando la base de datos forma parte de un grupo de disponibilidad, se genera un error.  
  
 Si la aplicación intenta tener acceso al recurso compartido con una ruta de acceso de ámbito de VNN cuando la base de datos no forma parte de un grupo de disponibilidad, la solicitud puede realizarse correctamente. En este caso, el nombre de red virtual se resuelve en el nombre de equipo. Sin embargo, este uso no se recomienda en absoluto, ya que la ruta de acceso de ámbito de VNN dejará de funcionar si se quita el grupo de disponibilidad.  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Enable and Configure FILESTREAM](../../../relational-databases/blob/enable-and-configure-filestream.md)  
  
-   [Habilitar los requisitos previos de FileTables](../../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)  
  
##  <a name="RelatedContent"></a> Contenido relacionado  
 Ninguno.  
  
## <a name="see-also"></a>Vea también  
 [Información general de grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)  
  
  
