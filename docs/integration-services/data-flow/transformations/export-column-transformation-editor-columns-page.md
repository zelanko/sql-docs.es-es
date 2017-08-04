---
title: "Editor de transformación de columna (página columnas) exportar | Documentos de Microsoft"
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
- sql13.dts.designer.fileextractortransformation.columns.f1
helpviewer_keywords:
- Export Column Transformation Editor
ms.assetid: b659a5c2-5509-4b5b-9c82-136c971d5c7f
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e3538e9379c48faaa700f56aa1ecf0ceafc68e2a
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="export-column-transformation-editor-columns-page"></a>Editor de transformación Exportar columna (página Columnas)
  Use la página **Columnas** del cuadro de diálogo **Editor de transformación Exportar columna** para especificar las columnas del flujo de datos que desea extraer a los archivos. Podrá especificar si desea que la transformación Exportar columna anexe los datos a un archivo o sobrescriba un archivo existente.  
  
 Para obtener más información acerca de la transformación Exportar columna, vea [Export Column Transformation](../../../integration-services/data-flow/transformations/export-column-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Columna Extraer**  
 Seleccione de la lista las columnas de entrada que contengan datos de texto o imagen. Todas las filas deben poseer definiciones para la **Columna Extraer** y la **Columna Ruta de archivo**.  
  
 **Columna Ruta de archivo**  
 Seleccione de la lista las columnas de entrada que contengan rutas de archivo y nombres de archivo. Todas las filas deben poseer definiciones para la **Columna Extraer** y la **Columna Ruta de archivo**.  
  
 **Permitir la anexión**  
 Especifique si desea que la transformación anexe los datos a los archivos existentes. El valor predeterminado es **false**.  
  
 **Forzar el truncamiento**  
 Especifique si desea que la transformación elimine el contenido de los archivos existentes antes de escribir los datos. El valor predeterminado es **false**.  
  
 **BOM de escritura**  
 Especifique si desea escribir una marca de orden de bytes (BOM) en el archivo. Solo se escribirá una BOM si los datos poseen el tipo de datos **DT_NTEXT** o DT_WSTR y no están anexados a un archivo de datos existente.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de transformación Exportar columna &#40; Página de salida de error &#41;](../../../integration-services/data-flow/transformations/export-column-transformation-editor-error-output-page.md)  
  
  
