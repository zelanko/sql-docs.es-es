---
title: Administrador de conexiones de varios archivos | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- folders [Integration Services], connections
- files [Integration Services], connections
- Multiple Files connection manager
- connection managers [Integration Services], Multiple Files
- connections [Integration Services], files
- multiple file connections
ms.assetid: 10bdc56e-c5cd-4ddb-b2f7-375fe57fe8b2
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 54f769172d7148635b898751f561c9d15e27569b
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/12/2018
ms.locfileid: "35402657"
---
# <a name="multiple-files-connection-manager"></a>administrador de conexiones de varios archivos
  Un administrador de conexiones de varios archivos habilita un paquete para que haga referencia a los archivos y carpetas existentes o para crear archivos y carpetas en tiempo de ejecución.  
  
> [!NOTE]  
>  Las tareas integradas y componentes de flujo de datos en [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no usan el administrador de conexiones de varios archivos. Sin embargo, puede usar este administrador de conexiones en la tarea Script o en el componente de script. Para obtener información acerca de cómo se utilizan los administradores de conexión en la tarea Script, vea [Conectarse a orígenes de datos de la tarea Script](../../integration-services/extending-packages-scripting/task/connecting-to-data-sources-in-the-script-task.md). Para obtener información acerca de cómo se utilizan los administradores de conexión en el componente de script, vea [Conectarse a orígenes de datos del componente de script](../../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md).  
  
## <a name="usage-types-of-the-multiple-files-connection-manager"></a>Tipos de uso del administrador de conexiones de varios archivos  
 La propiedad **FileUsageType** del administrador de conexiones de varios archivos especifica la forma en que se usa la conexión. El administrador de conexiones de varios archivos puede crear archivos, carpetas, usar archivos existentes y usar carpetas existentes.  
  
 La tabla siguiente enumera los valores de **FileUsageType**.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**0**|El administrador de conexiones de varios archivos usa un archivo existente.|  
|**1**|El administrador de conexiones de varios archivos crea un archivo.|  
|**2**|El administrador de conexiones de varios archivos usa una carpeta existente.|  
|**3**|El administrador de conexiones de varios archivos crea una carpeta.|  
  
## <a name="configuration-of-the-multiple-files-connection-manager"></a>Configuración del administrador de conexiones de varios archivos  
 Cuando se agrega un administrador de conexiones de varios archivos a un paquete, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea un administrador de conexiones que se resuelve en una conexión de varios archivos en tiempo de ejecución, configura las propiedades de conexión de varios archivos y agrega la conexión de varios archivos a la colección **Connections** del paquete.  
  
 La propiedad **ConnectionManagerType** del administrador de conexiones se establece en **MULTIFILE**.  
  
 Puede configurar el administrador de conexiones de varios archivos de las maneras siguientes:  
  
-   Especificar el tipo de uso de archivos y carpetas.  
  
-   Especificar archivos y carpetas.  
  
-   Si usa varios archivos o carpetas, especificar el orden en que se obtiene acceso a los archivos y carpetas.  
  
 Si el administrador de conexiones de varios archivos hace referencia a varios archivos y carpetas, las rutas de los archivos y carpetas se separan con la barra vertical (|). La propiedad **ConnectionString** del administrador de conexiones tiene el formato siguiente:  
  
 \<*ruta de acceso*>|\<*ruta de acceso*>  
  
 También puede especificar varios archivos o carpetas mediante caracteres comodín. Por ejemplo, para hacer referencia a todos los archivos de texto de la unidad C, el valor de la propiedad **ConnectionString** se puede establecer en C:\\*.txt.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información sobre las propiedades que puede configurar en el Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vea [Referencia de la interfaz de usuario del cuadro de diálogo Agregar administrador de conexiones de archivos](../../integration-services/connection-manager/add-file-connection-manager-dialog-box-ui-reference.md).  
  
 Para obtener información sobre la configuración de un administrador de conexiones mediante programación, vea <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> y [Agregar conexiones mediante programación](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
  
