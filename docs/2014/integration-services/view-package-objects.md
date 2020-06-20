---
title: Ver objetos de paquete | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, properties
- properties [Integration Services]
- Package Explorer window [Integration Services]
- packages [Integration Services], properties
- explorer view [Integration Services]
- SSIS packages, properties
- viewing package objects
- SQL Server Integration Services packages, properties
ms.assetid: a85c0245-0a68-4eb0-83b1-9b11df80bd10
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 8ab1a510ec348ca30ffd1b8946b71ab935c0057c
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84972531"
---
# <a name="view-package-objects"></a>Ver objetos de paquete
  En el Diseñador de [!INCLUDE[ssIS](../includes/ssis-md.md)] , la pestaña **Explorador de paquetes** proporciona una vista de explorador del paquete. La vista refleja la jerarquía de contenedores de la arquitectura de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . El contenedor de paquetes se encuentra en la parte superior de la jerarquía y puede expandir el paquete para ver las conexiones, ejecutables, controladores de eventos, proveedores de registro, restricciones de precedencia y variables del paquete.

 Los ejecutables, que son los contenedores y las tareas del paquete, pueden incluir controladores de eventos, restricciones de precedencia y variables. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] admite una jerarquía anidada de contenedores, y los contenedores de bucles For, bucles Foreach y secuencias pueden incluir otros ejecutables.

 Si un paquete incluye un flujo de datos, el **Explorador de paquetes** incluye la tarea Flujo de datos y una carpeta **Componentes** que enumera los componentes de flujo de datos.

 Desde la pestaña **Explorador de paquetes** , puede eliminar objetos en un paquete y obtener acceso a la ventana **Propiedades** para ver las propiedades del objeto.

 El siguiente diagrama muestra una vista de árbol de un paquete simple.

 ![Captura de pantalla de la pestaña Explorador de paquetes](media/packageexplorer.gif "Captura de pantalla de la pestaña Explorador de paquetes")

### <a name="to-view-package-content"></a>Para ver el contenido de los paquetes

-   [Ver objetos de paquete en el Explorador de paquetes](../../2014/integration-services/view-package-objects-in-package-explorer.md)

## <a name="see-also"></a>Consulte también
 [Integration Services las tareas](control-flow/integration-services-tasks.md) [Integration Services](control-flow/integration-services-containers.md) las [restricciones de precedencia](control-flow/precedence-constraints.md) de los contenedores [Integration Services &#40;las variables de&#41; de SSIS](integration-services-ssis-variables.md) [Integration Services &#40;los controladores de eventos&#41; SSIS](integration-services-ssis-event-handlers.md) Integration Services &#40;el registro de&#41; de [SSIS](performance/integration-services-ssis-logging.md)


