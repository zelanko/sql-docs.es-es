---
title: "Notas de la versión de SQL Server 2012 SP2 | Microsoft Docs"
ms.prod: sql-server
ms.prod_service: sql-non-specified
ms.service: server-general
ms.component: 
ms.technology: server-general
ms.custom: 
ms.date: 01/31/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 67cb8b3e-3d82-47f4-840d-0f12a3bff565
caps.latest.revision: "6"
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 83969d05f234dc5e6384754971ca6eb5a2621006
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="sql-server-2012-sp2-release-notes"></a>SQL Server 2012 SP2 Release Notes
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)] En las notas de la versión, se describen los problemas que debe conocer antes de instalar SQL Server 2012 Service Pack 2 o para solucionar los problemas que surjan. Las notas de la versión solo están disponibles en Internet, no se incluyen en el disco de instalación. Se actualizan periódicamente, conforme se van detectando nuevos problemas. Vea [Errores corregidos en el Service Pack 2 de SQL Server 2012](http://support.microsoft.com/KB/2958429) si desea más información.  
  
## <a name="choose-the-correct-file-to-download-and-install"></a>Elegir el archivo correcto para su descarga e instalación  
Use la tabla siguiente para determinar la ubicación y el nombre del archivo que debe descargar en función de la versión que tenga instalada actualmente. Las páginas de descarga contienen los requisitos del sistema e instrucciones básicas para la instalación.  
  
||||  
|-|-|-|  
|**La versión instalada actualmente es...**|**Y desea...**|**Descargue e instale...**|  
|Instalaciones de 32 bits:|||  
|Una versión de 32 bits de cualquier edición de SQL Server 2012|Actualizar a la versión de 32 bits de SQL Server 2012 SP2|**SQLServer2012SP2-KB2958429-**<arch>**-**<lang id>**.exe** desde la página de descarga de [SQL Server 2012 SP2](http://go.microsoft.com/fwlink/?LinkID=401006)|  
|Una versión de 32 bits de SQL Server 2012 RTM Express|Actualizar a la versión de 32 bits de SQL Server 2012 Express SP2|**SQLEXPR_**<arch>**_**<lang>**.msi** desde la [página de descarga de SQL Server 2012 SP2 Express](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|Una versión de 32 bits únicamente las herramientas de cliente y de administración para SQL Server 2012 (incluido SQL Server 2012 Management Studio)|Actualizar las herramientas de cliente y de administración a la versión de 32 bits de SQL Server 2012 SP2|**SQLEXPRWT_**<arch>**_**<lang>**.msi** desde la [página de descarga de SQL Server 2012 SP2 Express](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|Una versión de 32 bits de SQL Server 2012 Management Studio Express|Actualizar a la versión de 32 bits de SQL Server 2012 SP2 Management Studio Express|**SQLManagementStudio_**<arch>**_**<lang>**.msi** desde la [página de descarga de SQL Server 2012 SP2 Express](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|Una versión de 32 bits de cualquier edición de SQL Server 2012 y una versión de 32 bits de las herramientas de cliente y de administración (incluido SQL Server 2012 RTM Management Studio)|Actualizar todos los productos a la versión de 32 bits de SQL Server 2012 SP2|**SQLEXPRADV_**<arch>**_**<lang>**.msi** desde la [página de descarga de SQL Server 2012 SP2 Express.](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|Una versión de 32 bits de una o más herramientas del [Feature Pack de Microsoft SQL Server 2012 RTM](http://www.microsoft.com/download/details.aspx?id=29065) o el [Feature Pack de Microsoft SQL Server 2012 SP1](http://go.microsoft.com/fwlink/p/?LinkID=268266)|Actualizar las herramientas a la versión de 32 bits del Feature Pack de Microsoft SQL Server 2012 S2|Una o varias herramientas de [la página de descarga del Feature Pack de SQL Server 2012 SP2 de Microsoft](http://go.microsoft.com/fwlink/?LinkID=401008)|  
|Instalaciones de 64 bits:|||  
|Una versión de 64 bits de cualquier edición de SQL Server 2012|Actualizar a la versión de 64 bits de SQL Server 2012 SP2|SQLServer2012SP2-KB2958429-<arch>-<langid>.exe desde la [página de descarga de SQL Server 2012 SP2](http://go.microsoft.com/fwlink/?LinkID=401006)|  
|Una versión de 64 bits de SQL Server 2012 RTM Express|Actualizar a la versión de 64 bits de SQL Server 2012 SP2|**SQLEXPR_**<arch>**_**<lang>**.msi** desde la [página de descarga de SQL Server 2012 SP2 Express](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|Una versión de 64 bits únicamente las herramientas de cliente y de administración para SQL Server 2012 (incluido SQL Server 2012 Management Studio)|Actualizar las herramientas de cliente y de administración a la versión de 64 bits de SQL Server 2012 SP2|**SQLEXPRWT_**<arch>**_**<lang>**.msi** desde la [página de descarga de SQL Server 2012 SP2 Express](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|Una versión de 64 bits de SQL Server 2012 Management Studio Express|Actualizar a la versión de 64 bits de SQL Server 2012 SP2 Management Studio Express|**SQLManagementStudio_**<arch>**_**<lang>**.msi** desde la [página de descarga de SQL Server 2012 SP2 Express](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|Una versión de 64 bits de una o más herramientas del [Feature Pack de Microsoft SQL Server 2012 RTM](http://www.microsoft.com/download/details.aspx?id=29065) o el [Feature Pack de Microsoft SQL Server 2012 SP1](http://go.microsoft.com/fwlink/p/?LinkID=268266)|Actualizar las herramientas a la versión de 64 bits del Feature Pack de Microsoft SQL Server 2012 S2|Una o varias herramientas de [la página de descarga del Feature Pack de SQL Server 2012 SP2 de Microsoft](http://go.microsoft.com/fwlink/?LinkID=401008)|  
  
