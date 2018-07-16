---
title: Essentials de paquetes SSIS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- package requirements
ms.assetid: b0c86c35-e3d3-4724-9a96-4087e9d74bf3
caps.latest.revision: 27
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a34b86dd370850f61a931aa640df7fb9999d2c08
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37225845"
---
# <a name="ssis-package-essentials"></a>Fundamentos de los paquetes de SSIS
  Un paquete es el objeto que implementa la funcionalidad de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para extraer, transformar y cargar datos. Un paquete se crea utilizando el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] en [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. También puede crear un paquete ejecutando el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o el Asistente para proyectos de conexiones de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Para obtener más información, [crear paquetes en SQL Server Data Tools](create-packages-in-sql-server-data-tools.md) en el Diseñador SSIS y [Asistente para importar proyectos](../../2014/integration-services/import-project-wizard.md).  
  
 Un paquete básico incluye los elementos siguientes:  
  
 **Elementos de flujo de control**  
 Estos elementos necesarios realizan varias funciones, proporcionan estructura y controlan el orden en el que se ejecutan los elementos. Los principales elementos de flujo de control son las tareas, los contenedores y restricciones de precedencia. Es necesario que haya por lo menos un elemento de flujo de control en un paquete.  
  
 Para más información, consulte [Control Flow](control-flow/control-flow.md).  
  
 **Elementos de flujo de datos**  
 Estos elementos opcionales extraen, modifican y cargan datos en los orígenes de datos. Los principales elementos de un flujo de datos son orígenes, transformaciones y destinos. No es necesario que haya en este caso elementos de flujo de datos en el paquete.  
  
 Para más información, consulte [Data Flow](data-flow/data-flow.md).  
  
 Para obtener un ejemplo de cómo crear un paquete básico, consulte [lección 1: crear el proyecto y el paquete básico](lesson-1-create-a-project-and-basic-package-with-ssis.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Crear paquetes en herramientas de datos de SQL Server](create-packages-in-sql-server-data-tools.md)  
  
-   [Agregar o eliminar tareas o contenedores en un flujo de control](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  
-   [Establecer las propiedades de tareas o contenedores](../../2014/integration-services/set-the-properties-of-a-task-or-container.md)  
  
-   [Agregar o eliminar un componente en un flujo de datos](data-flow/add-or-delete-a-component-in-a-data-flow.md)  
  
## <a name="related-content"></a>Contenido relacionado  
  
1.  Vídeo, [Crear un paquete básico (vídeo de SQL Server)](http://go.microsoft.com/fwlink/?LinkId=131023), en MSDN.Microsoft.com  
  
## <a name="see-also"></a>Vea también  
 [Servicios de integración &#40;SSIS&#41; paquetes](../../2014/integration-services/integration-services-ssis-packages.md)   
 [Restricciones de precedencia](control-flow/precedence-constraints.md)  
  
  
