---
title: Proteger elementos de origen de datos compartidos | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- shared data sources [Reporting Services]
- data sources [Reporting Services], shared
- security [Reporting Services], data sources
ms.assetid: 7299e498-0a1a-4821-a22a-5199bb773ce0
caps.latest.revision: 35
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e056f5577c2c569e333f2341060862c06d803f6b
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="secure-shared-data-source-items"></a>Proteger elementos de orígenes de datos compartidos
  Puede establecer la seguridad en un origen de datos compartido para habilitar o deshabilitar el acceso a él.  
  
 Un usuario con acceso mínimo a un origen de datos compartido (por ejemplo, el acceso concedido con el rol **Explorador** ) puede ver la lista de informes que usan el elemento, siempre que el usuario también esté autorizado a ver los informes.  
  
 Un usuario con acceso adicional (como el concedido con el rol **Administrador de contenido** ) puede ver y establecer propiedades para el origen de datos compartido.  
  
 Para establecer la seguridad, cree una asignación de roles que especifique la cuenta de usuario o de grupo que tiene acceso al origen de datos compartido. Los usuarios con acceso a un origen de datos compartido pueden cambiar su nombre, descripción, cadena de conexión o información de credenciales.  
  
## <a name="tasks-and-access-to-items"></a>Tareas y acceso a elementos  
 Cuando cree asignaciones de roles, utilice un rol que tenga estas tareas para asignar los permisos apropiados a usuarios y grupos.  
  
|Seleccione esta tarea|Para conceder a los usuarios permiso para|  
|----------------------|---------------------------------|  
|Ver orígenes de datos|Ver el origen de datos compartido en la jerarquía de carpetas. Sin esta tarea, el elemento no está visible para los usuarios y no pueden saber que el origen de datos está disponible.|  
|Administrar orígenes de datos|Ver propiedades que especifican el nombre, la descripción y la información de conexión. Esta tarea también se utiliza para mostrar un origen de datos compartido en la jerarquía de carpetas. Si elige esta tarea, puede omitir la tarea "Ver orígenes de datos".|  
|Establecer la seguridad de elementos individuales|Crear y modificar asignaciones de roles que controlen el acceso al origen de datos compartido. Esta tarea debe utilizarse con las tareas "Ver orígenes de datos" o "Administrar orígenes de datos". De lo contrario, no surte efecto porque el usuario no puede seleccionar el elemento.|  
  
## <a name="see-also"></a>Vea también  
 [Administrar los orígenes de datos de informe](../../reporting-services/report-data/manage-report-data-sources.md)   
 [Carpetas protegidas](../../reporting-services/security/secure-folders.md)   
 [Proteger los informes y recursos](../../reporting-services/security/secure-reports-and-resources.md)   
 [Conceder permisos en un servidor de informes de modo nativo](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)   
 [Almacenar credenciales en un origen de datos de Reporting Services](../../reporting-services/report-data/store-credentials-in-a-reporting-services-data-source.md)  
  
  
