---
title: Evaluar una directiva de administración basada en directivas desde dicha directiva | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, evaluate policy
ms.assetid: 0b3214bd-d0ab-45ab-9281-3d95507abe54
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4820426060069c805bd0391fa2f1f135f2766ed3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48228145"
---
# <a name="evaluate-a-policy-based-management-policy-from-that-policy"></a>Evaluar una directiva de administración basada en directivas desde dicha directiva
  En este tema se describe cómo evaluar una directiva utilizando esa directiva en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para evaluar una directiva mediante:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Requiere la pertenencia al rol PolicyAdministratorRole en la base de datos msdb.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-evaluate-a-policy"></a>Para evaluar una directiva  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor que contiene la directiva que desea evaluar.  
  
2.  Haga clic en el signo más para expandir la carpeta **Administración** .  
  
3.  Haga clic en el signo más para expandir la carpeta **Administración de directivas**.  
  
4.  Haga clic en el signo más para expandir la carpeta **Directivas** .  
  
5.  Haga clic con el botón derecho en la directiva que quiere evaluar y seleccione **Evaluar**.  
  
6.  En el cuadro de diálogo **Evaluar resultados**  se muestran los resultados de la evaluación de la directiva. En los destinos que no cumplen la directiva y que tienen propiedades que pueden estar reconfiguradas por la administración basada en directivas, puede exigir el cumplimiento de la directiva haciendo clic en **Aplicar**. Para obtener más información acerca de las opciones disponibles en el cuadro de diálogo **Evaluar directivas** , vea [Evaluate Policies Dialog Box, Policy Selection Page](evaluate-policies-dialog-box-policy-selection-page.md) y [Evaluate Policies Dialog Box, Evaluation Results Page](evaluate-policies-dialog-box-evaluation-results-page.md).  
  
7.  Cuando termine, haga clic en **Cerrar**.  
  
  
