---
title: Eliminar automáticamente un trabajo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- dropping jobs
- SQL Server Agent jobs, removing
- automatic job removal
- jobs [SQL Server Agent], deleting
- deleting jobs
- removing jobs
ms.assetid: 92dbb6da-5919-4bde-9354-d454e9ea3da0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 42538ac6566b70105fd183da1cadd00f7fd0c13b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85011789"
---
# <a name="automatically-delete-a-job"></a>Automatically Delete a Job
  En este tema se describe cómo configurar el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para que elimine los trabajos automáticamente cuando se realizan correctamente, con error o se completan mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o objetos de administración de SQL Server.  
  
 Estas respuestas permiten a los administradores de las bases de datos saber cuándo se completan los trabajos y con qué frecuencia se ejecutan. Algunas respuestas de trabajos típicas son:  
  
-   Notificar al operador mediante correo electrónico, localizador electrónico o un mensaje de **net send** .  
  
     Use una de estas respuestas de trabajo si el operador debe realizar una acción de seguimiento. Por ejemplo, si un trabajo de copia de seguridad se realiza correctamente, se debe notificar de ello al operador para que quite la cinta de copia de seguridad y la guarde en un lugar seguro.  
  
-   Escribir un mensaje de evento en el registro de aplicación Windows.  
  
     Puede utilizar esta respuesta solo para trabajos con errores.  
  
-   Eliminar automáticamente el trabajo.  
  
     Utilice esta respuesta de trabajo si está seguro de que no necesita volver a ejecutar este trabajo.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para especificar respuestas de trabajos, utilizando:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [objetos de administración de SQL Server](#SMO)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
 Para obtener información detallada, vea [Implementar la seguridad del Agente SQL Server](implement-sql-server-agent-security.md).  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-automatically-delete-a-job"></a>Para eliminar automáticamente un trabajo  
  
1.  En el **Explorador de objetos**, conéctese a una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] y expándala.  
  
2.  Expanda **Agente SQL Server**, expanda **Trabajos**, haga clic con el botón derecho en el trabajo que desee editar y haga clic en **Propiedades**.  
  
3.  Seleccione la página **Notificaciones** .  
  
4.  Active **Eliminar el trabajo automáticamente**y elija una de las opciones siguientes:  
  
    -   Haga clic en **Cuando el trabajo se realiza correctamente** para eliminar el estado del trabajo cuando se ha completado correctamente.  
  
    -   Haga clic en **Cuando se produce un error en el trabajo** para eliminar el trabajo cuando no se ha completado correctamente.  
  
    -   Haga clic en **Si el trabajo termina** para eliminar el trabajo independientemente del estado de finalización.  
  
##  <a name="using-sql-server-management-objects"></a><a name="SMO"></a>Usar Objetos de administración de SQL Server  
 **Para eliminar automáticamente un trabajo**  
  
 Use la propiedad `DeleteLevel` de la clase `Job` mediante el lenguaje de programación que desee, como Visual Basic, Visual C# o PowerShell. Para más información, consulte [Objetos de administración de SQL Server (SMO)](https://msdn.microsoft.com/library/ms162169.aspx).  
  
  
