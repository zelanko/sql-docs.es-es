---
title: Evaluar una directiva de administración basada en directivas según una programación | Microsoft Docs
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
- Policy-Based Management, evaluate policy
ms.assetid: bea09522-ff47-4037-ab55-a98ea7c10099
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 56354766e7000bf5e7d7a1eb214da1be796ae82f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107860"
---
# <a name="evaluate-a-policy-based-management-policy-on-a-schedule"></a>Evaluar una directiva de administración basada en directivas según una programación
  En este tema se describe cómo evaluar una directiva de administración basada en directivas según una programación en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para evaluar una directiva según una programación mediante**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Requiere la pertenencia al rol PolicyAdministratorRole en la base de datos msdb.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-evaluate-a-policy-on-a-schedule"></a>Para evaluar una directiva según una programación  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor que contiene la programación de directiva que desea evaluar.  
  
2.  Haga clic en el signo más para expandir la carpeta **Administración** .  
  
3.  Haga clic en el signo más para expandir la carpeta **Administración de directivas**.  
  
4.  Haga clic en el signo más para expandir la carpeta **Directivas** .  
  
5.  Haga clic con el botón derecho en la directiva cuya programación quiera evaluar y seleccione **Propiedades**.  
  
6.  En el cuadro diálogo *Abrir directiva –***nombre_de_directiva*, en la lista **Modo de evaluación**, seleccione **Al programar**.  
  
7.  En **Programación**, haga clic en **Elegir** para especificar una programación existente o en **Nuevo** para crear una programación nueva.  
  
8.  Cuando termine, haga clic en **Aceptar**.  
  
  