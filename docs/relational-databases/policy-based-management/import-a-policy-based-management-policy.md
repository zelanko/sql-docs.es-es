---
description: Importar una directiva de administración basada en directivas
title: Importar una directiva de administración basada en directivas | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, import policy
ms.assetid: 850b7ef9-d2b7-4754-bf04-7cb419ffb776
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 37f49a006b0fe17120af2309f9b3991ab594ebda
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88423719"
---
# <a name="import-a-policy-based-management-policy"></a>Importar una directiva de administración basada en directivas
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  En este tema se describe cómo importar una instancia de directiva de administración basada en directivas en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="permissions"></a>Permisos
 Requiere la pertenencia al rol PolicyAdministratorRole en la base de datos msdb.

  
##  <a name="using-sql-server-management-studio"></a>Uso de SQL Server Management Studio  
  
### <a name="to-import-a-policy-instance"></a>Para importar una instancia de directiva  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor en que residirá la instancia de directiva recién importada.  
  
2.  Haga clic en el signo más para expandir la carpeta **Administración** .  
  
3.  Haga clic en el signo más para expandir la carpeta **Administración de directivas**.  
  
4.  Haga clic con el botón derecho en la carpeta **Directivas** y seleccione **Importar directiva**.  
  
5.  En el cuadro de diálogo **Importar** , escriba la ruta de acceso y el nombre del archivo, o use el botón Examinar (**...**) para buscar el archivo XML que contiene la directiva y, después, seleccione el archivo. Para obtener más información acerca de las opciones disponibles en el cuadro de diálogo **Importar** , vea [Import Policies Dialog Box](../../relational-databases/policy-based-management/import-policies-dialog-box.md).  
  
6.  Cuando termine, haga clic en **Aceptar**.  


## <a name="example-policies"></a>Directivas de ejemplo
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] no incluye directivas de ejemplo, pero se puede tener acceso a las directivas de ejemplo distribuidas anteriormente instalando [la versión 17 de SQL Server Management Studio](../../ssms/release-notes-ssms.md#previous-ssms-releases).  Una vez instalada la versión 17 de SQL Server Management Studio, encontrará las directivas de ejemplo en `C:\Program Files (x86)\Microsoft SQL Server\140\Tools\Policies`. Estas directivas se pueden importar y usar como base para sus propias directivas de administración basada en directivas.
