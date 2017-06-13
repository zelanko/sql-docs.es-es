---
title: rsAccessedDenied - Error de Reporting Services | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- rsAccessDenied error
ms.assetid: 2f76b1bf-96a2-4755-b76b-84e933220efc
caps.latest.revision: 21
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7ece42006b7022bd3fa031cd95ef97767055ad53
ms.contentlocale: es-es
ms.lasthandoff: 06/13/2017

---
# <a name="rsaccesseddenied---reporting-services-error"></a>rsAccessedDenied - Error de Reporting Services
  El error [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] rsAccessedDenied **en** se produce cuando un usuario no dispone de permiso para realizar una acción. Por ejemplo, el usuario no dispone de una asignación de rol que le permita abrir un informe o no abrió el explorador con los permisos necesarios.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** Modo nativo de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] &#124; Modo de SharePoint|  
  
-   Si el error se produce al obtener acceso al servidor de informes directamente a través de una dirección URL, la excepción se asigna a un error de HTTP 401.  
  
-   Si el error se produce al utilizar el Administrador de informes u otra herramienta, aparece en una página de error.  
  
-   Si el error se produce durante una operación programada, suscripción o entrega, aparecerá solamente en el archivo de registro del servidor de informes.  
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|**Nombre del producto**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**Identificador del evento**|en|  
|**Origen del evento**|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings|  
|**Componente**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|**Texto del mensaje**|Los permisos otorgados al usuario 'miDominio\miCuenta' son insuficientes para realizar esta operación. (rsAccessDenied) (ReportingServicesLibrary)|  
  
## <a name="user-action"></a>Acción del usuario  
 El permiso para obtener acceso al contenido y a las operaciones del servidor de informes se concede mediante asignaciones de roles. En una nueva instalación, solo los administradores locales tienen acceso a un servidor de informes. Para conceder acceso a otros usuarios, el administrador local debe crear una asignación de roles que especifique una cuenta de grupo o usuario de dominio, uno o más roles que definan las tareas que el usuario puede realizar y un ámbito (normalmente la carpeta Inicio o el nodo raíz de la jerarquía de carpetas del servidor de informes). Puede usar el Administrador de informes para crear las asignaciones de roles. Para obtener más información, busque "Asignaciones de roles" en los Libros en pantalla de SQL Server.  
  
 Este error también se produce por la administración local del servidor de informes. Para obtener más información, vea [Configurar un servidor de informes en modo nativo para la administración local &#40;SSRS&#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
## <a name="see-also"></a>Vea también  
 [Asignaciones de roles](../../reporting-services/security/role-assignments.md)   
 [Conceder permisos en un servidor de informes en modo nativo](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)   
 [Roles y permisos &#40;Reporting Services&#41;](../../reporting-services/security/roles-and-permissions-reporting-services.md)  
  
  
