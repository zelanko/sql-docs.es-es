---
title: Exportar a Editor de transformación de columna (página columnas) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fileextractortransformation.columns.f1
helpviewer_keywords:
- Export Column Transformation Editor
ms.assetid: b659a5c2-5509-4b5b-9c82-136c971d5c7f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d7682e3c22885b50e1516a8f30cce468852ae2c7
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58378064"
---
# <a name="export-column-transformation-editor-columns-page"></a>Editor de transformación Exportar columna (página Columnas)
  Use la página **Columnas** del cuadro de diálogo **Editor de transformación Exportar columna** para especificar las columnas del flujo de datos que desea extraer a los archivos. Podrá especificar si desea que la transformación Exportar columna anexe los datos a un archivo o sobrescriba un archivo existente.  
  
 Para obtener más información acerca de la transformación Exportar columna, vea [Export Column Transformation](data-flow/transformations/export-column-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Columna Extraer**  
 Seleccione de la lista las columnas de entrada que contengan datos de texto o imagen. Todas las filas deben poseer definiciones para la **Columna Extraer** y la **Columna Ruta de archivo**.  
  
 **Columna Ruta de archivo**  
 Seleccione de la lista las columnas de entrada que contengan rutas de archivo y nombres de archivo. Todas las filas deben poseer definiciones para la **Columna Extraer** y la **Columna Ruta de archivo**.  
  
 **Permitir la anexión**  
 Especifique si desea que la transformación anexe los datos a los archivos existentes. De manera predeterminada, es `false`.  
  
 **Forzar el truncamiento**  
 Especifique si desea que la transformación elimine el contenido de los archivos existentes antes de escribir los datos. De manera predeterminada, es `false`.  
  
 **BOM de escritura**  
 Especifique si desea escribir una marca de orden de bytes (BOM) en el archivo. Solo se escribirá una BOM si los datos poseen el tipo de datos `DT_NTEXT` o DT_WSTR y no están anexados a un archivo de datos existente.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de transformación Exportar columna &#40;página Salida de error&#41;](../../2014/integration-services/export-column-transformation-editor-error-output-page.md)  
  
  
