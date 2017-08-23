---
title: Tarea notificar al operador | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.notifyoperatortask.f1
helpviewer_keywords:
- Notify Operator task
- notifications [Integration Services]
- SQL Server Agent [Integration Services]
ms.assetid: 6c816c68-c6d6-44e4-bb34-c8e060a958a1
caps.latest.revision: 43
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fb791195dccb44add2d1b196e33e03d3a45d7049
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="notify-operator-task"></a>Notificar al operador, tarea
  La tarea Notificar al operador envía mensajes de notificación a los operadores del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Un operador del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es un alias para una persona o grupo que puede recibir notificaciones electrónicas. Para obtener más información sobre operadores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vea [Operadores](http://msdn.microsoft.com/library/38e8488f-2669-4cea-b9c3-5f394a663678).  
  
 Si usa la tarea Notificar al operador, un paquete puede notificar a uno o más operadores a través de correo electrónico, buscapersonas o **net send**. Es posible notificar a cada operador por distintos métodos. Por ejemplo, se notifica al Operador A por correo electrónico y mediante buscapersonas, y al Operador B mediante buscapersonas y **net send**. Los operadores que reciben notificaciones de la tarea deben ser miembros de la colección **OperatorNotify** en la tarea Notificar al operador.  
  
 La tarea Notificar al operador es la única tarea de mantenimiento de la base de datos que no encapsula una instrucción Transact-SQL o un comando DBCC.  
  
## <a name="configuration-of-the-notify-operator-task"></a>Configuración de la tarea Notificar al operador  
 Puede establecer propiedades a través del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] . Esta tarea se encuentra en la sección **Tareas del plan de mantenimiento** del **Cuadro de herramientas** , en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el tema siguiente:  
  
-   [Tarea Notificar al operador &#40;Plan de mantenimiento&#41;](../../relational-databases/maintenance-plans/notify-operator-task-maintenance-plan.md)  
  
 Para obtener más información sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
  
