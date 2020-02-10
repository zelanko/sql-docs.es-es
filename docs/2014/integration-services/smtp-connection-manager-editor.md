---
title: Editor del administrador de conexiones SMTP | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.smtpconnection.f1
helpviewer_keywords:
- SMTP Connection Manager Editor
ms.assetid: 2693de0d-b04d-4325-a856-ce667d2b8aa1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 527c8f647c963c2c1c03171eeb154a790ab1994a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66055559"
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
  
 **Usar autenticación de Windows**  
 Seleccione esta opción para enviar correo electrónico mediante un servidor SMTP que utiliza Autenticación de Windows para autenticar el acceso al servidor.  
  
> [!IMPORTANT]  
>  El administrador de conexiones SMTP solo es compatible con la autenticación anónima y la autenticación de Windows. No admite la autenticación básica.  
  
> [!NOTE]  
>  Al usar Microsoft Exchange como servidor SMTP, es posible que deba establecer **usar autenticación de Windows** en `True`. Es posible que los servidores Exchange estén configurados para no permitir conexiones SMTP no autenticadas.  
  
 **Habilitar Capa de sockets seguros (SSL)**  
 Seleccione esta opción para cifrar comunicación mediante Capa de sockets seguros (SSL) al enviar mensajes de correo electrónico.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  
