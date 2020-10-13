---
title: Configurar el almacenamiento de datos del punto de control de la utilidad (utilidad de SQL Server) | Microsoft Docs
description: Obtenga información sobre la utilidad Almacén de administración de datos, donde las instancias de SQL Server almacenan los datos. Aprenda a configurar su período de retención de datos y su directorio.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: c2c6f050-8cdb-4b8e-ad38-4aae0a949847
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 06080937156afc4e38c9ef59bd9b92e98695eb57
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2020
ms.locfileid: "91867877"
---
# <a name="configure-your-utility-control-point-data-warehouse-sql-server-utility"></a>Configurar el almacenamiento de datos del punto de control de la utilidad (utilidad de SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Los datos que recopilan las instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se almacenan en el almacén de administración de datos de la utilidad (UMDW); el nombre del archivo de este almacén es sysutility_mdw.  
  
 Puede configurar el período para la retención de datos en el almacén de administración de datos de utilidad. Para obtener más información, vea [Administración de la utilidad &#40;Utilidad de SQL Server&#41;](/previous-versions/sql/sql-server-2016/ee240832(v=sql.130)).  
  
 Los siguientes valores de configuración no se pueden establecer en esta versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Nombre de UMDW: Sysutility_mdw.  
  
-   Frecuencia de la carga del conjunto de recopilación: cada 15 minutos.  
  
 El directorio de UMDW se puede configurar: \<System drive>:\Archivos de programa\Microsoft SQL Server\MSSQL10_50.<Nombre_de_UCP>\MSSQL\Data\\, donde \<System drive> normalmente es la unidad C:\. El archivo de registro, Sysutility_mdw_\<GUID>_LOG, se encuentra en el mismo directorio.  
  
> [!NOTE]  
>  La ubicación del archivo del almacén de administración de datos de utilidad se puede cambiar mediante detach/attach o ALTER DATABASE. Recomendamos el uso de ALTER DATABASE. Para obtener más información, vea [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
## <a name="see-also"></a>Consulte también  
 [Características y tareas de la utilidad de SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)  
  
