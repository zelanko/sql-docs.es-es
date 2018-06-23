---
title: Editor de código fuente de OData (página conexión) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- Sql12.dts.designer.odatasource.connection.f1
ms.assetid: 20bcd347-4547-4fad-b182-9571030101df
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 35f67b1f60acd8fd65132f1d6fe71bff2d52c724
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36203446"
---
# <a name="odata-source-editor-connection-page"></a>Editor de origen OData (página Conexión)
  Use la página **Conexión** del cuadro de diálogo **Editor de origen OData** para seleccionar el administrador de conexiones OData para el origen OData. Esta página también permite especificar una ruta de acceso de colección o a recursos y las opciones de consulta deseadas para indicar qué datos hay que recuperar del origen OData. Para obtener más información acerca del origen OData, vea [OData Source](data-flow/odata-source.md).  
  
## <a name="static-options"></a>Opciones estáticas  
 **Administrador de conexiones OData**  
 Seleccione un administrador de conexiones de la lista o cree una conexión haciendo clic en **Nuevo**.  
  
 **Nueva**  
 Cree un administrador de conexiones mediante el cuadro de diálogo **Editor del administrador de conexiones OData** .  
  
 **Usar ruta de acceso de colección o a recursos**  
 Especifique el método para seleccionar datos del origen.  
  
|Opción|Descripción|  
|------------|-----------------|  
|Collection|Recupera datos del origen OData mediante un nombre de colección.|  
|Ruta de acceso a recursos|Recupera datos del origen OData mediante una ruta de acceso a recursos.|  
  
 **Opciones de consulta**  
 Especifique las opciones de consulta.  Por ejemplo: $top=5  
  
 **Dirección URL de fuente**  
 Muestra la dirección URL de la fuente de solo lectura según las opciones que ha seleccionado en este cuadro de diálogo.  
  
 **Vista previa**  
 Muestra una vista previa de los resultados mediante el cuadro de diálogo **Vista previa** . **Vista previa** puede mostrar hasta 20 filas.  
  
## <a name="dynamic-options"></a>Opciones dinámicas  
  
### <a name="use-collection-or-resource-path--collection"></a>Usar ruta de acceso de colección o de recurso = Colección  
 **Collection**  
 Seleccione una colección de la lista desplegable.  
  
### <a name="use-collection-or-resource-path--resource-path"></a>Usar ruta de acceso de colección o de recurso = Ruta de acceso a recursos  
 **Resource path**  
 Escriba una ruta de acceso a recursos. Por ejemplo: Empleados  
  
## <a name="see-also"></a>Vea también  
 [Editor de código fuente de OData &#40;página columnas&#41;](../../2014/integration-services/odata-source-editor-columns-page.md)   
 [Editor de código fuente de OData &#40;página de salida de Error&#41;](../../2014/integration-services/odata-source-editor-error-output-page.md)   
 [Administrador de conexiones OData](connection-manager/odata-connection-manager.md)  
  
  