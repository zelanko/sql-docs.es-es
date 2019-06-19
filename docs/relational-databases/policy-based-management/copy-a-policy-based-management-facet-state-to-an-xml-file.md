---
title: Copia de en un archivo XML un estado de faceta de administración basada en directivas | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, copy facet state to XML file
ms.assetid: 7d604ab1-6dd6-4f8e-a79c-eba99ab106fd
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 45ebbb2cbbc0e39ee3da54e4b914aff4906df1cc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63007616"
---
# <a name="copy-a-policy-based-management-facet-state-to-an-xml-file"></a>Copiar en un archivo XML un estado de faceta de administración basada en directivas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describe cómo copiar el estado de una faceta de administración basada en directivas en un archivo XML en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para copiar un estado de faceta en un archivo XML mediante:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Los procedimientos descritos en este tema requieren la pertenencia al rol PolicyAdministratorRole de la base de datos msdb.  
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-copy-a-facet-state-to-an-xml-file"></a>Para copiar un estado de faceta en un archivo XML  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], objeto de instancia, base de datos u objeto de base de datos y, después, haga clic en **Facetas**.  
  
2.  En el cuadro de diálogo **Ver facetas -** _nombre_de_objeto_, haga clic en **Exportar estado actual como directiva**.  
  
3.  En el cuadro de diálogo **Exportar como directiva** , escriba la ruta de acceso y el nombre del archivo, o use el botón Examinar ( **...** ) para buscar el archivo y, después, escriba el nombre del archivo XML. Para obtener más información acerca de las opciones disponibles en este cuadro de diálogo, vea [Export As Policy Dialog Box](../../relational-databases/policy-based-management/export-as-policy-dialog-box.md).  
  
4.  Cuando termine, haga clic en **Aceptar**.  
  
  
