---
title: Elementos protegibles | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- securable items [Reporting Services]
- roles [Reporting Services], securable items
- security [Reporting Services], securable items listed
- role-based security [Reporting Services], securable items
ms.assetid: 27f58d4c-5c7b-4947-af5b-0f1fa60faf5f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4c5c4d515ebe6aa9b4b8120ae909f07dccc74de0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66101697"
---
# <a name="securable-items"></a>Elementos protegibles
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa la seguridad basada en roles para controlar el acceso a los elementos que se almacenan en un servidor de informes. Cuando concede un acceso de usuario a un servidor de informes, normalmente lo hace creando un par de asignaciones de roles:  
  
-   En el nivel de sitio  
  
-   En Inicio, que es el nodo raíz de la jerarquía de carpetas del servidor de informes  
  
 La seguridad se hereda dentro de la jerarquía de carpetas del servidor de informes. La creación de asignaciones de roles en el nivel de sitio y en la carpeta Inicio establece la herencia de permisos que se extiende a todos los elementos y operaciones en un servidor de informes.  
  
 Se puede invalidar la herencia de permisos definiendo la seguridad de elementos individuales. Entre los elementos que se pueden proteger individualmente se incluyen los siguientes:  
  
-   Carpetas  
  
-   Informes  
  
-   Modelos de informe  
  
-   Recursos  
  
-   Orígenes de datos compartidos  
  
-   Conjuntos de datos compartidos  
  
 Otras construcciones, como programaciones y suscripciones, no se protegen de forma explícita. Las programaciones y suscripciones operan en el contexto de seguridad de un informe.  
  
## <a name="item-descriptions"></a>Descripciones de elementos  
 La siguiente tabla muestra los elementos protegibles y describe sus características.  
  
|Elemento|Características|  
|----------|---------------------|  
|Carpetas|La seguridad de las carpetas se aplica a la carpeta en sí y a los elementos que contiene. La carpeta Inicio es el nodo raíz de la jerarquía de carpetas. La seguridad que establezca para esta carpeta determinará la configuración de seguridad inicial de todas las carpetas, informes, recursos y orígenes de datos compartidos subordinados en la jerarquía de carpetas. Para obtener más información, vea [Proteger carpetas](secure-folders.md).<br /><br /> Mis informes es una carpeta especial que se protege mediante una asignación de roles implícita basada en un rol dedicado. Para obtener más información, vea [Proteger Mis informes](secure-my-reports.md).|  
|Informes|Los informes y los informes vinculados se pueden proteger con el fin de controlar la gama de acciones que los usuarios pueden realizar, como cambiar las propiedades de un determinado informe.<br /><br /> El historial del informe se protege a través del informe que contiene el historial. No se pueden proteger instantáneas individuales dentro del historial del informe.<br /><br /> Para obtener más información sobre la seguridad de los informes, vea [Proteger informes y recursos](secure-reports-and-resources.md).|  
|Modelos de informe|Puede especificar una asignación de roles para todo el modelo de informe o parte de él. Puesto que los modelos de informe pueden ser bastante extensos, es posible que desee proteger los elementos del modelo que se asignan a datos confidenciales.|  
|Recursos|Los recursos se pueden proteger para controlar el acceso al recurso en sí y a sus propiedades.<br /><br /> Solo se pueden proteger como elementos individuales los recursos independientes. Los recursos que estén incrustados en un informe no se pueden proteger independientemente de dicho informe.<br /><br /> Para obtener más información sobre la seguridad de los recursos, vea [Proteger informes y recursos](secure-reports-and-resources.md).|  
|Orígenes de datos compartidos|Los orígenes de datos compartidos se pueden proteger para limitar el acceso al elemento y sus páginas de propiedades. Para obtener más información, vea [Proteger elementos de orígenes de datos compartidos](secure-shared-data-source-items.md).|  
|Conjuntos de datos compartidos|Los conjuntos de datos compartidos se pueden proteger para controlar el intervalo de acciones que los usuarios pueden realizar, como ver o cambiar la definición, o cambiar las propiedades de un conjunto de datos compartido determinado.<br /><br /> Para obtener más información, vea [Proteger los elementos de un conjunto de datos compartido](secure-shared-dataset-items.md).|  
  
## <a name="see-also"></a>Vea también  
 [Conceder permisos en un servidor de informes en modo nativo](granting-permissions-on-a-native-mode-report-server.md)   
 [Crear, eliminar o modificar un rol &#40;Management Studio&#41;](role-definitions-create-delete-or-modify.md)   
 [Conceder a un usuario acceso a un servidor de informes &#40;Administrador de informes&#41;](grant-user-access-to-a-report-server.md)   
 [Modificar o eliminar una asignación de roles &#40;Administrador de informes&#41;](role-assignments-modify-or-delete.md)  
  
  
