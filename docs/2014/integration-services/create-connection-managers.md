---
title: Crear administradores de conexiones | Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.connectionmanager.f1
helpviewer_keywords:
- Integration Services packages, connections
- SSIS packages, connections
- packages [Integration Services], connections
- connection managers [Integration Services], creating
- SQL Server Integration Services packages, connections
ms.assetid: 6ca317b8-0061-4d9d-b830-ee8c21268345
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 807241aec9544c8a6366b8d12c0aaddb4b0d228a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48074472"
---
# <a name="create-connection-managers"></a>Crear administradores de conexiones
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] incluye una serie de administradores de conexión adaptados a las necesidades de las tareas que se conectan a diferentes tipos de servidores y orígenes de datos. Los administradores de conexión son utilizados por los componentes de flujo de datos, que extraen y cargan datos en diferentes tipos de almacenes de datos, y por los proveedores de registro que escriben registros en un servidor, tabla o archivo de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Por ejemplo, un paquete con una tarea Enviar correo usa un tipo de administrador de conexiones SMTP para conectarse a un servidor de Protocolo simple de transferencia de correo (SMTP). Un paquete con una tarea Ejecutar SQL puede usar un administrador de conexiones OLE DB para conectarse a una base de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Para más información, vea [Conexiones de Integration Services &#40;SSIS&#41;](connection-manager/integration-services-ssis-connections.md).  
  
 Para crear y configurar automáticamente los administradores de conexiones al crear un paquete nuevo, puede utilizar el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Este asistente también ayuda a crear y configurar los orígenes y destinos que utilizan los administradores de conexiones. Para más información, consulte [Create Packages in SQL Server Data Tools](create-packages-in-sql-server-data-tools.md).  
  
 Para crear manualmente un nuevo administrador de conexiones y agregarlo a un paquete existente, se usa el área **Administradores de conexiones** que aparece en las pestañas **Flujo de control**, **Flujo de datos**y **Controladores de eventos** del Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] . Desde el área **Administrador de conexiones** , se elige el tipo de administrador de conexiones que se desea crear y luego se establecen las propiedades del administrador de conexiones mediante un cuadro de diálogo proporcionado por el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] . Para obtener más información, vea la sección "Usar el área Administradores de conexiones" más adelante en este tema.  
  
 Una vez agregado el administrador de conexiones a un paquete, puede usarlo en tareas, contenedores de bucles Foreach, orígenes, transformaciones y destinos. Para obtener más información, vea [Tareas de Integration Services](control-flow/integration-services-tasks.md), [Contenedor Foreach Loop](control-flow/foreach-loop-container.md) y [Flujo de datos](data-flow/data-flow.md).  
  
## <a name="using-the-connection-managers-area"></a>Uso del área Administradores de conexión  
 Puede crear administradores de conexión mientras las pestañas **Flujo de control**, **Flujo de datos**o **Controladores de eventos** del Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] están activas.  
  
 El siguiente diagrama muestra el área **Administradores de conexión** en la pestaña **Flujo de control** del Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
 ![Captura de pantalla del diseñador de flujo de control con paquete](media/samplecontrolflow.gif "Screenshot of control flow designer with package")  
  
#### <a name="to-add-configure-or-delete-a-connection-manager-in-ssis-designer"></a>Para agregar, configurar o eliminar un administrador de conexiones en el Diseñador SSIS  
  
-   [Agregar, eliminar o compartir un administrador de conexiones en un paquete](../../2014/integration-services/add-delete-or-share-a-connection-manager-in-a-package.md)  
  
-   [Establecer las propiedades de un administrador de conexiones](../../2014/integration-services/set-the-properties-of-a-connection-manager.md)  
  
## <a name="32-bit-and-64-bit-providers-for-connection-managers"></a>Proveedores de 32 y 64 bits para administradores de conexión  
 Muchos de los proveedores que utilizan los administradores de conexión están disponibles en versiones de 32 y 64 bits. El entorno de diseño de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] es un entorno de 32 bits; solamente verá proveedores de 32 bits al diseñar un paquete. Por lo tanto, solo se puede configurar un administrador de conexiones para que utilice un proveedor de 64 bits específico si también está instalada la versión de 32 bits del mismo proveedor.  
  
 En tiempo de ejecución, se utiliza la versión correcta, independientemente de que haya especificado la versión de 32 bits del proveedor en tiempo de diseño. Se puede ejecutar la versión de 64 bits del proveedor aun cuando el paquete se ejecuta en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
 Las dos versiones del proveedor tienen el mismo identificador. Para especificar si el tiempo de ejecución de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] usa una versión de 64 bits disponible del proveedor, establezca la propiedad Run64BitRuntime del proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Si la propiedad Run64BitRuntime se establece en `true`, el tiempo de ejecución busca y usa el proveedor de 64 bits; si Run64BitRuntime es `false`, el tiempo de ejecución busca y usa el proveedor de 32 bits. Para obtener más información sobre las propiedades que se pueden establecer en proyectos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], vea [Entornos de Studio e Integration Services &#40;SSIS&#41;](integration-services-ssis-development-and-management-tools.md).  
  
## <a name="see-also"></a>Vea también  
 [Flujo de control](control-flow/control-flow.md)   
 [Flujo de datos](data-flow/data-flow.md)   
 [Servicios de integración &#40;SSIS&#41; controladores de eventos](integration-services-ssis-event-handlers.md)  
  
  
