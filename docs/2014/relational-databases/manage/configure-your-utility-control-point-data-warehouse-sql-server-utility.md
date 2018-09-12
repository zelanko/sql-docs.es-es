---
title: Configurar el almacenamiento de datos del punto de control de la utilidad (utilidad de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c2c6f050-8cdb-4b8e-ad38-4aae0a949847
caps.latest.revision: 6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d8df4e8b4250e2648a84e871f65f649c7663cf19
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2018
ms.locfileid: "43816911"
---
# <a name="configure-your-utility-control-point-data-warehouse-sql-server-utility"></a>Configurar el almacenamiento de datos del punto de control de la utilidad (utilidad de SQL Server)
  Los datos que recopilan las instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se almacenan en el almacén de administración de datos de la utilidad (UMDW); el nombre del archivo de este almacén es sysutility_mdw.  
  
 Puede configurar el período para la retención de datos en el almacén de administración de datos de utilidad. Para obtener más información, vea [Administración de la utilidad &#40;Utilidad de SQL Server&#41;](../../database-engine/utility-administration-sql-server-utility.md).  
  
 Los siguientes valores de configuración no se pueden establecer en esta versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Nombre de UMDW: Sysutility_mdw.  
  
-   Frecuencia de la carga del conjunto de recopilación: cada 15 minutos.  
  
 El directorio del UMDW se puede configurar: \<unidad del sistema>:Archivos de programa\Microsoft SQL Server\MSSQL10_50.<UCP_Name>\MSSQL\Data\\, donde \<unidad del sistema> normalmente es la unidad C:\. El archivo de registro, Sysutility_mdw_\<GUID>_LOG, se encuentra en el mismo directorio.  
  
> [!NOTE]  
>  La ubicación del archivo del almacén de administración de datos de utilidad se puede cambiar mediante detach/attach o ALTER DATABASE. Recomendamos el uso de ALTER DATABASE. Para obtener más información, vea [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql).  
  
## <a name="see-also"></a>Vea también  
 [Características y tareas de la utilidad de SQL Server](sql-server-utility-features-and-tasks.md)  
  
  
