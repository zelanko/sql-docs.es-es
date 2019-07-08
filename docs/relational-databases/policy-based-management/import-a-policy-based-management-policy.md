---
title: Importar una directiva de administración basada en directivas | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
manager: craigg
ms.openlocfilehash: 5c3a8ee9af1451d275f4168c86e5067fc26c06bd
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/05/2019
ms.locfileid: "67584904"
---
# <a name="import-a-policy-based-management-policy"></a>Importar una directiva de administración basada en directivas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describe cómo importar una instancia de directiva de administración basada en directivas en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para importar una instancia de directiva mediante:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se distribuye con directivas que se pueden utilizar para supervisar una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. De forma predeterminada, estas directivas no se instalan en [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], pero se pueden importar desde la ubicación predeterminada de C:\Archivos de programa\Microsoft SQL Server\###\Tools\Policies\DatabaseEngine\1033 o C:\Archivos de programa (x86)\Microsoft SQL Server\###\Tools\Policies\DatabaseEngine\1033 en las instalaciones de 64 bits.
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Requiere la pertenencia al rol PolicyAdministratorRole en la base de datos msdb.  
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-import-a-policy-instance"></a>Para importar una instancia de directiva  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor en que residirá la instancia de directiva recién importada.  
  
2.  Haga clic en el signo más para expandir la carpeta **Administración** .  
  
3.  Haga clic en el signo más para expandir la carpeta **Administración de directivas**.  
  
4.  Haga clic con el botón derecho en la carpeta **Directivas** y seleccione **Importar directiva**.  
  
5.  En el cuadro de diálogo **Importar** , escriba la ruta de acceso y el nombre del archivo, o use el botón Examinar ( **...** ) para buscar el archivo XML que contiene la directiva y, después, seleccione el archivo. Para obtener más información acerca de las opciones disponibles en el cuadro de diálogo **Importar** , vea [Import Policies Dialog Box](../../relational-databases/policy-based-management/import-policies-dialog-box.md).  
  
6.  Cuando termine, haga clic en **Aceptar**.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

