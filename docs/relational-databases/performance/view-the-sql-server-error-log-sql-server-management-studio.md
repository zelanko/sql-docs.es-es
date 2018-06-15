---
title: Ver el registro de errores de SQL Server (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 09/29/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: performance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- viewing logs
- displaying logs
- errors [SQL Server], logs
- logs [SQL Server], SQL Server error logs
- logs [SQL Server], viewing
ms.assetid: 55f468ba-146c-4ab3-95cd-d35d051afd12
caps.latest.revision: 14
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 57bd20cc06d52e58c81c2691844516dc0037435f
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2018
ms.locfileid: "34332906"
---
# <a name="view-the-sql-server-error-log-sql-server-management-studio"></a>Ver el registro de errores de SQL Server (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
El registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contiene eventos definidos por el usuario y determinados eventos del sistema que puede usar para solucionar problemas. 

## <a name="view-the-logs"></a>Ver los registros

1. En SQL Server Management Studio, seleccione **Explorador de objetos**. Para abrir **Explorador de objetos**, seleccione F8. O bien, en el menú superior, seleccione **Ver** y, después, **Explorador de objetos**:
    
    ![Object_Explorer](../../relational-databases/performance/media/object-explorer.png) 

2. En **Explorador de objetos**, conéctese a una instancia de SQL Server y expándala.
  
3. Busque y expanda la sección **Administración** (suponiendo que tiene los permisos para verla).

4. Haga clic con el botón derecho en **Registros de SQL Server**, seleccione **Ver** y, luego, elija **Registro de SQL Server**.

    ![View_SQLServer_Log_SSMS](../../relational-databases/performance/media/view-sqlserver-log-ssms.png) 
 
5. Aparecerá el **Visor de archivos de registro** (puede tardar un momento) con una lista de los registros que puede ver.
  
  ## <a name="see-also"></a>Vea también
  Para obtener más información, consulte la publicación [Identify location of the SQL Server Error Log file](https://www.mssqltips.com/sqlservertip/2506/identify-location-of-the-sql-server-error-log-file/) (Identificar la ubicación del archivo de registro de errores de SQL Server) de [MSSQLTips.com's](https://www.mssqltips.com/).

