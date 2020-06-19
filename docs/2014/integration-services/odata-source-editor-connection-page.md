---
title: Editor de origen OData (página conexión) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- Sql12.dts.designer.odatasource.connection.f1
ms.assetid: 20bcd347-4547-4fad-b182-9571030101df
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 64d40dd2a6f0f2568e7e7817a3a9366be8f83cc4
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965085"
---
# <a name="odata-source-editor-connection-page"></a>Editor de origen OData (página Conexión)
  Use la página **Conexión** del cuadro de diálogo **Editor de origen OData** para seleccionar el administrador de conexiones OData para el origen OData. Esta página también permite especificar una ruta de acceso de colección o a recursos y las opciones de consulta deseadas para indicar qué datos hay que recuperar del origen OData. Para obtener más información acerca del origen OData, vea [OData Source](data-flow/odata-source.md).  
  
## <a name="static-options"></a>Opciones estáticas  
 **Administrador de conexiones OData**  
 Seleccione un administrador de conexiones de la lista o cree una conexión haciendo clic en **Nuevo**.  
  
 **Nuevo**  
 Cree un administrador de conexiones mediante el cuadro de diálogo **Editor del administrador de conexiones OData** .  
  
 **Usar ruta de acceso de colección o a recursos**  
 Especifique el método para seleccionar datos del origen.  
  
|Opción|Descripción|  
|------------|-----------------|  
|Colección|Recupera datos del origen OData mediante un nombre de colección.|  
|Ruta de acceso a recursos|Recupera datos del origen OData mediante una ruta de acceso a recursos.|  
  
 **Opciones de consulta**  
 Especifique las opciones de consulta.  Por ejemplo: $top=5  
  
 **Dirección URL de fuente**  
 Muestra la dirección URL de la fuente de solo lectura según las opciones que ha seleccionado en este cuadro de diálogo.  
  
 **Versión preliminar**  
 Muestra una vista previa de los resultados mediante el cuadro de diálogo **Vista previa** . **Vista previa** puede mostrar hasta 20 filas.  
  
## <a name="dynamic-options"></a>Opciones dinámicas  
  
### <a name="use-collection-or-resource-path--collection"></a>Usar ruta de acceso de colección o de recurso = Colección  
 **Colección**  
 Seleccione una colección de la lista desplegable.  
  
### <a name="use-collection-or-resource-path--resource-path"></a>Usar ruta de acceso de colección o de recurso = Ruta de acceso a recursos  
 **Ruta de acceso a recursos**  
 Escriba una ruta de acceso a recursos. Por ejemplo: Empleados  
  
## <a name="see-also"></a>Consulte también  
 [Editor de origen OData &#40;página columnas&#41;](../../2014/integration-services/odata-source-editor-columns-page.md)   
 [Editor de origen OData &#40;página salida de error&#41;](../../2014/integration-services/odata-source-editor-error-output-page.md)   
 [Administrador de conexiones OData](connection-manager/odata-connection-manager.md)  
  
  
