---
title: Copia de en un archivo XML un estado de faceta de administración basada en directivas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, copy facet state to XML file
ms.assetid: 7d604ab1-6dd6-4f8e-a79c-eba99ab106fd
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3cae39c440c86348763b20ae04c70b3ce2ecc181
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2019
ms.locfileid: "54127108"
---
# <a name="copy-a-policy-based-management-facet-state-to-an-xml-file"></a>Copiar en un archivo XML un estado de faceta de administración basada en directivas
  En este tema se describe cómo copiar el estado de una faceta de administración basada en directivas en un archivo XML en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para copiar un estado de faceta en un archivo XML mediante:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Los procedimientos descritos en este tema requieren la pertenencia al rol PolicyAdministratorRole de la base de datos msdb.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-copy-a-facet-state-to-an-xml-file"></a>Para copiar un estado de faceta en un archivo XML  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], objeto de instancia, base de datos u objeto de base de datos y, después, haga clic en **Facetas**.  
  
2.  En el **ver facetas -**_object_name_ cuadro de diálogo, haga clic en **exportar estado actual como directiva**.  
  
3.  En el cuadro de diálogo **Exportar como directiva** , escriba la ruta de acceso y el nombre del archivo, o use el botón Examinar (**...**) para buscar el archivo y, después, escriba el nombre del archivo XML. Para obtener más información acerca de las opciones disponibles en este cuadro de diálogo, vea [Export As Policy Dialog Box](export-as-policy-dialog-box.md).  
  
4.  Cuando termine, haga clic en **Aceptar**.  
  
  
