---
title: "Configuraci&#243;n del destino de streaming de datos | Microsoft Docs"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "SQL11.DTS.DESIGNER.DATASTREAMINGDEST.F1"
ms.assetid: bcdbb833-20c8-47ff-a641-bb517f9a1af3
caps.latest.revision: 7
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 7
---
# Configuraci&#243;n del destino de streaming de datos
  Configure el destino de streaming de datos en el cuadro de diálogo **Advanced Editor for Data Streaming Destination** (Editor avanzado para destino de streaming de datos). Abra este cuadro de diálogo; para ello, haga doble clic en el componente, o bien haga clic con el botón derecho en el componente del diseñador del flujo de datos y luego haga clic en **Editar**.  
  
 Este cuadro de diálogo tiene tres pestañas: **Propiedades de componente**, **Columnas de entrada**y **Propiedades de entrada y salida**.  
  
## Pestaña Propiedades de componente  
 Esta pestaña contiene los campos editables siguientes:  
  
|Campo|Description|  
|-----------|-----------------|  
|Nombre|Nombre del componente de destino de streaming de datos en el paquete.|  
|ValidateExternalMetadata|Indica si el componente se valida con orígenes de datos externos en el tiempo de diseño. Si se establece en false, la validación con orígenes de datos externos se retrasa hasta el tiempo de ejecución.|  
|IDColumnName|La vista generada por el asistente para publicación de fuentes de distribución de datos tiene esta columna de ID adicional. La columna de ID sirve como valor EntityKey para los datos de salida del flujo de datos cuando otras aplicaciones consumen los datos como una fuente OData.<br /><br /> El nombre predeterminado para esta columna es _ID. Puede especificar un nombre diferente para la columna ID.|  
  
## Pestaña Columnas de entrada  
 En el panel superior de esta pestaña, verá todas las columnas de entrada disponibles. Seleccione las columnas que desea incluir en la salida de este componente. Las columnas seleccionadas se muestran en una lista en el panel inferior. Puede cambiar el nombre de la columna de salida escribiendo el nuevo nombre en el campo **Alias de salida** de la lista.  
  
## Pestaña Propiedades de entrada y salida  
 Al igual que ocurre con la pestaña Columnas de entrada, puede cambiar los nombres de las columnas de salida en esta pestaña. En la vista de árbol de la izquierda, expanda **Data Streaming Destination Input** (Entrada de destino de streaming de datos) y luego expanda **Columnas de entrada**. Haga clic en el nombre de la columna de entrada y cambie el nombre de la columna de salida en el panel derecho.  
  
## Vea también  
 [Destino de streaming de datos](../../integration-services/data-flow/data-streaming-destination.md)   
 [Tutorial: Publicar un paquete SSIS como una vista SQL](../../integration-services/data-flow/walkthrough-publish-an-ssis-package-as-a-sql-view.md)  
  
  