---
title: Editor del Administrador de conexiones de archivos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fileconnectionmanager.f1
helpviewer_keywords:
- File Connection Manager Editor
ms.assetid: 051c48e5-3d86-49af-b554-ff62e3de3622
caps.latest.revision: 22
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0691e6d8b6bebec04d2126bba0caa8b14ed3cdd1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37311945"
---
# <a name="file-connection-manager-editor"></a>Editor del administrador de conexiones de archivos
  Utilice el cuadro de diálogo **Editor del administrador de conexiones de archivos** para especificar las propiedades utilizadas para conectarse a un archivo o una carpeta.  
  
> [!NOTE]  
>  Para establecer la propiedad ConnectionString del administrador de conexiones de archivos, puede especificar una expresión en la ventana Propiedades de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Pero para evitar que se produzca un error de validación al usar una expresión para especificar el archivo o la carpeta, en **Editor del administrador de conexiones de archivos**, en **Archivo/Carpeta**, agregue la ruta de acceso de un archivo o una carpeta.  
  
 Para obtener más información acerca del administrador de conexiones de archivos, vea [File Connection Manager](connection-manager/file-connection-manager.md).  
  
## <a name="options"></a>Opciones  
 **Tipo de uso**  
 Especifica si el **Administrador de conexiones de archivos** se conecta a un archivo o una carpeta existente o si crea un nuevo archivo o una nueva carpeta.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|Crear archivo|Crea un nuevo archivo en tiempo de ejecución.|  
|Archivo existente|Utiliza un archivo existente.|  
|Crear carpeta|Crea una nueva carpeta en tiempo de ejecución.|  
|Carpeta existente|Utiliza una carpeta existente.|  
  
 **Archivo / Carpeta**  
 Si se trata de **Archivo**, especifica el archivo que se va a usar.  
  
 Si se trata de **Carpeta**, especifica la carpeta que se va a utilizar.  
  
 **Examinar**  
 Seleccione el archivo o la carpeta mediante el cuadro de diálogo **Seleccionar archivo** o **Buscar carpeta** .  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  
