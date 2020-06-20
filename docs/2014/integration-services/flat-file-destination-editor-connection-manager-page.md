---
title: Editor de destino de archivos planos (página Administrador de conexiones) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.flatfiledestadapter.connection.f1
helpviewer_keywords:
- Flat File Destination Editor
ms.assetid: b01571fa-bc19-4742-8eed-ac163172a919
author: janinezhang
ms.author: janinez
ms.openlocfilehash: c7d2c37e38386f7e46c1b8a0800d45dfc0b9b0dd
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84967085"
---
# <a name="flat-file-destination-editor-connection-manager-page"></a>Editor de destino de archivos planos (página Administrador de conexiones)
  Utilice la página **Administrador de conexiones** del cuadro de diálogo **Editor de destino de archivos planos** para seleccionar la conexión de archivos planos del destino y para especificar si se debe sobrescribir o anexar en el archivo de destino existente. El destino de archivo plano escribe datos en un archivo de texto. Este archivo de texto puede tener los formatos: delimitado, ancho fijo, ancho fijo con delimitadores de fila o derecho irregular.  
  
 Para obtener más información acerca del destino de archivo plano, vea [Flat File Destination](data-flow/flat-file-destination.md).  
  
## <a name="options"></a>Opciones  
 **Administrador de conexiones de archivos planos**  
 Seleccione un administrador de conexiones existente en el cuadro de lista o haga clic en **Nueva**para crear una conexión.  
  
 **Nuevo**  
 Cree una conexión con los cuadros de diálogo **Formato del archivo plano** y **Editor del administrador de conexiones de archivos planos** .  
  
 Además de los formatos estándar de archivo plano delimitado, ancho fijo y desigual a la derecha, el cuadro de diálogo **Formato de archivo plano** tiene una cuarta opción, **Ancho fijo con delimitadores de fila**. Esta opción representa un caso especial del formato derecho desigual en el que [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] agrega una columna ficticia como última columna de datos. Esta columna ficticia sirve para garantizar que la última columna tenga un ancho fijo.  
  
 La opción **Ancho fijo con delimitadores de fila** no está disponible en el **Editor del administrador de conexiones de archivos planos**. Si es necesario, puede emular esta opción en el editor. Para emular esta opción, en la página **General** del **Editor del administrador de conexiones de archivos planos**seleccione **Desigual a la derecha**en **Formato**, . A continuación en la página **Avanzadas** del editor, agregue una nueva columna ficticia como última columna de datos.  
  
 **Sobrescribir los datos del archivo**  
 Indique si desea sobrescribir un archivo existente o anexar datos en él.  
  
 **Encabezado**  
 Escriba un bloque de texto para insertarlo en el archivo antes de que se escriban datos. Utilice esta opción para incluir información adicional, como encabezados de columna.  
  
 **Versión preliminar**  
 Muestra una vista previa de los resultados mediante el cuadro de diálogo **Vista de datos** . La vista previa puede mostrar hasta 200 filas.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de destino de archivos planos &#40;página Asignaciones&#41;](../../2014/integration-services/flat-file-destination-editor-mappings-page.md)  
  
  
