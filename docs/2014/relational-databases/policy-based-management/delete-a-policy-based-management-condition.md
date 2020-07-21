---
title: Eliminación de una condición de administración basada en directivas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, delete policy conditions
ms.assetid: e04148b8-f6dd-4c50-a5ef-c650b71dbf4d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 9e34188156c8c98c6c3da9cb7f641739d96a926f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85068885"
---
# <a name="delete-a-policy-based-management-condition"></a>Eliminar una condición de administración basada en directivas
  En este tema se describe cómo eliminar una condición de administración basada en directivas en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para eliminar una condición mediante:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permisos  
 Requiere la pertenencia al rol PolicyAdministratorRole en la base de datos msdb.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-delete-a-condition"></a>Para eliminar una condición  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor que contiene la condición que desea eliminar.  
  
2.  Haga clic en el signo más para expandir la carpeta **Administración** .  
  
3.  Haga clic en el signo más para expandir la carpeta **Administración de directivas**.  
  
4.  Haga clic en el signo más para expandir la carpeta **Condiciones** .  
  
5.  Haga clic con el botón derecho en la condición que quiera eliminar y, después, seleccione **Eliminar**.  
  
6.  En el cuadro de diálogo **Eliminar objeto** , asegúrese de que está seleccionada la condición correcta y haga clic en **Aceptar**.  
  
  
