---
title: "Editor de destino de archivo (página Administrador de conexiones) planos | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.flatfiledestadapter.connection.f1
helpviewer_keywords:
- Flat File Destination Editor
ms.assetid: b01571fa-bc19-4742-8eed-ac163172a919
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 85e551983f5409098187848014bd4819e0810c90
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="flat-file-destination-editor-connection-manager-page"></a>Editor de destino de archivos planos (página Administrador de conexiones)
  Utilice la página **Administrador de conexiones** del cuadro de diálogo **Editor de destino de archivos planos** para seleccionar la conexión de archivos planos del destino y para especificar si se debe sobrescribir o anexar en el archivo de destino existente. El destino de archivo plano escribe datos en un archivo de texto. Este archivo de texto puede tener los formatos: delimitado, ancho fijo, ancho fijo con delimitadores de fila o derecho irregular.  
  
 Para obtener más información acerca del destino de archivo plano, vea [Flat File Destination](../../integration-services/data-flow/flat-file-destination.md).  
  
## <a name="options"></a>Opciones  
 **Administrador de conexiones de archivos planos**  
 Seleccione un administrador de conexiones existente en el cuadro de lista o haga clic en **Nueva**para crear una conexión.  
  
 **Nueva**  
 Cree una conexión con los cuadros de diálogo **Formato del archivo plano** y **Editor del administrador de conexiones de archivos planos** .  
  
 Además de los formatos estándar de archivo plano delimitado, ancho fijo y desigual a la derecha, el cuadro de diálogo **Formato de archivo plano** tiene una cuarta opción, **Ancho fijo con delimitadores de fila**. Esta opción representa un caso especial del formato derecho desigual en el que [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] agrega una columna ficticia como última columna de datos. Esta columna ficticia sirve para garantizar que la última columna tenga un ancho fijo.  
  
 La opción **Ancho fijo con delimitadores de fila** no está disponible en el **Editor del administrador de conexiones de archivos planos**. Si es necesario, puede emular esta opción en el editor. Para emular esta opción, en la página **General** del **Editor del administrador de conexiones de archivos planos**seleccione **Desigual a la derecha**en **Formato**, . A continuación en la página **Avanzadas** del editor, agregue una nueva columna ficticia como última columna de datos.  
  
 **Sobrescribir los datos del archivo**  
 Indique si desea sobrescribir un archivo existente o anexar datos en él.  
  
 **Encabezado**  
 Escriba un bloque de texto para insertarlo en el archivo antes de que se escriban datos. Utilice esta opción para incluir información adicional, como encabezados de columna.  
  
 **Vista previa**  
 Muestra una vista previa de los resultados mediante el cuadro de diálogo **Vista de datos** . La vista previa puede mostrar hasta 200 filas.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de destino de archivos planos &#40; Página Asignaciones &#41;](../../integration-services/data-flow/flat-file-destination-editor-mappings-page.md)  
  
  
