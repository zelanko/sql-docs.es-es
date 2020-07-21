---
title: Editor de la tarea transferir procedimientos almacenados principales (página general) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferstoredprocedurestask.general.f1
helpviewer_keywords:
- Transfer Stored Procedures Task Editor
ms.assetid: fa1abd4c-e2be-427f-be53-860e49c97227
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8a25a5c9c6ed3802e21ac522e94163ce5fb9e8c0
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85420512"
---
# <a name="transfer-master-stored-procedures-task-editor-general-page"></a>Editor de la tarea Transferir procedimientos almacenados principales (Página General)
  Use la página **General** del cuadro de diálogo **Editor de la tarea Transferir procedimientos almacenados principales** para asignar un nombre a la tarea de transferencia de procedimientos almacenados master y describirla. Para obtener más información acerca de esta tarea, vea [Transfer Master Stored Procedures Task](control-flow/transfer-master-stored-procedures-task.md).  
  
> [!NOTE]  
>  Esta tarea transfiere solo los procedimientos almacenados definidos por el usuario que pertenecen a **dbo** desde una base de datos **master** del servidor de origen a una base de datos **master** del servidor de destino. A los usuarios se les debe conceder el permiso CREATE PROCEDURE en la base de datos **maestra** del servidor de destino o deben ser miembros del rol fijo del servidor **sysadmin** del servidor de destino para crear procedimientos almacenados en dicho servidor.  
  
## <a name="options"></a>Opciones  
 **Nombre**  
 Escriba un nombre único para la tarea de transferencia de procedimientos almacenados principales. Este nombre se utiliza como etiqueta en el icono de tarea.  
  
> [!NOTE]  
>  Los nombres de tarea deben ser únicos en un paquete.  
  
 **Descripción**  
 Escriba una descripción de la tarea de transferencia de procedimientos almacenados principales.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Tareas de Integration Services](control-flow/integration-services-tasks.md)   
 [Editor de la tarea transferir procedimientos almacenados principales &#40;página procedimientos almacenados&#41;](../../2014/integration-services/transfer-master-stored-procedures-task-editor-stored-procedures-page.md)   
 [Página Expresiones](expressions/expressions-page.md)  
  
  
