---
title: Proteger carpetas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- high-security folders [Reporting Services]
- low-security folders
- folders [Reporting Services], security
- security [Reporting Services], folders
ms.assetid: 0fd91f77-0143-476b-9af0-87293be78e44
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 201facc6500339eb8804f3de22d25337dcc07089
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66101707"
---
# <a name="secure-folders"></a>Proteger carpetas
  La seguridad de las carpetas es fundamental para proteger todo el contenido de un servidor de informes. Puesto que la seguridad se hereda en toda la estructura de carpetas, puede designar secciones grandes o pequeñas de la jerarquía de carpetas para permitir ciertos tipos de acceso.  
  
 Las carpetas de alta seguridad se pueden utilizar para almacenar informes confidenciales o como áreas de ensayo; por ejemplo, puede utilizar una carpeta para probar informes antes de moverlos a la ubicación final. Para controlar el acceso a esta área, puede definir una asignación de roles que solo permita a los autores de los informes agregar y eliminar elementos, y una segunda asignación de roles que permita a los evaluadores ejecutar informes, pero no agregar ni quitar elementos. Puesto que las asignaciones de roles están definidas explícitamente para evaluadores y autores de informes, ningún otro usuario (excepto los administradores del sistema local) puede tener acceso a la carpeta.  
  
 Las carpetas de baja seguridad pueden utilizarse para almacenar informes a los que desea tener acceso con facilidad.  
  
 La seguridad de las carpetas constituye la base de la seguridad de nivel de elemento, comenzando con el nodo raíz de la jerarquía de carpetas del servidor de informes, la carpeta Inicio. Puesto que la seguridad se hereda, es aconsejable establecer una directiva de seguridad bastante restrictiva en la carpeta Inicio. Usar el rol **Explorador** en las asignaciones de roles de la carpeta particular es exactamente igual que proporcionar acceso de solo vista.  
  
## <a name="tasks-and-folder-access"></a>Tareas y acceso a carpetas  
 Cuando cree asignaciones de roles para carpetas, tenga en cuenta las tareas que figuran en la siguiente tabla.  
  
|Seleccione esta tarea|Para conceder permiso para|  
|----------------------|---------------------------|  
|Ver carpetas|Ver la jerarquía de carpetas y las propiedades de solo lectura que indican cuándo se creó y modificó la carpeta.<br /><br /> Los usuarios no pueden ver elementos en la carpeta a menos que se asignan a roles que también se incluyen las siguientes tareas: "Ver informes", "Modelos de vista", "Ver recursos" y "Ver orígenes de datos".|  
|Administrar carpetas|Ver las propiedades de la carpeta, cambiar el nombre o la descripción, o bien mover la carpeta a otra ubicación. Esta tarea permite a los usuarios crear carpetas.|  
|Administrar informes|Agregar informes del sistema de archivos a una carpeta, así como publicar informes desde el Diseñador de informes al servidor de informes.|  
|Administrar orígenes de datos|Agregar nuevos elementos de orígenes de datos compartidos a una carpeta y cambiar los orígenes de datos compartidos existentes.|  
|Establecer la seguridad de elementos individuales|Puede definir y modificar las asignaciones de roles que controlan el acceso a la carpeta. Esta tarea debe utilizarse con "Ver carpetas" o "Administrar carpetas". De lo contrario, no surtirá efecto, ya que el usuario no podrá seleccionar el elemento.|  
  
## <a name="see-also"></a>Vea también  
 [Proteger informes y recursos](secure-reports-and-resources.md)   
 [Proteger elementos de orígenes de datos compartidos](secure-shared-data-source-items.md)   
 [Concesión de permisos en un servidor de informes en modo nativo](granting-permissions-on-a-native-mode-report-server.md)  
  
  
