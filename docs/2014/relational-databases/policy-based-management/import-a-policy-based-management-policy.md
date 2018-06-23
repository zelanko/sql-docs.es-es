---
title: Importar una directiva de administración basada en directivas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Policy-Based Management, import policy
ms.assetid: 850b7ef9-d2b7-4754-bf04-7cb419ffb776
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: d28c6ffad683aee7dd364a360ba0800b13fdaa67
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36112469"
---
# <a name="import-a-policy-based-management-policy"></a>Importar una directiva de administración basada en directivas
  En este tema se describe cómo importar una instancia de directiva de administración basada en directivas en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para importar una instancia de directiva mediante:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se distribuye con directivas que se pueden utilizar para supervisar una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. De forma predeterminada, estas directivas no se instalan en [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], pero se pueden importar desde la ubicación predeterminada de C:\Archivos de programa\Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Requiere la pertenencia al rol PolicyAdministratorRole en la base de datos msdb.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-import-a-policy-instance"></a>Para importar una instancia de directiva  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor en que residirá la instancia de directiva recién importada.  
  
2.  Haga clic en el signo más para expandir la carpeta **Administración** .  
  
3.  Haga clic en el signo más para expandir la carpeta **Administración de directivas**.  
  
4.  Haga clic con el botón derecho en la carpeta **Directivas** y seleccione **Importar directiva**.  
  
5.  En el cuadro de diálogo **Importar** , escriba la ruta de acceso y el nombre del archivo, o use el botón Examinar (**...**) para buscar el archivo XML que contiene la directiva y, después, seleccione el archivo. Para obtener más información acerca de las opciones disponibles en el cuadro de diálogo **Importar** , vea [Import Policies Dialog Box](import-policies-dialog-box.md).  
  
6.  Cuando termine, haga clic en **Aceptar**.  
  
  