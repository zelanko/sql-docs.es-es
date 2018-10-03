---
title: Administrador de conexiones de varios archivos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- folders [Integration Services], connections
- files [Integration Services], connections
- Multiple Files connection manager
- connection managers [Integration Services], Multiple Files
- connections [Integration Services], files
- multiple file connections
ms.assetid: 10bdc56e-c5cd-4ddb-b2f7-375fe57fe8b2
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a0b08bcbf989f2c6fc0bc5b6cc163150b388d797
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48085955"
---
# <a name="multiple-files-connection-manager"></a>administrador de conexiones de varios archivos
  Un administrador de conexiones de varios archivos habilita un paquete para que haga referencia a los archivos y carpetas existentes o para crear archivos y carpetas en tiempo de ejecución.  
  
> [!NOTE]  
>  Las tareas integradas y componentes de flujo de datos en [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no usan el administrador de conexiones de varios archivos. Sin embargo, puede usar este administrador de conexiones en la tarea Script o en el componente de script. Para obtener información acerca de cómo se utilizan los administradores de conexión en la tarea Script, vea [Conectarse a orígenes de datos de la tarea Script](../extending-packages-scripting/task/connecting-to-data-sources-in-the-script-task.md). Para obtener información acerca de cómo se utilizan los administradores de conexión en el componente de Script, consulte [conexión a orígenes de datos en el componente de Script] (.. / extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md.  
  
## <a name="usage-types-of-the-multiple-files-connection-manager"></a>Tipos de uso del administrador de conexiones de varios archivos  
 La propiedad `FileUsageType` del administrador de conexiones de varios archivos especifica la forma en que se usa la conexión. El administrador de conexiones de varios archivos puede crear archivos, carpetas, usar archivos existentes y usar carpetas existentes.  
  
 En la tabla siguiente se enumera los valores de `FileUsageType`.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**0**|El administrador de conexiones de varios archivos usa un archivo existente.|  
|**1**|El administrador de conexiones de varios archivos crea un archivo.|  
|**2**|El administrador de conexiones de varios archivos usa una carpeta existente.|  
|**3**|El administrador de conexiones de varios archivos crea una carpeta.|  
  
## <a name="configuration-of-the-multiple-files-connection-manager"></a>Configuración del administrador de conexiones de varios archivos  
 Cuando se agrega un administrador de conexiones de varios archivos a un paquete, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea un administrador de conexiones que se resuelve en una conexión de varios archivos en tiempo de ejecución, configura las propiedades de conexión de varios archivos y agrega la conexión de varios archivos a la colección `Connections` del paquete.  
  
 El `ConnectionManagerType` propiedad del Administrador de conexiones se establece en `MULTIFILE`.  
  
 Puede configurar el administrador de conexiones de varios archivos de las maneras siguientes:  
  
-   Especificar el tipo de uso de archivos y carpetas.  
  
-   Especificar archivos y carpetas.  
  
-   Si usa varios archivos o carpetas, especificar el orden en que se obtiene acceso a los archivos y carpetas.  
  
 Si el administrador de conexiones de varios archivos hace referencia a varios archivos y carpetas, las rutas de los archivos y carpetas se separan con la barra vertical (|). La propiedad `ConnectionString` del administrador de conexiones tiene el formato siguiente:  
  
 \<*ruta de acceso*>|\<*ruta de acceso*>  
  
 También puede especificar varios archivos o carpetas mediante caracteres comodín. Por ejemplo, para hacer referencia unidad de todos los archivos de texto en C, el valor de la `ConnectionString` propiedad se puede establecer en C:\\*.txt.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información sobre las propiedades que puede configurar en el Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vea [Referencia de la interfaz de usuario del cuadro de diálogo Agregar administrador de conexiones de archivos](add-file-connection-manager-dialog-box-ui-reference.md).  
  
 Para obtener información acerca de cómo configurar un administrador de conexiones mediante programación, vea <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> y [agregar conexiones mediante programación](../building-packages-programmatically/adding-connections-programmatically.md).  
  
  
