---
title: Editor de destino de ODBC (página Administrador de conexiones) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.odbcdest.connection.f1
ms.assetid: f6d9c6c2-e4c4-468b-9e0d-af7b9609614d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 281bbda38a6711efd4e2ffae7afbfa17d689254b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66057205"
---
# <a name="odbc-destination-editor-connection-manager-page"></a>Editor de destino de ODBC (página Administrador de conexiones)
  Use la página **Administrador de conexiones** del cuadro de diálogo **Editor de destino de ODBC** para seleccionar el administrador de conexiones de ODBC para el destino. Esta página también permite seleccionar una tabla o vista de la base de datos.  
  
 Para obtener más información acerca del destino de ODBC, vea [ODBC Destination](data-flow/odbc-destination.md).  
  
 **Para abrir la página Administrador de conexiones del Editor de destino de ODBC**  
  
## <a name="task-list"></a>Lista de tareas  
  
-   En [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], abra el paquete [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] que tiene el destino de ODBC.  
  
-   En la pestaña **Flujo de datos** , haga doble clic en el destino de ODBC.  
  
-   En el **Editor de destino de ODBC**, haga clic en **Administrador de conexiones**.  
  
## <a name="options"></a>Opciones  
  
### <a name="connection-manager"></a>Administrador de conexiones  
 Seleccione un administrador de conexiones de ODBC existente en la lista o haga clic en Nueva para crear una nueva conexión. La conexión puede ser a cualquier base de datos compatible con ODBC.  
  
### <a name="new"></a>New  
 Haga clic en **Nueva**. Se abrirá el cuadro de diálogo **Configurar el administrador de conexiones ODBC** , donde puede crear un administrador de conexiones nuevo.  
  
### <a name="data-access-mode"></a>Modo de acceso a datos  
 Seleccione el método para cargar datos en el destino. Las opciones se muestran en la tabla siguiente:  
  
|Opción|Descripción|  
|------------|-----------------|  
|Nombre de la tabla - Lote|Seleccione esta opción para configurar el destino de ODBC de manera que funcione en modo por lotes. Cuando seleccione esta opción, aparecerán las opciones siguientes:|  
||**Nombre de la tabla o la vista**: seleccione una tabla o vista disponible en la lista.<br /><br /> Esta lista contiene solo las 1000 primeras tablas. Si la base de datos contiene más de 1000 tablas, puede escribir el principio de un nombre de tabla o usar el carácter comodín (\*) para escribir cualquier parte del nombre con el fin de mostrar las tablas que quiere usar.<br /><br /> **Tamaño del lote**: escriba el tamaño del lote para la carga masiva. Es el número de filas cargadas como un lote.|  
|Nombre de la tabla - Fila a fila|Seleccione esta opción para configurar el destino de ODBC de manera que se inserte cada una de las filas en la tabla de destino de una en una. Cuando seleccione esta opción, aparecerá la opción siguiente:|  
||**Nombre de la tabla o la vista**: seleccione en la lista una tabla o vista disponible en la base de datos.<br /><br /> Esta lista contiene solo las 1000 primeras tablas. Si la base de datos contiene más de 1000 tablas, puede escribir el principio de un nombre de tabla o usar el comodín (*) para escribir cualquier parte del nombre con el fin de mostrar la tabla o las tablas que desea usar.|  
  
### <a name="preview"></a>Vista previa  
 Haga clic en **Vista previa** para ver hasta 200 filas de datos para la tabla que ha seleccionado.  
  
## <a name="see-also"></a>Consulte también  
 [Propiedades personalizadas del destino ODBC](data-flow/odbc-destination-custom-properties.md)   
 [Editor de destino de ODBC &#40;página asignaciones&#41;](../../2014/integration-services/odbc-destination-editor-mappings-page.md)   
 [Editor de destinos de ODBC &#40;página Salida de error&#41;](../../2014/integration-services/odbc-destination-editor-error-output-page.md)  
  
  
