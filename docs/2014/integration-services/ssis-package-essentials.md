---
title: Essentials de paquetes SSIS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- package requirements
ms.assetid: b0c86c35-e3d3-4724-9a96-4087e9d74bf3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3a12fb33db8b1b4da1b33c02850a108b1e30b2d2
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58390803"
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
  
 Para obtener un ejemplo de cómo crear un paquete básico, consulte [lección 1: Crear el proyecto y el paquete básico](lesson-1-create-a-project-and-basic-package-with-ssis.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Crear paquetes en herramientas de datos de SQL Server](create-packages-in-sql-server-data-tools.md)  
  
-   [Agregar o eliminar tareas o contenedores en un flujo de control](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  
-   [Establecer las propiedades de tareas o contenedores](../../2014/integration-services/set-the-properties-of-a-task-or-container.md)  
  
-   [Agregar o eliminar un componente en un flujo de datos](data-flow/add-or-delete-a-component-in-a-data-flow.md)  
  
## <a name="related-content"></a>Contenido relacionado  
  
1.  Vídeo, [Crear un paquete básico (vídeo de SQL Server)](https://go.microsoft.com/fwlink/?LinkId=131023), en MSDN.Microsoft.com  
  
## <a name="see-also"></a>Vea también  
 [Paquetes de Integration Services &#40;SSIS&#41;](../../2014/integration-services/integration-services-ssis-packages.md)   
 [Restricciones de precedencia](control-flow/precedence-constraints.md)  
  
  
