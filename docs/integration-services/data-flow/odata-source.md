---
title: Origen OData | Documentos de Microsoft
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.DTS.DESIGNER.ODATASOURCE.F1
- sql13.dts.designer.odatasource.connection.f1
- sql13.dts.designer.odatasource.columns.f1
- sql13.dts.designer.odatasource.erroroutput.f1
ms.assetid: cc9003c9-638e-432b-867e-e949d50cec90
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: ee79d0f1b31963b7d13aa07bf4603246139c3a7c
ms.openlocfilehash: 1e0ef2b7cca9509a58aeadca3903e8aec3b7b9b9
ms.contentlocale: es-es
ms.lasthandoff: 08/23/2017

---
# <a name="odata-source"></a>Origen OData
Use el componente de origen OData en un paquete SSIS para consumir datos de un servicio de Open Data Protocol (OData). El componente admite los protocolos OData v3 y v4.  
  
-   Protocolo OData V3, el componente admite los formatos de datos ATOM y JSON.  
  
-   Protocolo OData V4, el componente admite el formato de datos JSON.  

El origen OData incluye compatibilidad para los orígenes de datos siguientes:
-   Microsoft Dynamics AX en línea y Microsoft Dynamics CRM Online
-   Listas de SharePoint. Para ver todas las listas en un servidor de SharePoint, use la siguiente dirección URL: http://\<server > / _vti_bin/ListData.svc. Para obtener más información sobre las convenciones de direcciones URL de SharePoint, vea [Interfaz de REST de SharePoint Foundation](http://msdn.microsoft.com/library/ff521587.aspx).
  
## <a name="odata-format-and-performance"></a>Formato OData y el rendimiento
 La mayoría de los servicios de OData pueden devolver resultados en varios formatos. Puede especificar el formato del resultado establecer mediante el `$format` la opción de consulta. Los formatos como JSON y JSON Light son más eficaces que ATOM o XML, y pueden conseguir mejor rendimiento cuando se transfieren grandes cantidades de datos. En la tabla siguiente se muestran resultados de pruebas de ejemplo. Como puede ver, hubo una mejora del rendimiento del 30-53 % al cambiar de ATOM a JSON y del 67 % cuando se cambió de ATOM al nuevo formato JSON Light (disponible en WCF Data Services 5.1).  
  
|Filas|ATOM|JSON|JSON (Light)|  
|-|-|-|-|  
|10000|113 segundos|74 segundos|68 segundos|  
|1000000|1110 segundos|853 segundos|665 segundos|  
  
## <a name="related-topics-in-this-section"></a>Temas relacionados en esta sección  
  
-   [Tutorial: Usar el origen OData](../../integration-services/data-flow/tutorial-using-the-odata-source.md)  
  
-   [Modificar una consulta de origen OData en tiempo de ejecución](../../integration-services/data-flow/modify-odata-source-query-at-runtime.md)  
  
-   [Propiedades del origen OData](../../integration-services/data-flow/odata-source-properties.md)  
  
## <a name="odata-source-editor-connection-page"></a>Editor de origen OData (página Conexión)
  Use la página **Conexión** del cuadro de diálogo **Editor de origen OData** para seleccionar el administrador de conexiones OData para el origen OData. Esta página también permite especificar una ruta de acceso de colección o a recursos y las opciones de consulta deseadas para indicar qué datos hay que recuperar del origen OData. 
  
### <a name="static-options"></a>Opciones estáticas  
 **Administrador de conexiones OData**  
 Seleccione un administrador de conexiones de la lista o cree una conexión haciendo clic en **Nuevo**.  
  
 Después de seleccionar o crear un administrador de conexiones, el cuadro de diálogo muestra la versión del Protocolo OData que está utilizando el Administrador de conexiones.  
  
 **Nuevo**  
 Cree un administrador de conexiones mediante el cuadro de diálogo **Editor del administrador de conexiones OData** .  
  
 **Usar ruta de acceso de colección o a recursos**  
 Especifique el método para seleccionar datos del origen.  
  
|Opción|Description|  
|------------|-----------------|  
|Collection|Recupera datos del origen OData mediante un nombre de colección.|  
|Ruta de acceso a recursos|Recupera datos del origen OData mediante una ruta de acceso a recursos.|  
  
 **Opciones de consulta**  
 Especifique las opciones de consulta. Por ejemplo: `$top=5` 
  
 **Dirección URL de fuente**  
 Muestra solo lectura en función de las opciones que ha seleccionado en este cuadro de diálogo de dirección URL de fuente.  
  
 **Vista previa**  
 Muestra una vista previa de los resultados mediante el cuadro de diálogo **Vista previa** . **Vista previa** puede mostrar hasta 20 filas.  
  
### <a name="dynamic-options"></a>Opciones dinámicas  
  
#### <a name="use-collection-or-resource-path--collection"></a>Usar ruta de acceso de colección o de recurso = Colección  
 **Collection**  
 Seleccione una colección de la lista desplegable.  
  
#### <a name="use-collection-or-resource-path--resource-path"></a>Usar ruta de acceso de colección o de recurso = Ruta de acceso a recursos  
 **Resource path**  
 Escriba una ruta de acceso a recursos. Por ejemplo: Empleados  
  
## <a name="odata-source-editor-columns-page"></a>Editor de origen OData (página Columnas)
  Use la página **Columnas** del cuadro de diálogo **Editor de origen OData** para seleccionar las columnas externas (origen) que se van a incluir en la salida y asignarlas a columnas de salida.  
  
### <a name="options"></a>Opciones  
 **Columnas externas disponibles**  
 Muestra la lista de columnas de origen disponibles en el origen de datos. Use las casillas de la lista para agregar o quitar columnas a la tabla en la parte inferior de la página. Las columnas seleccionadas se agregan a la salida.  
  
 **Columna externa**  
 Muestra las columnas de origen que eligió incluir en la salida.  
  
 **Columna de salida**  
 Permite proporcionar un nombre único para cada columna de salida. El nombre predeterminado es el nombre de la columna externa (origen) seleccionada; sin embargo, puede elegir un nombre único y descriptivo.  
  
## <a name="odata-source-editor-error-output-page"></a>Editor de origen OData (página Salida de error)
  Use la página **Salida de error** del cuadro de diálogo **Editor de origen OData** para seleccionar opciones de control de errores y establecer las propiedades en las columnas de salida de errores.  
  
### <a name="options"></a>Opciones  
 **Entrada/salida**  
 Muestra el nombre del origen de datos.  
  
 **Columna**  
 Muestra las columnas externas (origen) que se han seleccionado en la página **Administrador de conexiones** del cuadro de diálogo **Editor de origen OData** .  
  
 **Error**  
 Permite especificar qué debe ocurrir cuando se produce un error: omitir el error, redirigir la fila o hacer que el componente no funcione.  
  
 **Temas relacionados:** [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **Truncamiento**  
 Permite especificar qué debe ocurrir cuando se produce un truncamiento: omitir el error, redirigir la fila o hacer que el componente no funcione.  
  
 **Description**  
 Muestra la descripción del error.  
  
 **Establecer este valor en las celdas seleccionadas**  
 Permite especificar qué debe ocurrir en todas las celdas seleccionadas cuando se produce un error o un truncamiento: omitir el error, redirigir la fila o hacer que el componente no funcione.  
  
 **Aplicar**  
 Aplica la opción de control de errores a las celdas seleccionadas.  
  
## <a name="see-also"></a>Vea también  
 [Administrador de conexiones OData](../../integration-services/connection-manager/odata-connection-manager.md)  
  
  

