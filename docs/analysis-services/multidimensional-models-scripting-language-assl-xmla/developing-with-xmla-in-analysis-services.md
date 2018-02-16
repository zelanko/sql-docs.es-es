---
title: Desarrollar con XMLA en Analysis Services | Documentos de Microsoft
ms.custom: 
ms.date: 02/14/2018
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- XML for Analysis, data mining
- commands [XML for Analysis]
- data mining [XML for Analysis]
- XMLA, data mining
- XML for Analysis, Analysis Services tasks
- XMLA, Analysis Services tasks
ms.assetid: 54445ee7-720c-4683-99a6-e75b3dcca904
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6bf41801ce6b81c532d8be56b5afdfe4fd5e901f
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2018
---
# <a name="developing-with-xmla-in-analysis-services"></a>Desarrollar con XMLA en Analysis Services
  XML for Analysis (XMLA) es un protocolo XML basado en SOAP, diseñado específicamente para el acceso universal a los datos de cualquier origen de datos multidimensionales estándar a los que se puede acceder mediante una conexión HTTP. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa XMLA como único protocolo al comunicar con aplicaciones cliente. Básicamente, todas las bibliotecas de cliente admitidas por Analysis Services formulan solicitudes y respuestas en XMLA.  
  
 Como desarrollador, puede usar XMLA para integrar una aplicación cliente con [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], sin dependencias en las interfaces COM o .NET Framework. Los requisitos de la aplicación que incluyen el hospedaje en una amplia variedad de plataformas se pueden satisfacer utilizando XMLA y una conexión HTTP a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] es totalmente compatible con la especificación 1.1 de XMLA, pero también amplía para habilitar la definición de datos, manipulación de datos y la compatibilidad con el control de datos. Se hace referencia a las extensiones de Analysis Services como Analysis Services Scripting Language (ASSL). El uso conjunto de XMLA y ASSL habilita un conjunto más amplio de funciones que las proporcionadas por XMLA en solitario. Para obtener más información acerca de ASSL, vea [desarrollar con Analysis Services Scripting Language &#40; ASSL &#41; ](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Description|  
|-----------|-----------------|  
|[Administrar las conexiones y sesiones &#40; XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)|Describe cómo conectar con una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y cómo administrar las sesiones y la disponibilidad de estados en XMLA.|  
|[Controlar errores y advertencias &#40; XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/handling-errors-and-warnings-xmla.md)|Describe cómo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] devuelve información sobre errores y advertencias para los métodos y comandos en XMLA.|  
|[Definir e identificar objetos &#40; XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/defining-and-identifying-objects-xmla.md)|Describe identificadores de objetos y referencias a objetos y cómo usar identificadores y referencias dentro de los comandos XMLA.|  
|[Administración de transacciones &#40; XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-transactions-xmla.md)|Detalla cómo utilizar el [BeginTransaction](../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md), [CommitTransaction](../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md), y [RollbackTransaction](../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md) comandos para definir y administrar una transacción en el XMLA actual explícitamente sesión.|  
|[Cancelar comandos &#40; XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/canceling-commands-xmla.md)|Describe cómo utilizar el [cancelar](../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)comando para cancelar comandos, sesiones y conexiones en XMLA.|  
|[Realizar operaciones por lotes &#40; XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/performing-batch-operations-xmla.md)|Describe cómo utilizar el [lote](../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md) comando para ejecutar XMLA varios comandos, en serie o en paralelo, ya sea en la misma transacción o como transacciones independientes, con un único XMLA [Execute](../../analysis-services/xmla/xml-elements-methods-execute.md) método.|  
|[Creación y modificación de objetos &#40; XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/creating-and-altering-objects-xmla.md)|Describe cómo utilizar el [crear](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md), [Alter](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md), y [eliminar](../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md) comandos, junto con elementos de Analysis Services Scripting Language (ASSL), para definir, cambiar o quitar objetos de un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instancia.|  
|[Bloquear y desbloquear bases de datos &#40; XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/locking-and-unlocking-databases-xmla.md)|Detalla cómo utilizar el [bloqueo](../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md) y [Unlock](../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md) comandos para bloquear y desbloquear un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] base de datos.|  
|[Procesar objetos &#40; XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/processing-objects-xmla.md)|Describe cómo utilizar el [proceso](../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md) comando al proceso una [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] objeto.|  
|[Mezclar particiones &#40; XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/merging-partitions-xmla.md)|Describe cómo utilizar el [MergePartitions](../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md) comando mezclar particiones en un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instancia.|  
|[Diseñar agregaciones &#40; XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/designing-aggregations-xmla.md)|Describe cómo utilizar el [DesignAggregations](../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md) comando, ya sea en iterativo o en modo por lotes, para diseñar agregaciones para un diseño de agregaciones en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|[Copia de seguridad, restaurar y sincronizar las bases de datos &#40; XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)|Describe cómo utilizar el [copia de seguridad](../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md) y [restaurar](../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md) comandos para copia de seguridad y restaurar un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] base de datos desde un archivo de copia de seguridad.<br /><br /> También describe cómo utilizar el [sincronizar](../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md) comando para sincronizar un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] base de datos con una base de datos existente en la misma instancia o en una instancia diferente.|  
|[Insertar, actualizar y quitar miembros &#40; XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md)|Describe cómo utilizar el [insertar](../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md), [actualización](../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md), y [Drop](../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md) comandos para agregar, cambiar o eliminar miembros de una dimensión habilitada para escritura.|  
|[Actualizar celdas &#40; XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/updating-cells-xmla.md)|Describe cómo utilizar el [UpdateCells](../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md) comando para cambiar los valores de las celdas de una partición habilitada para escritura.|  
|[Administración de las memorias caché &#40; XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-caches-xmla.md)|Detalla cómo utilizar el [ClearCache](../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md) comando para borrar las cachés de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] objetos.|  
|[Supervisar seguimientos &#40; XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/monitoring-traces-xmla.md)|Describe cómo utilizar el [suscribir](../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md) comando para suscribirse a y supervisar un seguimiento existente en un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instancia.|  
  
## <a name="data-mining-with-xmla"></a>Minería de datos con XMLA  
 XML for Analysis es totalmente compatible con los conjuntos de filas de esquema de minería de datos. Estos conjuntos de filas proporcionan información para consultar modelos de minería de datos utilizando la [Discover](../../analysis-services/xmla/xml-elements-methods-discover.md) método. Para obtener más información acerca de conjuntos de filas de esquema de minería de datos, vea [conjuntos de filas de esquema de minería de datos](../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
 Para obtener más información acerca de DMX, vea [extensiones de minería de datos &#40; DMX &#41; Referencia](../../dmx/data-mining-extensions-dmx-reference.md).  
  
## <a name="namespace-and-schema"></a>Espacio de nombres y esquema  
  
### <a name="namespace"></a>Espacio de nombres  
 El esquema definido en esta especificación utiliza el espacio de nombres XML `http://schemas.microsoft.com/AnalysisServices/2003/Engine` y la abreviatura estándar "DDL".  
  
### <a name="schema"></a>Esquema  
 La definición de un esquema de lenguaje de definición de esquema XML (XSD) para el lenguaje de definición de objeto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se basa en la definición de la jerarquía y los elementos del esquema en esta sección.  
  
## <a name="extensibility"></a>Extensibilidad  
 Extensibilidad del esquema de lenguaje de definición de objeto se proporciona por medio de un **anotación** elemento que se incluye en todos los objetos. Este elemento puede contener XML válido de cualquier espacio de nombres XML (excepto el espacio de nombres de destino que define el DDL), sujeto a las reglas siguientes:  
  
-   El XML solo puede contener elementos.  
  
-   Cada elemento debe tener un nombre único. Se recomienda que el valor de **nombre** hacer referencia el espacio de nombres de destino.  
  
 Estas reglas se imponen para que el contenido de la **anotación** etiqueta se puede exponer como un conjunto de pares de nombre/valor a través de Decision Support Objects (DSO) 9.0.  
  
 Comentarios y espacios en blanco dentro del **anotación** etiqueta que no se incluyen con un elemento secundario no puede conservarse. Además, todos los elementos deben ser de lectura y escritura; los elementos de solo lectura se omiten.  
  
 El esquema de lenguaje de definición de objeto es de tipo cerrado; el servidor no permite la sustitución de tipos derivados de los elementos definidos en el esquema. Por lo tanto, el servidor solamente acepta el conjunto de elementos aquí definidos y ningún otro elemento o atributo. Los elementos desconocidos hacen que el motor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] genere un error.  
  
## <a name="see-also"></a>Vea también  
 [Desarrollar con Analysis Services Scripting Language &#40; ASSL &#41;](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [Descripción de la arquitectura OLAP de Microsoft](../../analysis-services/multidimensional-models/olap-physical/understanding-microsoft-olap-architecture.md)  
  
  
