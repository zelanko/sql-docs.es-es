---
title: Consulta de las propiedades de una faceta de administración basada en directivas
description: Obtenga información sobre cómo ver las propiedades de una faceta de administración basada en directivas en SQL Server mediante SQL Server Management Studio (SSMS).
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, view facet properties
ms.assetid: 022a244c-c2e7-4467-b9a2-c7a27859be22
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 3a5a938928817b8ffb5282b2af7d2a505b442302
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "75558100"
---
# <a name="view-the-properties-of-a-policy-based-management-facet"></a>Ver las propiedades de una faceta de administración basada en directivas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describe cómo ver las propiedades de una faceta de administración basada en directivas en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para ver propiedades de una faceta mediante:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Requiere la pertenencia al rol PolicyAdministratorRole en la base de datos msdb.  
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-view-the-properties-of-a-facet"></a>Para ver las propiedades de una faceta  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor que contiene la faceta cuyas propiedades desea ver.  
  
2.  Haga clic en el signo más para expandir la carpeta **Administración** .  
  
3.  Haga clic en el signo más para expandir la carpeta **Administración de directivas**.  
  
4.  Haga clic en el signo más para expandir la carpeta **Facetas** .  
  
5.  Haga clic con el botón derecho en la faceta cuyas propiedades quiere ver y seleccione **Propiedades**. Para más información sobre las opciones disponibles en el cuadro de diálogo **Propiedades de faceta -** _nombre_de_faceta_, vea [Cuadro de diálogo Propiedades de faceta, página General](../../relational-databases/policy-based-management/facet-properties-dialog-box-general-page.md), [Cuadro de diálogo Propiedades de faceta, página Directivas dependientes](../../relational-databases/policy-based-management/facet-properties-dialog-box-dependent-policies-page.md) y [Cuadro de diálogo Propiedades de faceta, página Condiciones dependientes](../../relational-databases/policy-based-management/facet-properties-dialog-box-dependent-conditions-page.md).  
  
6.  Cuando termine, haga clic en **Cerrar**.  

