---
title: Evaluar una directiva de administración basada en directivas según una programación | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, evaluate policy
ms.assetid: bea09522-ff47-4037-ab55-a98ea7c10099
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: ad7d22492411538a1f397f1a7d02436d1a02bde7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67901154"
---
# <a name="evaluate-a-policy-based-management-policy-on-a-schedule"></a>Evaluar una directiva de administración basada en directivas según una programación
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describe cómo evaluar una directiva de administración basada en directivas según una programación en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para evaluar una directiva según una programación mediante**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Requiere la pertenencia al rol PolicyAdministratorRole en la base de datos msdb.  
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-evaluate-a-policy-on-a-schedule"></a>Para evaluar una directiva según una programación  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor que contiene la programación de directiva que desea evaluar.  
  
2.  Haga clic en el signo más para expandir la carpeta **Administración** .  
  
3.  Haga clic en el signo más para expandir la carpeta **Administración de directivas**.  
  
4.  Haga clic en el signo más para expandir la carpeta **Directivas** .  
  
5.  Haga clic con el botón derecho en la directiva cuya programación quiera evaluar y seleccione **Propiedades**.  
  
6.  En el cuadro de diálogo **Abrir directiva -** _nombre_de_directiva_, en la lista **Modo de evaluación**, seleccione **Al programar**.  
  
7.  En **Programación**, haga clic en **Elegir** para especificar una programación existente o en **Nuevo** para crear una programación nueva.  
  
8.  Cuando termine, haga clic en **Aceptar**.  
  
  
