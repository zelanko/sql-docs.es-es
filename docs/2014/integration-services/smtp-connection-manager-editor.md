---
title: Editor del Administrador de conexiones SMTP | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.smtpconnection.f1
helpviewer_keywords:
- SMTP Connection Manager Editor
ms.assetid: 2693de0d-b04d-4325-a856-ce667d2b8aa1
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 03e02d95d9f4ba358c85b0c90f4c5ab1b2029e63
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48118588"
---
# <a name="smtp-connection-manager-editor"></a>Editor del administrador de conexiones SMTP
  Use el cuadro de diálogo **Editor del administrador de conexiones SMTP** para especificar un servidor de protocolo simple de transferencia de correo (SMTP).  
  
 Para obtener más información acerca del administrador de conexiones SMTP, vea [SMTP Connection Manager](connection-manager/smtp-connection-manager.md).  
  
## <a name="options"></a>Opciones  
 **Nombre**  
 Proporcione un nombre único para el administrador de conexiones.  
  
 **Descripción**  
 Describa el administrador de conexiones. Como método recomendado, describa el administrador de conexiones desde el punto de vista de su propósito, para que los paquetes estén autodocumentados y sean más fáciles de mantener.  
  
 **Servidor SMTP**  
 Proporcione el nombre del servidor SMTP.  
  
 **Utilizar autenticación de Windows**  
 Seleccione esta opción para enviar correo electrónico mediante un servidor SMTP que utiliza Autenticación de Windows para autenticar el acceso al servidor.  
  
> [!IMPORTANT]  
>  El administrador de conexiones SMTP solo es compatible con la autenticación anónima y la autenticación de Windows. No admite la autenticación básica.  
  
> [!NOTE]  
>  Cuando se usa Microsoft Exchange como servidor SMTP, es posible que deba establecer **utilizar autenticación de Windows** a `True`. Es posible que los servidores Exchange estén configurados para no permitir conexiones SMTP no autenticadas.  
  
 **Habilitar capa de sockets seguros (SSL)**  
 Seleccione esta opción para cifrar comunicación mediante Capa de sockets seguros (SSL) al enviar mensajes de correo electrónico.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  
