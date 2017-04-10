---
title: "Editor del administrador de conexiones de archivos | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.fileconnectionmanager.f1"
helpviewer_keywords: 
  - "Editor del administrador de conexiones de archivos"
ms.assetid: 051c48e5-3d86-49af-b554-ff62e3de3622
caps.latest.revision: 22
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 22
---
# Editor del administrador de conexiones de archivos
  Utilice el cuadro de diálogo **Editor del administrador de conexiones de archivos** para especificar las propiedades utilizadas para conectarse a un archivo o una carpeta.  
  
> [!NOTE]  
>  Para establecer la propiedad ConnectionString del administrador de conexiones de archivos, puede especificar una expresión en la ventana Propiedades de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Pero para evitar que se produzca un error de validación al usar una expresión para especificar el archivo o la carpeta, en **Editor del administrador de conexiones de archivos**, en **Archivo/Carpeta**, agregue la ruta de acceso de un archivo o una carpeta.  
  
 Para obtener más información acerca del administrador de conexiones de archivos, vea [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md).  
  
## Opciones  
 **Tipo de uso**  
 Especifica si el **Administrador de conexiones de archivos** se conecta a un archivo o una carpeta existente o si crea un nuevo archivo o una nueva carpeta.  
  
|Value|Description|  
|-----------|-----------------|  
|Crear archivo|Crea un nuevo archivo en tiempo de ejecución.|  
|Archivo existente|Utiliza un archivo existente.|  
|Crear carpeta|Crea una nueva carpeta en tiempo de ejecución.|  
|Carpeta existente|Utiliza una carpeta existente.|  
  
 **Archivo / Carpeta**  
 Si se trata de **Archivo**, especifica el archivo que se va a usar.  
  
 Si se trata de **Carpeta**, especifica la carpeta que se va a utilizar.  
  
 **Examinar**  
 Seleccione el archivo o la carpeta mediante el cuadro de diálogo **Seleccionar archivo** o **Buscar carpeta**.  
  
## Vea también  
 [Referencia de errores y mensajes de Integration Services](../../integration-services/integration-services-error-and-message-reference.md)  
  
  