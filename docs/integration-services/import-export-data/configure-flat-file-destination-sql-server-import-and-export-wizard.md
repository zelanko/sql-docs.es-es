---
title: "Configurar el destino de archivo sin formato (importación de SQL Server y Asistente para exportación) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.configureflatfiledest.f1
ms.assetid: 318e8da0-37d3-46cd-943a-fc5d66aad93a
caps.latest.revision: 53
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 560965a241b24a09f50a23faf63ce74d0049d5a7
ms.openlocfilehash: 93fbd5e9429d06e3f011f6f0aff03d76a3db9000
ms.contentlocale: es-es
ms.lasthandoff: 10/13/2017

---
# <a name="configure-flat-file-destination-sql-server-import-and-export-wizard"></a>Configurar el destino del archivo plano (Asistente para importación y exportación de SQL Server)
  Si ha seleccionado un destino de archivo sin formato, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muestra Import and Export Wizard **configurar destino de archivo plano** después de especificar que van a copiar de una tabla o después de proporcionar una consulta. En esta página, especifique las opciones de formato del archivo de destino plano. Opcionalmente, revise la asignación de columnas individuales y obtenga una vista previa de los datos de ejemplo.  
  
## <a name="screen-shot-of-the-configure-flat-file-destination-page"></a>Captura de pantalla de la página Configurar el destino del archivo plano  
 La captura de pantalla siguiente muestra un ejemplo de la **configurar destino de archivo plano** página del asistente.
 
 En este ejemplo, el usuario ha especificado las siguientes opciones para crear un archivo típico de (valores separados por comas) de CSV.
-   **Delimitador de filas**. Cada fila de datos en la salida finaliza con un retorno de carro-combinación de avance de línea.
-   **Delimitador de columna**. Las columnas de datos dentro de cada fila se separan con una coma.

 ![Configurar página de archivo sin formato de la importación y el Asistente para exportación](../../integration-services/import-export-data/media/flat-file.png)
  
## <a name="pick-a-source-table"></a>Seleccionar una tabla de origen
 **Tabla o vista de origen**  
-   Si se especifica en una página anterior que van a copiar de una tabla, seleccione la tabla de origen o la vista de la lista desplegable.
-   Si se proporciona una consulta, `"Query"` está seleccionada y es la única opción.  

## <a name="specify-row-and-column-delimiters-for-the-output"></a>Especificar los delimitadores de filas y columnas para la salida
 **Delimitador de filas**  
 Seleccione esta opción en la lista de delimitadores para separar las filas en la salida. No hay ninguna opción para especificar un *personalizado* delimitador de filas.  
  
|Valor|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|Las filas se delimitan mediante una combinación de retorno de carro y avance de línea.|  
|**{CR}**|Las filas se delimitan mediante un retorno de carro.|  
|**{LF}**|Las filas se delimitan mediante un avance de línea.|  
|**Punto y coma {;}**|Las filas se delimitan mediante un punto y coma.|  
|**Dos puntos {:}**|Las filas se delimitan mediante dos puntos.|  
|**Coma {,}**|Las filas se delimitan mediante una coma.|  
|**Tabulación {t}**|Las filas se delimitan mediante una tabulación.|  
|**Barra vertical {&#124;}**|Las filas se delimitan mediante una barra vertical.|  
  
 **Delimitador de columna**  
 Seleccione esta opción en la lista de delimitadores para separar las columnas en la salida. No hay ninguna opción para especificar un *personalizado* delimitador de columna.  
  
|Valor|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|Las columnas se delimitan mediante una combinación de retorno de carro y avance de línea.|  
|**{CR}**|Las columnas se delimitan mediante un retorno de carro.|  
|**{LF}**|Las columnas se delimitan mediante un avance de línea.|  
|**Punto y coma {;}**|Las columnas se delimitan mediante un punto y coma.|  
|**Dos puntos {:}**|Las columnas se delimitan mediante dos puntos.|  
|**Coma {,}**|Las columnas se delimitan mediante una coma.|  
|**Tabulación {t}**|Las columnas se delimitan mediante una tabulación.|  
|**Barra vertical {&#124;}**|Las columnas se delimitan mediante una barra vertical.|  

## <a name="optionally-review-column-mappings-and-preview-data"></a>Opcionalmente, revise las asignaciones de columna y obtener una vista previa de datos

**Editar asignaciones**   
Si lo desea, haga clic en **editar asignaciones** para mostrar la **asignaciones de columnas** cuadro de diálogo para la tabla seleccionada. Use el cuadro de diálogo **Asignaciones de columnas** para hacer lo siguiente.
-   Revise la asignación de columnas individuales entre el origen y el destino.
-   Copie solo un subconjunto de columnas si selecciona **Omitir** para las columnas que no desea copiar.

Para más información, vea [Asignaciones de columnas](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md).  

**Vista previa**  
Si lo desea, haga clic en **vista previa** para obtener una vista previa de hasta 200 filas de datos de ejemplo en el **vista previa de datos** cuadro de diálogo. Esto confirma que el asistente va a copiar los datos que quiere copiar. Para más información, vea [Vista previa de los datos](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md).  
  
Después de obtener una vista previa de los datos, es posible que quiera cambiar las opciones que seleccionó en páginas anteriores del asistente. Para realizar estas modificaciones, vuelva a la página **Configurar el destino del archivo plano** y después haga clic en **Atrás** para volver a las páginas anteriores en las que puede cambiar sus selecciones.  

## <a name="whats-next"></a>¿Qué debe hacer a continuación?  
 Después de especificar las opciones de formato del archivo plano de destino, la página siguiente es **Guardar y ejecutar paquete**. En esta página, especifique si quiere ejecutar la operación inmediatamente. Según la configuración, también puede guardar la configuración como un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] paquete para personalizarlo y reutilizarla más adelante. Para más información, vea [Guardar y ejecutar paquete](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md).  


