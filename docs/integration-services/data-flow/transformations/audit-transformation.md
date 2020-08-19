---
description: Auditar, transformación
title: Transformación Auditar | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.audittrans.f1
- sql13.dts.designer.audittransformation.f1
helpviewer_keywords:
- environment data in packages [Integration Services]
- Audit transformation
ms.assetid: 8c143682-9c81-4150-83d6-1d9678151d37
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e04af79dc2020a2273717785fca57aac5e4de451
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88392281"
---
# <a name="audit-transformation"></a>Auditar, transformación

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  La transformación Auditar habilita el flujo de datos en un paquete para incluir datos sobre el entorno en el que se ejecuta el paquete. Por ejemplo, el nombre del paquete, el equipo y el operador se pueden agregar al flujo de datos. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] incluye variables del sistema que proporcionan esta información.  
  
## <a name="system-variables"></a>Variables del sistema  
 En la tabla siguiente se describen las variables del sistema que la transformación Auditar puede usar.  
  
|Variable del sistema|Índice|Descripción|  
|---------------------|-----------|-----------------|  
|**ExecutionInstanceGUID**|0|El GUID que identifica la instancia de ejecución del paquete.|  
|**PackageID**|1|Identificador único del paquete.|  
|**PackageName**|2|Nombre del paquete.|  
|**VersionID**|3|La versión del paquete.|  
|**ExecutionStartTime**|4|La hora a la que se inició la ejecución del paquete.|  
|**MachineName**|5|El nombre del equipo.|  
|**UserName**|6|El nombre de inicio de sesión de la persona que inició el paquete.|  
|**TaskName**|7|El nombre de la tarea Flujos de datos a la que está asociada la transformación Auditar.|  
|**TaskId**|8|El identificador único de la tarea Flujo de datos.|  
  
## <a name="configuration-of-the-audit-transformation"></a>Configuración de la transformación Auditar  
 Para configurar la transformación Auditar debe proporcionar el nombre de una nueva columna de salida que se agregará a la salida de transformación y después asignar la variable del sistema a la columna de salida. Puede asignar una sola variable del sistema a varias columnas.  
  
 Esta transformación tiene una entrada y una salida. No admite una salida de error.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propiedades personalizadas de transformación](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Para más información sobre cómo establecer propiedades, vea [Establecer las propiedades de un componente de flujo de datos](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="audit-transformation-editor"></a>Editor de transformación Auditar
  La transformación Auditar habilita el flujo de datos en un paquete para incluir datos sobre el entorno en el que se ejecuta el paquete. Por ejemplo, el nombre del paquete, el equipo y el operador se pueden agregar al flujo de datos. [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] incluye variables del sistema que proporcionan esta información.  
  
### <a name="options"></a>Opciones  
 **Nombre de la columna de salida**  
 Proporciona el nombre de una nueva columna de salida que contendrá la información de auditoría.  
  
 **Tipo de auditoría**  
 Seleccione una variable del sistema disponible para suministrar la información de auditoría.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**GUID de instancia de ejecución**|Inserte el GUID que identifica exclusivamente la instancia de ejecución del paquete.|  
|**Id. de paquete**|Inserte el GUID que identifica exclusivamente el paquete.|  
|**Nombre del paquete**|Inserte el nombre del paquete.|  
|**Id. de la versión**|Inserte el GUID que identifica exclusivamente la versión del paquete.|  
|**Hora de inicio de ejecución**|Inserte la hora en la que se iniciará la ejecución del paquete.|  
|**Nombre de la máquina**|Inserte el nombre del equipo en el que se inició el paquete.|  
|**Nombre de usuario**|Inserte el nombre de inicio de sesión del usuario que inició el paquete.|  
|**Nombre de la tarea**|Inserte el nombre de la tarea Flujo de datos con la que está asociada la transformación Auditar.|  
|**Identificador de tarea**|Inserte el GUID que identifica exclusivamente la tarea Flujo de datos con la que está asociada la transformación Auditar.|  
  
  
