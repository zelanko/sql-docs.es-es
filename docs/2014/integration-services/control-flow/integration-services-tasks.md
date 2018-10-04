---
title: Tareas de Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- scripts [Integration Services], tasks
- files [Integration Services], task options
- workflow tasks [Integration Services]
- Integration Services, tasks
- adding package tasks
- tasks [Integration Services], listed
- SSIS tasks
- SSIS, tasks
- control flow [Integration Services], tasks
- tasks [Integration Services]
- grouping tasks
- tasks [Integration Services], about tasks
- SQL Server Integration Services tasks
- data preparation tasks [Integration Services]
- directory operations [Integration Services]
ms.assetid: 75c8901d-6966-4af3-abe5-10af6dd9313b
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a87a28e1e39959868b1a39c897b8b67716227466
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48111854"
---
# <a name="integration-services-tasks"></a>Tareas de Integration Services
  Las tareas son elementos de flujo de control que definen las unidades de trabajo que se realizan en un flujo de control de paquetes. Un paquete de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] consta de una o más tareas. Si el paquete contiene más de una tarea, las tareas se conectan y ordenan en el flujo de control mediante restricciones de precedencia.  
  
 También puede escribir tareas personalizadas mediante un lenguaje de programación compatible con COM, como Visual Basic, o un lenguaje de programación .NET, como C#.  
  
 El Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , la herramienta gráfica de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para trabajar con paquetes, proporciona la superficie de diseño para crear flujos de control de paquetes y proporciona editores personalizados para configurar las tareas. También se puede programar el modelo de objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para crear paquetes mediante programación.  
  
## <a name="types-of-tasks"></a>Tipos de tareas  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] incluye los siguientes tipos de tareas.  
  
 Tarea Flujo de datos  
 Tarea que ejecuta flujos de datos para extraer datos, aplicar transformaciones de nivel de columna y cargar datos.  
  
 Tareas de preparación de datos  
 Estas tareas llevan a cabo los procesos siguientes: copiar archivos y directorios; descargar archivos y datos; ejecutar métodos web; aplicar operaciones a documentos XML; y generar perfiles de los datos para la limpieza.  
  
 Tareas de flujo de trabajo  
 Tareas que se comunican con otros procesos para ejecutar paquetes, ejecutar programas o archivos por lotes, enviar y recibir mensajes entre paquetes, enviar mensajes de correo electrónico, leer datos de Instrumental de administración de Windows (WMI) y detectar eventos de WMI.  
  
 Tareas de SQL Server  
 Tareas de acceso, copia, inserción, eliminación y modificación de objetos y datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Tareas de scripting  
 Tareas que amplían la funcionalidad de los paquetes mediante scripts.  
  
 Tareas de Analysis Services  
 Tareas de creación, modificación, eliminación y procesamiento de objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Tareas de mantenimiento  
 Tareas que realizan funciones administrativas como crear copias de seguridad y reducir bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , volver a generar y reorganizar índices, y ejecutar trabajos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Tareas personalizadas  
 Además, también puede escribir tareas personalizadas mediante un lenguaje de programación compatible con COM, como Visual Basic, o un lenguaje de programación .NET, como C#. Si quiere tener acceso a una tarea personalizada en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , puede crear y registrar una interfaz de usuario para la tarea. Para obtener más información, vea [Desarrollar una tarea personalizada](../extending-packages-custom-objects/task/developing-a-custom-task.md).  
  
## <a name="configuration-of-tasks"></a>Configuración de tareas  
 Un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] puede contener una tarea individual, como una tarea Ejecutar SQL que elimina registros de una tabla de base de datos cuando se ejecuta el paquete. No obstante, los paquetes suelen contener varias tareas y cada tarea se establece para ejecutarse en el contexto del flujo de control de paquete. Los controladores de eventos, que son flujos de trabajo que se ejecutan en respuesta a eventos de tiempo de ejecución, también puede tener tareas.  
  
 Para obtener más información sobre cómo agregar una tarea a un paquete mediante el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vea [Agregar o eliminar tareas o contenedores en un flujo de control](add-or-delete-a-task-or-a-container-in-a-control-flow.md).  
  
 Para obtener más información sobre cómo agregar una tarea a un paquete mediante programación, vea [Agregar tareas mediante programación](../building-packages-programmatically/adding-tasks-programmatically.md).  
  
 Cada tarea puede configurarse individualmente a través de los cuadros de diálogo personalizados para cada tarea proporcionados por el diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a través de la ventana Propiedades incluida en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Un paquete puede incluir varias tareas del mismo tipo (por ejemplo, seis tareas Ejecutar SQL) y cada tarea se puede configurar de una manera diferente. Para obtener más información, vea [Establecer las propiedades de tareas o contenedores](../set-the-properties-of-a-task-or-container.md).  
  
## <a name="tasks-connections-and-groups"></a>Grupos y conexiones de tareas  
 Si una tarea contiene más de una tarea, dichas tareas se conectan y ordenan en el flujo de control mediante restricciones de precedencia. Para más información, consulte [Precedence Constraints](precedence-constraints.md).  
  
 Las tareas pueden agruparse y ejecutarse como una sola unidad de trabajo o repetirse en un bucle. Para obtener más información, consulte [Foreach Loop Container](foreach-loop-container.md), [For Loop Container](for-loop-container.md)y [Sequence Container](sequence-container.md).  
  
## <a name="related-tasks"></a>Related Tasks  
 [Agregar o eliminar tareas o contenedores en un flujo de control](add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  
  
