---
title: Configurar el almacenamiento de datos del punto de control de la utilidad (utilidad de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: c2c6f050-8cdb-4b8e-ad38-4aae0a949847
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d2a9f40c2d1566a1f8ca5f054467f61da1920e5f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62805941"
---
# <a name="configure-your-utility-control-point-data-warehouse-sql-server-utility"></a>Configurar el almacenamiento de datos del punto de control de la utilidad (utilidad de SQL Server)
  Los datos que recopilan las instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se almacenan en el almacén de administración de datos de la utilidad (UMDW); el nombre del archivo de este almacén es sysutility_mdw.  
  
 Puede configurar el período para la retención de datos en el almacén de administración de datos de utilidad. Para obtener más información, vea [Administración de la utilidad &#40;Utilidad de SQL Server&#41;](../../database-engine/utility-administration-sql-server-utility.md).  
  
 Los siguientes valores de configuración no se pueden establecer en esta versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Nombre de UMDW: Sysutility_mdw.  
  
-   Frecuencia de la carga del conjunto de recopilación: cada 15 minutos.  
  
 El directorio de UMDW se puede configurar: \<Unidad del sistema:>:Archivos de programa\Microsoft SQL Server\MSSQL10_50.<Nombre_UCP\MSSQL\Data\\,donde \<Unidad del sistema> normalmente es la unidad C:\. El archivo de registro, Sysutility_mdw_\<GUID>_LOG, se encuentra en el mismo directorio.  
  
> [!NOTE]  
>  La ubicación del archivo del almacén de administración de datos de utilidad se puede cambiar mediante detach/attach o ALTER DATABASE. Recomendamos el uso de ALTER DATABASE. Para obtener más información, vea [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql).  
  
## <a name="see-also"></a>Consulte también  
 [Características y tareas de la utilidad de SQL Server](sql-server-utility-features-and-tasks.md)  
  
  
