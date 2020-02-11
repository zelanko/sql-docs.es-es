---
title: Designar un operador para notificaciones de error | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, operators
- fail-safe operator [SQL Server]
- jobs [SQL Server Agent], operators
- notifications [SQL Server], job status
ms.assetid: 0f4eb513-5c0a-4523-974e-e85c1deeb57f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 54ec71df8efab1f60bfb7a5b9af448705e349d28
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68211424"
---
# <a name="designate-a-fail-safe-operator"></a>Designar un operador para notificaciones de error
  Un operador para notificaciones de error es un usuario que recibe la alerta si ésta no llega al operador designado. En este tema se describe cómo establecer un operador para notificaciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] error para recibir notificaciones [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] de alerta [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]del agente en mediante.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para designar un operador para notificaciones de error, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Las opciones buscapersonas y **net send** se quitarán del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente en una versión futura de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite utilizar estas características en los nuevos trabajos de programación y planee modificar las aplicaciones que actualmente las utilizan.  
  
-   Tenga en cuenta que deberá configurar el Agente SQL Server para que utilice el Correo electrónico de base de datos para enviar a los operadores notificaciones por correo electrónico o buscapersonas. Para obtener más información, vea el tema sobre [asignación de alertas a un operador](assign-alerts-to-an-operator.md).  
  
-   
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ofrece un método gráfico sencillo para administrar trabajos y es el método recomendado para crear y administrar la infraestructura de trabajo.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** pueden designar operadores para notificaciones de error.  
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-designate-a-fail-safe-operator"></a>Para designar un operador para notificaciones de error  
  
1.  En el **Explorador de objetos** , haga clic en el signo más para expandir el servidor que contiene el operador del Agente SQL Server que desea designar como operador para notificaciones de error.  
  
2.  Haga clic con el botón derecho en **Agente SQL Server** y seleccione **propiedades**.  

3.  En el cuadro de diálogo **propiedades de Agente SQL Server-**_Server_name_ , en **seleccionar una página**, seleccione **sistema de alerta**.  
 
4.  En **Operador para notificaciones de error**, seleccione **Habilitar operador para notificaciones de error**.  
  
5.  En la lista **Operador** , seleccione el operador que desee que sea el operador para notificaciones de error.  
  
6.  Active alguna o la totalidad de las siguientes casillas para especificar cómo se notificará al operador: **Correo electrónico**, **Buscapersonas**o **Net send**.  
  
7.  Cuando termine, haga clic en **Aceptar**.  
  
  
