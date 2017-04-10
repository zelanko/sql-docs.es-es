---
title: "Editor de origen OData (p&#225;gina Conexi&#243;n) | Microsoft Docs"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.odatasource.connection.f1"
ms.assetid: 20bcd347-4547-4fad-b182-9571030101df
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# Editor de origen OData (p&#225;gina Conexi&#243;n)
  Use la página **Conexión** del cuadro de diálogo **Editor de origen OData** para seleccionar el administrador de conexiones OData para el origen OData. Esta página también permite especificar una ruta de acceso de colección o a recursos y las opciones de consulta deseadas para indicar qué datos hay que recuperar del origen OData. Para obtener más información acerca del origen OData, vea [OData Source](../../integration-services/data-flow/odata-source.md).  
  
## Opciones estáticas  
 **Administrador de conexiones OData**  
 Seleccione un administrador de conexiones de la lista o cree una conexión haciendo clic en **Nuevo**.  
  
 Después de seleccionar o crear un administrador de conexiones, el cuadro de diálogo muestra la versión del Protocolo OData que está utilizando el Administrador de conexiones.  
  
 **Nuevo**  
 Cree un administrador de conexiones mediante el cuadro de diálogo **Editor del administrador de conexiones OData**.  
  
 **Usar ruta de acceso de colección o a recursos**  
 Especifique el método para seleccionar datos del origen.  
  
|Opción|Description|  
|------------|-----------------|  
|Collection|Recupera datos del origen OData mediante un nombre de colección.|  
|Ruta de acceso a recursos|Recupera datos del origen OData mediante una ruta de acceso a recursos.|  
  
 **Opciones de consulta**  
 Especifique las opciones de consulta.  Por ejemplo: $top=5  
  
 **Dirección URL de fuente**  
 Muestra la dirección URL de la fuente de solo lectura según las opciones que ha seleccionado en este cuadro de diálogo.  
  
 **Vista previa**  
 Muestra una vista previa de los resultados mediante el cuadro de diálogo **Vista previa**. **Vista previa** puede mostrar hasta 20 filas.  
  
## Opciones dinámicas  
  
### Usar ruta de acceso de colección o de recurso = Colección  
 **Collection**  
 Seleccione una colección de la lista desplegable.  
  
### Usar ruta de acceso de colección o de recurso = Ruta de acceso a recursos  
 **Ruta de acceso a recursos**  
 Escriba una ruta de acceso a recursos. Por ejemplo: Empleados  
  
## Vea también  
 [Editor de origen OData &#40;página Columnas&#41;](../../integration-services/data-flow/odata-source-editor-columns-page.md)   
 [Editor de origen OData &#40;página Salida de error&#41;](../../integration-services/data-flow/odata-source-editor-error-output-page.md)   
 [Administrador de conexiones OData](../../integration-services/connection-manager/odata-connection-manager.md)  
  
  