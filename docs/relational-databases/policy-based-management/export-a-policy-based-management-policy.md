---
title: "Exportar una directiva de administración basada en directivas | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Policy-Based Management, export policy
ms.assetid: f0001b33-9078-4432-8460-496736fb325a
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c409fd3fc46ce2612290737bf658dd4358280495
ms.lasthandoff: 04/11/2017

---
# <a name="export-a-policy-based-management-policy"></a>Exportar una directiva de administración basada en directivas
  En este tema se describe cómo exportar una directiva de administración basada en directivas en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para exportar una directiva mediante:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Requiere la pertenencia al rol PolicyAdministratorRole en la base de datos msdb.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-export-a-policy"></a>Para exportar una directiva  
  
1.  En el Explorador de objetos, haga clic en el signo más para expandir el servidor que contiene la directiva de administración basada en directivas que desea exportar.  
  
2.  Haga clic en el signo más para expandir la carpeta **Administración** .  
  
3.  Haga clic en el signo más para expandir la carpeta **Administración de directivas**.  
  
4.  Haga clic en el signo más para expandir la carpeta **Directivas** .  
  
5.  Haga clic con el botón derecho en la directiva que quiera exportar y seleccione **Exportar directiva**.  
  
6.  En el cuadro de diálogo **Exportar directiva** , escriba la ruta de acceso y el nombre del archivo en la barra de direcciones. También puede buscar una ubicación adecuada para el archivo en el panel de navegación del cuadro de diálogo, y escribir el nombre del archivo XML en el cuadro **Nombre de archivo** .  
  
7.  Cuando termine, haga clic en **Guardar**.  
  
  
