---
title: Eliminación de una directiva de administración basada en directivas | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, delete policies
ms.assetid: 488f0305-190c-4223-aa5c-e9bd43b520eb
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 7baf38add82c593cfa6049d71e9c0775eb64674f
ms.sourcegitcommit: ef6e3ec273b0521e7c79d5c2a4cb4dcba1744e67
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/10/2018
ms.locfileid: "51512820"
---
# <a name="delete-a-policy-based-management-policy"></a>Eliminar una directiva de administración basada en directivas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describe cómo eliminar una directiva de administración basada en directivas en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para eliminar una directiva mediante:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Requiere la pertenencia al rol PolicyAdministratorRole en la base de datos msdb.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-delete-a-policy"></a>Para eliminar una directiva  
  
1.  En el Explorador de objetos, haga clic en el signo más para expandir el servidor que contiene la directiva de administración basada en directivas que desea eliminar.  
  
2.  Haga clic en el signo más para expandir la carpeta **Administración** .  
  
3.  Haga clic en el signo más para expandir la carpeta **Administración de directivas**.  
  
4.  Haga clic en el signo más para expandir la carpeta **Directivas** .  
  
5.  Haga clic con el botón derecho en la directiva que quiere eliminar y seleccione **Eliminar**.  
  
6.  En el cuadro de diálogo **Eliminar objeto** , asegúrese de que está seleccionada la condición correcta y haga clic en **Aceptar**.  
  
  
