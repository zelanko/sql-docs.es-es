---
description: administrador de conexiones de archivos
title: Administrador de conexiones de archivos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.fileconnectionmanager.f1
helpviewer_keywords:
- folders [Integration Services], connections
- files [Integration Services], connections
- files [Integration Services]
- connection managers [Integration Services], File
- connections [Integration Services], files
- File connection manager
ms.assetid: 019078bc-44ee-4975-9169-0f9a89e3f3be
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ebe86146e2ce4f25f05c9948071d3fc7a4d4edb8
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/25/2020
ms.locfileid: "96123699"
---
# <a name="file-connection-manager"></a>administrador de conexiones de archivos

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Un administrador de conexiones de archivos permite a un paquete hacer referencia a un archivo o carpeta existente o crear un archivo o carpeta en tiempo de ejecución. Por ejemplo, puede hacer referencia a un archivo de Excel. Ciertos componentes de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] utilizan información de los archivos para realizar su trabajo. Por ejemplo, una tarea Ejecutar SQL puede hacer referencia a un archivo que contiene las instrucciones SQL que ejecuta la tarea. Otros componentes realizan operaciones en los archivos. Por ejemplo, la tarea Sistema de archivos puede hacer referencia a un archivo para copiarlo en una nueva ubicación.  
  
## <a name="usage-types-of-the-file-connection-manager"></a>Tipos de uso del administrador de conexiones de archivos  
 La propiedad **FileUsageType** del administrador de conexiones de archivos especifica la forma en que se usa la conexión de archivos. El administrador de conexiones de archivos puede crear un archivo, crear una carpeta, usar un archivo o una carpeta existente.  
  
 La tabla siguiente enumera los valores de **FileUsageType**.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**0**|El administrador de conexiones de archivos usa un archivo existente.|  
|**1**|El administrador de conexiones de archivos crea un archivo.|  
|**2**|El administrador de conexiones de archivos usa una carpeta existente.|  
|**3**|El administrador de conexiones de archivos crea una carpeta.|  
  
## <a name="multiple-file-or-folder-connections"></a>Conexiones de varios archivos o carpetas  
 El administrador de conexiones de archivos puede hacer referencia a un solo archivo o carpeta. Para hacer referencia a varios archivos o carpetas, use, en lugar de un Administrador de conexiones de archivos, un administrador de conexiones de varios archivos. Para más información, consulte [Multiple Files Connection Manager](../../integration-services/connection-manager/multiple-files-connection-manager.md).  
  
## <a name="configuration-of-the-file-connection-manager"></a>Configuración del administrador de conexiones de archivos  
 Cuando se agrega un administrador de conexiones de archivos a un paquete, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea un administrador de conexiones que se resuelve en una conexión de archivos en tiempo de ejecución, establece las propiedades de conexión de archivos y agrega la conexión de archivos a la colección **Conexiones** del paquete.  
  
 La propiedad **ConnectionManagerType** del administrador de conexiones se establece en **FILE**.  
  
 Puede configurar el administrador de conexiones de archivos de las maneras siguientes:  
  
-   Especificar el tipo de uso.  
  
-   Especificar un archivo o carpeta.  
  
 Para establecer la propiedad ConnectionString del administrador de conexiones de archivos, puede especificar una expresión en la ventana Propiedades de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Pero para evitar que se produzca un error de validación al usar una expresión para especificar el archivo o la carpeta, en **Editor del administrador de conexiones de archivos**, en **Archivo/Carpeta**, agregue la ruta de acceso de un archivo o una carpeta.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para más información sobre las propiedades que puede configurar en el Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] , consulte [Editor del administrador de conexiones de archivos]().  
  
 Para obtener información sobre la configuración de un administrador de conexiones mediante programación, vea <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> y [Agregar conexiones mediante programación](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="file-connection-manager-editor"></a>Editor del administrador de conexiones de archivos
  Utilice el cuadro de diálogo **Editor del administrador de conexiones de archivos** para especificar las propiedades utilizadas para conectarse a un archivo o una carpeta.  
  
> [!NOTE]  
>  Para establecer la propiedad ConnectionString del administrador de conexiones de archivos, puede especificar una expresión en la ventana Propiedades de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Pero para evitar que se produzca un error de validación al usar una expresión para especificar el archivo o la carpeta, en **Editor del administrador de conexiones de archivos**, en **Archivo/Carpeta**, agregue la ruta de acceso de un archivo o una carpeta.  
  
 Para obtener más información acerca del administrador de conexiones de archivos, vea [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md).  
  
### <a name="options"></a>Opciones  
 **Tipo de uso**  
 Especifica si el **Administrador de conexiones de archivos** se conecta a un archivo o una carpeta existente o si crea un nuevo archivo o una nueva carpeta.  
  
|Value|Descripción|  
|-----------|-----------------|  
|Crear archivo|Crea un nuevo archivo en tiempo de ejecución.|  
|Archivo existente|Utiliza un archivo existente.|  
|Crear carpeta|Crea una nueva carpeta en tiempo de ejecución.|  
|Carpeta existente|Utiliza una carpeta existente.|  
  
 **Archivo / Carpeta**  
 Si se trata de **Archivo**, especifica el archivo que se va a usar.  
  
 Si se trata de **Carpeta**, especifica la carpeta que se va a utilizar.  
  
 **Browse**  
 Seleccione el archivo o la carpeta mediante el cuadro de diálogo **Seleccionar archivo** o **Buscar carpeta** .  
  
