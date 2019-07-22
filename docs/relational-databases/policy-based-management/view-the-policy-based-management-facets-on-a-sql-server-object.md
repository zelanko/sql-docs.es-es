---
title: Ver las facetas de administración basada en directivas en un objeto de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, view facets
ms.assetid: 5f423b9f-a6c4-41a7-9d8d-8f4926ce1fb4
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 82acf976fef80f62059b5a433bb74e3fbbadec80
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68021431"
---
# <a name="view-the-policy-based-management-facets-on-a-sql-server-object"></a>Ver las facetas de administración basada en directivas en un objeto de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describe cómo ver todas las facetas de administración basada en directivas aplicadas a un objeto específico de SQL Server en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para ver todas las facetas de un objeto mediante:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Requiere la pertenencia al rol PolicyAdministratorRole en la base de datos msdb.  
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-view-all-of-the-facets-in-an-object"></a>Para ver todas las facetas de un objeto  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], objeto de instancia, base de datos u objeto de base de datos y, después, haga clic en **Facetas**.  
  
2.  En el cuadro de diálogo **Ver facetas -** _nombre_de_objeto_, en la lista **Faceta**, seleccione una faceta para ver sus propiedades. Para obtener más información acerca de las opciones disponibles en este cuadro de diálogo, vea [View Facets Dialog Box](../../relational-databases/policy-based-management/view-facets-dialog-box.md).  
  
3.  Cuando termine, haga clic en **Aceptar**.  
  
  
