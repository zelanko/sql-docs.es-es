---
title: "Editor de transformaci&#243;n B&#250;squeda (p&#225;gina General) | Microsoft Docs"
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
  - "sql13.dts.designer.lookuptransformation.general.f1"
ms.assetid: 4bd15e48-0feb-4f95-be91-5df58105dbfb
caps.latest.revision: 18
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 18
---
# Editor de transformaci&#243;n B&#250;squeda (p&#225;gina General)
  Utilice la página **General** del cuadro de diálogo Editor de transformación Búsqueda para seleccionar el modo de caché y el tipo de conexión, y especificar cómo administrar las filas sin entradas coincidentes.  
  
 Para obtener más información acerca de la transformación Búsqueda, vea [Lookup Transformation](../../../integration-services/data-flow/transformations/lookup-transformation.md).  
  
## Opciones  
 **Caché completa**  
 Generey cargue el conjunto de datos de referencia en la caché antes de que se ejecute la transformación Búsqueda.  
  
 **Caché parcial**  
 Genere el conjunto de datos de referencia durante la ejecución de la transformación Búsqueda. Cargue en la caché las filas con entradas coincidentes del conjunto de datos de referencia y las que no tienen entradas coincidentes.  
  
 **Sin caché**  
 Genere el conjunto de datos de referencia durante la ejecución de la transformación Búsqueda. No se carga ningún dato en la caché.  
  
 **Administrador de conexiones de caché**  
 Configure la transformación Búsqueda para utilizar un administrador de conexiones de caché. Esta opción solo está disponible si también está seleccionada la opción Caché completa.  
  
 **OLE DB, administrador de conexiones**  
 Configure la transformación Búsqueda para utilizar un administrador de conexiones OLE DB.  
  
 **Especificar cómo administrar las filas sin entradas coincidentes**  
 Seleccione una opción para administrar las filas que no coincidan por lo menos con una entrada del conjunto de datos de referencia.  
  
 Al seleccionar **Redirigir filas a resultados no coincidentes**, las filas se redirigen a un resultado sin coincidencia y no se tratan como errores. La opción **Error** de la página **Salida de error** del cuadro de diálogo **Editor de transformación Búsqueda** no está disponible.  
  
 Al seleccionar cualquier otra opción del cuadro de lista **Especifique cómo administrar las filas sin entradas coincidentes** , las filas se tratan como errores. La opción **Error** de la página **Salida de error** está disponible.  
  
## Recursos externos  
 Entrada del blog, [Lookup cache modes](http://go.microsoft.com/fwlink/?LinkId=219518) en blogs.msdn.com  
  
## Vea también  
 [Administrador de conexiones de caché](../../../integration-services/data-flow/transformations/cache-connection-manager.md)   
 [Editor de transformación Búsqueda &#40;página Conexión&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-connection-page.md)   
 [Editor de transformación Búsqueda &#40;página Columnas&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-columns-page.md)   
 [Editor de transformación Búsqueda &#40;página Avanzadas&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-advanced-page.md)   
 [Editor de transformación Búsqueda &#40;página Salida de error&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-error-output-page.md)  
  
  