---
title: Notificaciones (cuadro de diálogo Opciones de almacenamiento) (Analysis Services - datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.partitiondesigner.partitionstoragesettings.setstorageoptions.notifications.f1
ms.assetid: 5675cdbf-bfaa-4b6e-b716-31b8e9da72b4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 23845118c4c202db781fe325c4afc2402ceee271
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66072202"
---
# <a name="notifications-storage-options-dialog-box-analysis-services---multidimensional-data"></a>Notificaciones (cuadro de diálogo Opciones de almacenamiento) (Analysis Services - Datos multidimensionales)
  Use la pestaña **Notificaciones** del cuadro de diálogo **Opciones de almacenamiento** en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para establecer el método de notificación y las configuraciones relacionadas para una dimensión, un cubo, un grupo de medida o una partición.  
  
> [!NOTE]  
>  Antes de modificar estos parámetros de configuración, debe estar familiarizado con la funcionalidad del modo de almacenamiento y del almacenamiento en caché automático. Para más información, vea [Almacenamiento en caché automático &#40;Particiones&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).  
  
## <a name="options"></a>Opciones  
  
|Término|Definición|  
|----------|----------------|  
|**Modo de almacenamiento**|Seleccione el modo de almacenamiento que debe utilizarse para el objeto.<br /><br /> **MOLAP**<br /> El objeto utiliza almacenamiento OLAP multidimensional (MOLAP).<br /><br /> **HOLAP**<br /> El objeto utiliza almacenamiento OLAP híbrido (HOLAP).<br /><br /> **ROLAP**<br /> El objeto utiliza almacenamiento OLAP relacional (ROLAP).|  
|**Habilitar almacenamiento en caché automático**|Habilitar el almacenamiento en caché automático.<br /><br /> Nota: Si no se selecciona esta opción, todas las opciones excepto **modo de almacenamiento** están deshabilitados.|  
|**SQL Server**|Usa un mecanismo de rastreo especializado en [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para identificar cambios en tablas subyacentes para el objeto.|  
|**Especificar tablas de seguimiento**|Especifique las tablas subyacentes de las que debe realizarse el seguimiento para el objeto y, después, escriba una lista de tablas delimitadas por el carácter de punto y coma (;) o haga clic en el botón de puntos suspensivos ( **…** ) para abrir el cuadro de diálogo **Objetos relacionales** y elija las tablas de las que debe realizarse el seguimiento. Para obtener más información, vea [Cuadro de diálogo Objetos relacionales &#40;Analysis Services - Datos multidimensionales&#41;](relational-objects-dialog-box-analysis-services-multidimensional-data.md).<br /><br /> Si esta opción no está seleccionada, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] intenta determinar la lista de tablas subyacentes de las que debe realizarse el seguimiento para el objeto, si se cumplen determinados requisitos. Para obtener más información sobre estos requisitos, vea [Almacenamiento en caché automático &#40;Particiones&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).|  
|**Cliente iniciado**|Seleccione el comando XMLA (XML for Analysis) `NotifyTableChange` para identificar cambios en tablas subyacentes para el objeto. Por lo general, esta opción se activa si se desea utilizar un proceso de notificación basado en el cliente.|  
|**Especificar tablas de seguimiento**|Seleccione esta opción para especificar las tablas subyacentes de las que debe realizarse el seguimiento para el objeto y, después, escriba una lista de tablas delimitadas por el carácter de punto y coma (;) o haga clic en el botón de puntos suspensivos ( **…** ) para abrir el cuadro de diálogo **Objetos relacionales** y elija las tablas de las que debe realizarse el seguimiento. Para obtener más información, vea [Cuadro de diálogo Objetos relacionales &#40;Analysis Services - Datos multidimensionales&#41;](relational-objects-dialog-box-analysis-services-multidimensional-data.md).<br /><br /> Si esta opción no está seleccionada, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] intenta determinar la lista de tablas subyacentes de las que debe realizarse el seguimiento para el objeto, si se cumplen determinados requisitos. Para obtener más información sobre estos requisitos, vea [Almacenamiento en caché automático &#40;Particiones&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).|  
|**Sondeo programado**|Utiliza un mecanismo de sondeo para identificar cambios ejecutando una serie de consultas en las tablas subyacentes para el objeto.|  
|**Intervalo de sondeo**|Especifica el intervalo y las unidades de tiempo correspondientes al período que debe transcurrir antes de que [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ejecute las consultas de sondeo y las consultas de procesamiento definidas en la cuadrícula de sondeo.|  
|**Habilitar actualizaciones incrementales**|Actualiza de manera incremental la caché MOLAP para un objeto basado en un conjunto de sondeos y consultas de procesamiento destinado a identificar únicamente datos adicionales. Si se activa esta opción, la consulta de sondeo se asocia con un identificador de tablas en la vista del origen de datos. La consulta de procesamiento se usa entonces para comparar el valor actual de la consulta de sondeo con el valor almacenado de la consulta de sondeo ejecutada anteriormente para identificar cambios.<br /><br /> Si esta opción no está seleccionada, la memoria caché MOLAP se actualiza por completo. La consulta de sondeo se utiliza para identificar que se ha producido un cambio y no se necesita ninguna consulta de procesamiento ni ningún identificador de tabla.|  
|**Cuadrícula de sondeo**|Contiene las consultas de sondeo, las consultas de procesamiento y los identificadores de tabla que [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] usa para sondear el origen de datos e identificar cambios en las tablas subyacentes para el objeto. La cuadrícula contiene las columnas siguientes:<br /><br /> **Consulta de sondeo**: Escriba la consulta singleton ejecutada en el intervalo de sondeo para identificar cambios para el objeto o haga clic en el botón de puntos suspensivos ( **…** ) para abrir el cuadro de diálogo **Crear consulta de sondeo** y defina la consulta singleton. Para obtener más información, vea [Cuadro de diálogo Crear consulta de sondeo &#40;Analysis Services - Datos multidimensionales&#41;](create-polling-query-dialog-box-analysis-services-multidimensional-data.md). Si la opción **Habilitar actualizaciones incrementales** está activada, la consulta de sondeo deberá devolver un valor que identifique el último registro agregado a la tabla que se identifica en **Tabla**. Si la opción **Habilitar actualizaciones incrementales** no está activada, la consulta de sondeo deberá devolver un valor que identifique la cantidad de registros actual de la tabla.<br /><br /> **Consulta de procesamiento**: Escriba la consulta ejecutada en el intervalo de sondeo para recuperar registros nuevos de la tabla identificada en **Tabla**, o haga clic en el botón de puntos suspensivos ( **…** ) para abrir el cuadro de diálogo **Crear consulta de procesamiento** y defina la consulta. Para obtener más información, vea [Cuadro de diálogo Crear consulta de procesamiento &#40;Analysis Services - Datos multidimensionales&#41;](create-processing-query-dialog-box-analysis-services-multidimensional-data.md). La consulta debe definirse parámetros para Aceptar dos parámetros: el valor anterior devuelto por la consulta en **consulta de sondeo** y el valor actual devuelto por la consulta en **consulta de sondeo**-que se puede usar para identificar y extraer únicamente los registros que se han agregado durante el período de sondeo. Tenga en cuenta que esta opción solo se habilita si la opción **Habilitar actualizaciones incrementales** está seleccionada.<br /><br /> **Tabla**: Escriba el identificador de la tabla en la cual la consulta de **Consulta de sondeo** realiza el seguimiento del último registro, o haga clic en el botón de puntos suspensivos ( **…** ) para abrir el cuadro de diálogo **Buscar tabla** y seleccione la tabla. Para obtener más información, vea [Cuadro de diálogo Buscar tabla &#40;Analysis Services - Datos multidimensionales&#41;](find-table-dialog-box-analysis-services-multidimensional-data.md).|  
  
## <a name="see-also"></a>Vea también  
 [Cuadro de diálogo de opciones de almacenamiento &#40;Analysis Services - datos multidimensionales&#41;](storage-options-dialog-box-analysis-services-multidimensional-data.md)  
  
  
