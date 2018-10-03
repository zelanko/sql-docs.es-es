---
title: Configurar el destino del archivo plano (Asistente para importación y exportación de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.configureflatfiledest.f1
ms.assetid: 318e8da0-37d3-46cd-943a-fc5d66aad93a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f8dd326b588880ca2f095c83c6a2d9ad8f02ac32
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47694153"
---
# <a name="configure-flat-file-destination-sql-server-import-and-export-wizard"></a>Configurar el destino del archivo plano (Asistente para importación y exportación de SQL Server)
  Si ha seleccionado un destino de archivo plano, el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muestra **Configurar el destino del archivo plano** después de especificar que quiere copiar una tabla o después de proporcionar una consulta. En esta página, especifique las opciones de formato del archivo de destino plano. Opcionalmente, revise la asignación de columnas individuales y obtenga una vista previa de los datos de ejemplo.  
  
## <a name="screen-shot-of-the-configure-flat-file-destination-page"></a>Captura de pantalla de la página Configurar el destino del archivo plano  
 En la siguiente pantalla se muestra un ejemplo de la página **Configurar el destino del archivo plano** del asistente.
 
 En este ejemplo, el usuario ha especificado las siguientes opciones para crear un archivo CSV (valores separados por comas) típico.
-   **Delimitador de filas**. Cada fila de datos en la salida finaliza con una combinación de retorno de carro-avance de línea.
-   **Delimitador de columna**. Las columnas de datos dentro de cada fila se separan con una coma.

 ![Configurar la página de archivos planos del Asistente para importación y exportación](../../integration-services/import-export-data/media/flat-file.png)
  
## <a name="pick-a-source-table"></a>Seleccionar una tabla de origen
 **Tabla o vista de origen**  
-   Si ha especificado en una página anterior que quiere copiar una tabla, seleccione la tabla o vista de origen de la lista desplegable.
-   Si ha proporcionado una consulta, `"Query"` es la única opción y se selecciona.  

## <a name="specify-row-and-column-delimiters-for-the-output"></a>Especificar los delimitadores de filas y columnas para la salida
 **Delimitador de filas**  
 Seleccione de la lista de delimitadores para separar las filas en la salida. No hay ninguna opción para especificar un delimitador de fila *personalizado*.  
  
|Valor|Descripción|  
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
 Seleccione de la lista de delimitadores para separar las columnas en la salida. No hay ninguna opción para especificar un delimitador de columna *personalizado*.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**{CR}{LF}**|Las columnas se delimitan mediante una combinación de retorno de carro y avance de línea.|  
|**{CR}**|Las columnas se delimitan mediante un retorno de carro.|  
|**{LF}**|Las columnas se delimitan mediante un avance de línea.|  
|**Punto y coma {;}**|Las columnas se delimitan mediante un punto y coma.|  
|**Dos puntos {:}**|Las columnas se delimitan mediante dos puntos.|  
|**Coma {,}**|Las columnas se delimitan mediante una coma.|  
|**Tabulación {t}**|Las columnas se delimitan mediante una tabulación.|  
|**Barra vertical {&#124;}**|Las columnas se delimitan mediante una barra vertical.|  

## <a name="optionally-review-column-mappings-and-preview-data"></a>Revisión de las asignaciones de columnas y obtención de una vista previa de los datos (opcional)

**Editar asignaciones**   
Si quiere, puede hacer clic en **Editar asignaciones** para ver el cuadro de diálogo **Asignaciones de columnas** de la tabla seleccionada. Use el cuadro de diálogo **Asignaciones de columnas** para hacer lo siguiente.
-   Revise la asignación de columnas individuales entre el origen y el destino.
-   Copie solo un subconjunto de columnas si selecciona **Omitir** para las columnas que no desea copiar.

Para más información, vea [Asignaciones de columnas](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md).  

**Vista previa**  
Si quiere, puede hacer clic en **Vista previa** para obtener una vista previa de hasta 200 filas de datos de ejemplo en el cuadro de diálogo **Vista previa de los datos**. Esto confirma que el asistente va a copiar los datos que quiere copiar. Para más información, vea [Vista previa de los datos](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md).  
  
Después de obtener una vista previa de los datos, es posible que quiera cambiar las opciones que seleccionó en páginas anteriores del asistente. Para realizar estas modificaciones, vuelva a la página **Configurar el destino del archivo plano** y después haga clic en **Atrás** para volver a las páginas anteriores en las que puede cambiar sus selecciones.  

## <a name="whats-next"></a>¿Qué sigue?  
 Después de especificar las opciones de formato del archivo plano de destino, la página siguiente es **Guardar y ejecutar paquete**. En esta página, especifique si quiere ejecutar la operación inmediatamente. Según la configuración, es posible que también pueda guardar su configuración como un paquete [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para personalizarlo y volver a usarlo más adelante. Para más información, vea [Guardar y ejecutar paquete](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md).  

