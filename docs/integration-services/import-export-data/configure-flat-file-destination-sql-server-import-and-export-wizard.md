---
title: "Configurar el destino del archivo plano (Asistente para importaci&#243;n y exportaci&#243;n de SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.impexpwizard.configureflatfiledest.f1"
ms.assetid: 318e8da0-37d3-46cd-943a-fc5d66aad93a
caps.latest.revision: 53
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 50
---
# Configurar el destino del archivo plano (Asistente para importaci&#243;n y exportaci&#243;n de SQL Server)
  Si ha seleccionado un destino de archivo plano, el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muestra **Configurar el destino del archivo plano** después de especificar una tabla para copiar o de proporcionar una consulta. En esta página, especifique las opciones de formato del archivo plano de destino. Opcionalmente, revise la asignación de columnas individuales y obtenga una vista previa de los datos de ejemplo.  
  
## <a name="screen-shot-of-the-configure-flat-file-destination-page"></a>Captura de pantalla de la página Configurar el destino del archivo plano  
 La siguiente pantalla muestra la página **Configurar el destino del archivo plano** del asistente.
 
 En este ejemplo, el usuario quiere crear un archivo CSV (valores separados por comas) típico para finalizar cada fila de datos de la salida con una combinación de retorno de carro y avance de línea y separar las columnas de datos de cada fila con una coma.

 ![Configure flat file page of the Import and Export Wizard](../../integration-services/import-export-data/media/flat-file.png "Configure flat file page of the Import and Export Wizard")  
  
## <a name="pick-a-source-table"></a>Seleccione una tabla de origen. 
 **Tabla o vista de origen**  
 Seleccione la tabla o vista de origen.  

## <a name="specify-the-row-and-column-delimiters"></a>Especifique los delimitadores de fila y columna
 **Delimitador de filas**  
 Seleccione los delimitadores de filas de la lista. No hay ninguna opción para especificar un delimitador de fila personalizado.  
  
|Value|Description|  
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
 Seleccione los delimitadores de columna de la lista. No hay ninguna opción para especificar un delimitador de columna personalizado.  
  
|Value|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|Las columnas se delimitan mediante una combinación de retorno de carro y avance de línea.|  
|**{CR}**|Las columnas se delimitan mediante un retorno de carro.|  
|**{LF}**|Las columnas se delimitan mediante un avance de línea.|  
|**Punto y coma {;}**|Las columnas se delimitan mediante un punto y coma.|  
|**Dos puntos {:}**|Las columnas se delimitan mediante dos puntos.|  
|**Coma {,}**|Las columnas se delimitan mediante una coma.|  
|**Tabulación {t}**|Las columnas se delimitan mediante una tabulación.|  
|**Barra vertical {&#124;}**|Las columnas se delimitan mediante una barra vertical.|  

## <a name="optionally-edit-column-mappings-and-preview-sample-data"></a>También puede editar las asignaciones de columnas y obtener una vista previa de los datos de ejemplo

**Editar asignaciones**   
Opcionalmente, haga clic en **Editar asignaciones** para ver el cuadro de diálogo **Asignaciones de columnas** de la tabla seleccionada. Use el cuadro de diálogo **Asignaciones de columnas** para hacer lo siguiente.
-   Revise la asignación de columnas individuales entre el origen y el destino.
-   Copie solo un subconjunto de columnas si selecciona **Omitir** para las columnas que no desea copiar.

Para más información, vea [Asignaciones de columnas](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md).  

**Vista previa**  
Opcionalmente, haga clic en **Vista previa** para obtener una vista previa de hasta 200 filas de datos de ejemplo en el cuadro de diálogo **Vista previa de los datos**. Esto confirma que el asistente va a copiar los datos que quiere copiar. Para más información, vea [Vista previa de los datos](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md).  
  
Después de obtener una vista previa de los datos, es posible que quiera cambiar las opciones que seleccionó en páginas anteriores del asistente. Para realizar estas modificaciones, vuelva a la página **Configurar el destino del archivo plano** y después haga clic en **Atrás** para volver a las páginas anteriores en las que puede cambiar sus selecciones.  

## <a name="whats-next"></a>¿Qué debe hacer a continuación?  
 Después de especificar las opciones de formato del archivo plano de destino, la página siguiente es **Guardar y ejecutar paquete**. En esta página, especifique si quiere ejecutar la operación inmediatamente. Según la configuración, también puede guardar el paquete de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] creado por el asistente para personalizarlo y volver a usarlo más adelante. Para más información, vea [Guardar y ejecutar paquete](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md).  
