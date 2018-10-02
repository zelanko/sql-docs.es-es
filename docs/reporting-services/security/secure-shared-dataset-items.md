---
title: Proteger los elementos de un conjunto de datos compartido | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: security
ms.topic: conceptual
ms.assetid: 08e6d8b5-d88c-4ed2-9c05-55c757e00014
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 830955375dec473f7587ef33c1e7f6927df530b2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47725563"
---
# <a name="secure-shared-dataset-items"></a>Proteger los elementos de un conjunto de datos compartido
  En un servidor de informes, los elementos de un conjunto de datos compartido se pueden usar en varios informes. Puede proteger los conjuntos de datos compartidos para controlar el grado de acceso que los usuarios tienen. De forma predeterminada, solo los usuarios que son miembros del grupo integrado **Administradores** pueden ver los conjuntos de datos compartidos, modificar las propiedades, habilitar el almacenamiento en caché, crear planes de actualización de caché y eliminar elementos. Para todos los demás usuarios se deben crear asignaciones de roles que permitan el acceso a un conjunto de datos compartido.  
  
 Para establecer la seguridad, cree una asignación de roles que especifique la cuenta de usuario o de grupo que tiene acceso al conjunto de datos compartido.  
  
## <a name="role-based-access-to-shared-datasets"></a>Acceso basado en roles a los conjuntos de datos compartidos  
 Para conceder acceso a conjuntos de datos compartidos, puede permitir que los usuarios hereden las asignaciones de roles existentes en una carpeta primaria o creen una nueva asignación de rol en el propio elemento.  
  
 Las asignaciones de roles predeterminados que permiten agregar, eliminar, modificar propiedades de elementos y ver los informes relacionados y los orígenes de datos compartidos para los conjuntos de datos compartidos son Administrador de contenido, Mis Informes y Editor. Para modificar una definición de conjunto de datos compartido, utilice el Generador de informes o el Administrador de contenido de las asignaciones de roles predeterminados.  
  
 Dado que las asignaciones de roles se suelen heredar de un nodo primario, una carpeta que tenga habilitada la tarea **Ver informes** pasa ese permiso a los conjuntos de datos compartidos e informes de la carpeta.  
  
 Para proporcionar más control sobre los conjuntos de datos compartidos y los resultados de sus consultas, configure la seguridad en el nivel de los elementos en el elemento de conjunto de datos compartido o guarde los conjuntos de datos compartidos en una carpeta y configure la seguridad en el nivel de los elementos en la carpeta.  
  
## <a name="shared-dataset-parameters"></a>Parámetros de los conjuntos de datos compartidos  
 Los parámetros de los conjuntos de datos compartidos no se pueden utilizar para restringir los datos de usuarios concretos. El propósito de los parámetros de los conjuntos de datos compartidos es proporcionar una manera de especificar qué datos incluir cuando se procesa el conjunto de datos compartido. En el servidor de informes, no puede proteger los valores para un parámetro de un conjunto de datos compartido.  
  
 En la definición del conjunto de datos compartido, puede marcar los parámetros como de solo lectura y especificar los valores predeterminados. Los parámetros que están marcados como de solo lectura no se pueden invalidar en el servidor. Por ejemplo, en un plan de actualización de caché para un conjunto de datos compartido, no puede especificar los valores para los parámetros de solo lectura. Si los parámetros de un conjunto de datos compartido incluyen expresiones que hacen referencia a la colección global de usuarios o tienen alguna otra dependencia del usuario, no puede crear un plan de actualización de caché para el conjunto de datos compartido.  
  
## <a name="tasks-access-to-items-and-default-roles"></a>Tareas, acceso a los elementos y roles predeterminados  
 Los conjuntos de datos compartidos siguen el mismo modelo de seguridad que los informes. Para proporcionar a un usuario permiso para acciones concretas, elija un rol que incluya la tarea correspondiente que incluya permisos. En la siguiente tabla se enumeran las tareas y las acciones que incluyen.  
  
|Seleccione esta tarea|Para conceder a los usuarios permiso para|Roles predeterminados que incluyen la tarea|  
|----------------------|---------------------------------|-----------------------------------------|  
|Ver informes|Ver el elemento del conjunto de datos compartido en la jerarquía de carpetas. Sin esta tarea, el elemento no está visible para los usuarios y podrían no saber que el conjunto de datos está disponible.|Browser<br /><br /> Administrador de contenido<br /><br /> Generador de informes<br /><br /> Mis informes|  
|Administrar informes|Ver propiedades que especifican el nombre, la descripción y la información de conexión. Esta tarea también se utiliza para mostrar un elemento de conjunto de datos compartido en la jerarquía de carpetas. Si elige esta tarea, puede omitir la tarea "Ver informes".|Administrador de contenido<br /><br /> publicador<br /><br /> Mis informes|  
|Usar informes|Ver la definición del conjunto de datos compartido.|Administrador de contenido<br /><br /> Generador de informes|  
|Establecer la seguridad de elementos individuales|Crear y modificar asignaciones de roles que controlen el acceso al conjunto de datos compartido. Esta tarea debe utilizarse con las tareas "Ver informes" o "Administrar informes". De lo contrario, no surte efecto porque el usuario no puede seleccionar el elemento.|Administrador de contenido|  
  
 Para más información, vea [Tareas de nivel de elemento](../../reporting-services/security/tasks-and-permissions-item-level-tasks.md) y [Roles predefinidos](../../reporting-services/security/role-definitions-predefined-roles.md).  
  
## <a name="see-also"></a>Ver también  
 [Administrar conjuntos de datos compartidos](../../reporting-services/report-data/manage-shared-datasets.md)   
 [Proteger carpetas](../../reporting-services/security/secure-folders.md)   
 [Proteger informes y recursos](../../reporting-services/security/secure-reports-and-resources.md)   
 [Conceder permisos en un servidor de informes en modo nativo](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)   
 [Concesión de permisos en un servidor de informes en modo nativo](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
  
