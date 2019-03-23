---
title: Editor de la tarea FTP (página General) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.ftptask.general.f1
helpviewer_keywords:
- File Transfer Protocol Task Editor
ms.assetid: 28b46fdd-b04a-4f97-a99f-883f5735a6d9
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1b64b1f8511c9d079118881a9862eee11fdb636d
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58388743"
---
# <a name="ftp-task-editor-general-page"></a>Editor de la tarea FTP (página General)
  Use la página **General** del cuadro de diálogo **Editor de la tarea FTP** para especificar el administrador de conexiones FTP que se conecta al servidor FTP con el que se comunica la tarea. También puede asignar un nombre a la tarea FTP y describirla.  
  
 Para más información sobre esta tarea, vea [Tarea FTP](control-flow/ftp-task.md).  
  
## <a name="options"></a>Opciones  
 **FtpConnection**  
 Seleccione un administrador de conexiones FTP existente o haga clic en \<**Nueva conexión...**> para crear uno nuevo.  
  
> [!IMPORTANT]  
>  El administrador de conexiones FTP solo admite la autenticación anónima y la autenticación básica. No es compatible con la autenticación de Windows.  
  
 **Temas relacionados**: [Administrador de conexiones FTP](connection-manager/ftp-connection-manager.md), [Editor del administrador de conexiones FTP](../../2014/integration-services/ftp-connection-manager-editor.md)  
  
 **StopOnFailure**  
 Indica si la tarea FTP termina si se produce un error en una opción FTP.  
  
 **Name**  
 Proporcione un nombre único para la tarea FTP. Este nombre se utiliza como etiqueta en el icono de tarea.  
  
> [!NOTE]  
>  Los nombres de tarea deben ser únicos en un paquete.  
  
 **Descripción**  
 Escriba una descripción de la tarea FTP.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de la tarea FTP &#40;página Transferencia de archivos&#41;](../../2014/integration-services/ftp-task-editor-file-transfer-page.md)   
 [Página Expresiones](expressions/expressions-page.md)  
  
  
