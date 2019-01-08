---
title: Transformación Auditar | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.audittrans.f1
helpviewer_keywords:
- environment data in packages [Integration Services]
- Audit transformation
ms.assetid: 8c143682-9c81-4150-83d6-1d9678151d37
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: de3fd2e357d58d77bc82a551ab88f01db2c1c693
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52771277"
---
# <a name="audit-transformation"></a>Auditar, transformación
  La transformación Auditar habilita el flujo de datos en un paquete para incluir datos sobre el entorno en el que se ejecuta el paquete. Por ejemplo, el nombre del paquete, el equipo y el operador se pueden agregar al flujo de datos. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] incluye variables del sistema que proporcionan esta información.  
  
## <a name="system-variables"></a>Variables del sistema  
 En la tabla siguiente se describen las variables del sistema que la transformación Auditar puede usar.  
  
|Variable del sistema|Índice|Descripción|  
|---------------------|-----------|-----------------|  
|`ExecutionInstanceGUID`|0|El GUID que identifica la instancia de ejecución del paquete.|  
|`PackageID`|1|Identificador único del paquete.|  
|`PackageName`|2|Nombre del paquete.|  
|`VersionID`|3|La versión del paquete.|  
|`ExecutionStartTime`|4|La hora a la que se inició la ejecución del paquete.|  
|`MachineName`|5|El nombre del equipo.|  
|`UserName`|6|El nombre de inicio de sesión de la persona que inició el paquete.|  
|`TaskName`|7|El nombre de la tarea Flujos de datos a la que está asociada la transformación Auditar.|  
|**TaskId**|8|El identificador único de la tarea Flujo de datos.|  
  
## <a name="configuration-of-the-audit-transformation"></a>Configuración de la transformación Auditar  
 Para configurar la transformación Auditar debe proporcionar el nombre de una nueva columna de salida que se agregará a la salida de transformación y después asignar la variable del sistema a la columna de salida. Puede asignar una sola variable del sistema a varias columnas.  
  
 Esta transformación tiene una entrada y una salida. No admite una salida de error.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el cuadro de diálogo **Editor de transformación Auditar** , vea [Audit Transformation Editor](../../audit-transformation-editor.md).  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Propiedades comunes](../../common-properties.md)  
  
-   [Propiedades personalizadas de transformación](transformation-custom-properties.md)  
  
 Para más información sobre cómo establecer propiedades, vea [Establecer las propiedades de un componente de flujo de datos](../set-the-properties-of-a-data-flow-component.md).  
  
  
