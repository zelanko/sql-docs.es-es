---
title: Consulta del registro de errores de SQL Server(SSMS)
description: Consulte el registro de errores de SQL Server en SQL Server Management Studio (SSMS).
ms.custom: seo-dt-2019
ms.date: 09/29/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- viewing logs
- displaying logs
- errors [SQL Server], logs
- logs [SQL Server], SQL Server error logs
- logs [SQL Server], viewing
ms.assetid: 55f468ba-146c-4ab3-95cd-d35d051afd12
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: f6410575af0d05b8d407ba9f52cc116fbe2ac733
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2019
ms.locfileid: "74165474"
---
# <a name="view-the-sql-server-error-log-in-sql-server-management-studio-ssms"></a>Consulta del registro de errores de SQL Server en SQL Server Management Studio (SSMS)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
El registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contiene eventos definidos por el usuario y determinados eventos del sistema que puede usar para solucionar problemas. 

## <a name="view-the-logs"></a>Visualización de los registros

1. En SQL Server Management Studio, seleccione **Explorador de objetos**. Para abrir **Explorador de objetos**, seleccione F8. O bien, en el menú superior, seleccione **Ver** y, después, **Explorador de objetos**:
    
    ![Object_Explorer](../../relational-databases/performance/media/object-explorer.png) 

2. En **Explorador de objetos**, conéctese a una instancia de SQL Server y expándala.
  
3. Busque y expanda la sección **Administración** (suponiendo que tiene los permisos para verla).

4. Haga clic con el botón derecho en **Registros de SQL Server**, seleccione **Ver** y, luego, elija **Registro de SQL Server**.

    ![View_SQLServer_Log_SSMS](../../relational-databases/performance/media/view-sqlserver-log-ssms.png) 
 
5. Aparecerá el **Visor de archivos de registro** (puede tardar un momento) con una lista de los registros que puede ver.

  ## <a name="see-also"></a>Consulte también
  Para obtener más información, consulte la publicación [Identify location of the SQL Server Error Log file](https://www.mssqltips.com/sqlservertip/2506/identify-location-of-the-sql-server-error-log-file/) (Identificar la ubicación del archivo de registro de errores de SQL Server) de [MSSQLTips.com's](https://www.mssqltips.com/).

