---
title: "Ver las propiedades de una faceta de administración basada en directivas | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Policy-Based Management, view facet properties
ms.assetid: 022a244c-c2e7-4467-b9a2-c7a27859be22
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0ef0cb61dbfbf8e026b64db3ce97c24a3806be5b
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/23/2018
---
# <a name="view-the-properties-of-a-policy-based-management-facet"></a>Ver las propiedades de una faceta de administración basada en directivas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
En este tema se describe cómo ver las propiedades de una faceta de administración basada en directivas en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para ver propiedades de una faceta mediante:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Requiere la pertenencia al rol PolicyAdministratorRole en la base de datos msdb.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-view-the-properties-of-a-facet"></a>Para ver las propiedades de una faceta  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor que contiene la faceta cuyas propiedades desea ver.  
  
2.  Haga clic en el signo más para expandir la carpeta **Administración** .  
  
3.  Haga clic en el signo más para expandir la carpeta **Administración de directivas**.  
  
4.  Haga clic en el signo más para expandir la carpeta **Facetas** .  
  
5.  Haga clic con el botón derecho en la faceta cuyas propiedades quiere ver y seleccione **Propiedades**. Para obtener más información sobre las opciones disponibles en el cuadro de diálogo **Propiedades de faceta –***nombre_de_faceta*, vea [Cuadro de diálogo Propiedades de faceta, página General](../../relational-databases/policy-based-management/facet-properties-dialog-box-general-page.md), [Cuadro de diálogo Propiedades de faceta, página Directivas dependientes](../../relational-databases/policy-based-management/facet-properties-dialog-box-dependent-policies-page.md) y [Cuadro de diálogo Propiedades de faceta, página Condiciones dependientes](../../relational-databases/policy-based-management/facet-properties-dialog-box-dependent-conditions-page.md).  
  
6.  Cuando termine, haga clic en **Cerrar**.  
  
  
