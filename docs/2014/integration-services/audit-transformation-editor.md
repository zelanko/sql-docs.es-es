---
title: Editor de transformación auditar | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.audittransformation.f1
helpviewer_keywords:
- Audit Transformation Editor
ms.assetid: 32786a34-5870-4fde-83c7-ec74d62404b8
caps.latest.revision: 12
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f0ec690b0c1b90ffc01c5bf275769658c72ffc99
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37148356"
---
# <a name="audit-transformation-editor"></a>Editor de transformación Auditar
  La transformación Auditar habilita el flujo de datos en un paquete para incluir datos sobre el entorno en el que se ejecuta el paquete. Por ejemplo, el nombre del paquete, el equipo y el operador se pueden agregar al flujo de datos. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] incluye variables del sistema que proporcionan esta información.  
  
 Para obtener más información acerca de la transformación Auditar, vea [Audit Transformation](data-flow/transformations/audit-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Nombre de la columna de salida**  
 Proporciona el nombre de una nueva columna de salida que contendrá la información de auditoría.  
  
 **Tipo de auditoría**  
 Seleccione una variable del sistema disponible para suministrar la información de auditoría.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**GUID de instancia de ejecución**|Inserte el GUID que identifica exclusivamente la instancia de ejecución del paquete.|  
|**Id. de paquete**|Inserte el GUID que identifica exclusivamente el paquete.|  
|**Nombre del paquete**|Inserte el nombre del paquete.|  
|**Id. de versión**|Inserte el GUID que identifica exclusivamente la versión del paquete.|  
|**Hora de inicio de ejecución**|Inserte la hora en la que se iniciará la ejecución del paquete.|  
|**Nombre de equipo**|Inserte el nombre del equipo en el que se inició el paquete.|  
|**Nombre de usuario.**|Inserte el nombre de inicio de sesión del usuario que inició el paquete.|  
|**Nombre de tarea**|Inserte el nombre de la tarea Flujo de datos con la que está asociada la transformación Auditar.|  
|**Id. de tarea**|Inserte el GUID que identifica exclusivamente la tarea Flujo de datos con la que está asociada la transformación Auditar.|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  
