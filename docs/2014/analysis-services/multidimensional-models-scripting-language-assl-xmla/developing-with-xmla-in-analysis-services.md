---
title: Desarrollo con XMLA en Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- XML for Analysis, data mining
- commands [XML for Analysis]
- data mining [XML for Analysis]
- XMLA, data mining
- XML for Analysis, Analysis Services tasks
- XMLA, Analysis Services tasks
ms.assetid: 54445ee7-720c-4683-99a6-e75b3dcca904
author: minewiskan
ms.author: owend
ms.openlocfilehash: 2f5455b71306b3dd75406f107e5c1e971f6b923b
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545007"
---
# <a name="developing-with-xmla-in-analysis-services"></a>Desarrollar con XMLA en Analysis Services
  XML for Analysis (XMLA) es un protocolo XML basado en SOAP, diseñado específicamente para el acceso universal a los datos de cualquier origen de datos multidimensionales estándar a los que se puede acceder mediante una conexión HTTP. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa XMLA como único protocolo al comunicar con aplicaciones cliente. Básicamente, todas las bibliotecas de cliente admitidas por Analysis Services formulan solicitudes y respuestas en XMLA.  
  
 Como desarrollador, puede usar XMLA para integrar una aplicación cliente con [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], sin dependencias en las interfaces COM o .NET Framework. Los requisitos de la aplicación que incluyen el hospedaje en una amplia variedad de plataformas se pueden satisfacer utilizando XMLA y una conexión HTTP a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cumple totalmente la especificación 1.1 de XMLA, pero también la extiende para habilitar la definición de datos, la manipulación de datos y el soporte de control de datos. Se hace referencia a las extensiones de Analysis Services como Analysis Services Scripting Language (ASSL). El uso conjunto de XMLA y ASSL habilita un conjunto más amplio de funciones que las proporcionadas por XMLA en solitario. Para obtener más información sobre ASSL, vea [desarrollar con Analysis Services lenguaje de scripting &#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Administrar conexiones y sesiones &#40;XMLA&#41;](managing-connections-and-sessions-xmla.md)|Describe cómo conectar con una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y cómo administrar las sesiones y la disponibilidad de estados en XMLA.|  
|[Control de errores y advertencias &#40;XMLA&#41;](handling-errors-and-warnings-xmla.md)|Describe cómo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] devuelve información sobre errores y advertencias para los métodos y comandos en XMLA.|  
|[Definir e identificar objetos &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects)|Describe identificadores de objetos y referencias a objetos y cómo usar identificadores y referencias dentro de los comandos XMLA.|  
|[Administrar transacciones &#40;XMLA&#41;](managing-transactions-xmla.md)|Detalla cómo usar los comandos [BeginTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/begintransaction-element-xmla), [CommitTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/committransaction-element-xmla)y [RollbackTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/rollbacktransaction-element-xmla) para definir y administrar explícitamente una transacción en la sesión XMLA actual.|  
|[Cancelar comandos &#40;&#41;XMLA](../multidimensional-models-scripting-language-assl-xmla/canceling-commands-xmla.md)|Describe cómo usar el comando [Cancel](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/cancel-element-xmla)para cancelar comandos, sesiones y conexiones en XMLA.|  
|[Realizar operaciones por lotes &#40;XMLA&#41;](performing-batch-operations-xmla.md)|Describe cómo usar el comando [batch](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla) para ejecutar varios comandos XMLA, en serie o en paralelo, dentro de la misma transacción o como transacciones independientes, utilizando un solo método [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) de XMLA.|  
|[Crear y modificar objetos &#40;XMLA&#41;](creating-and-altering-objects-xmla.md)|Describe cómo usar los comandos [Create](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla), [ALTER](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla)y [Delete](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/delete-element-xmla) , junto con los elementos del lenguaje de scripting de Analysis Services (ASSL), para definir, cambiar o quitar objetos de una [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instancia de.|  
|[Bloquear y desbloquear bases de datos &#40;XMLA&#41;](locking-and-unlocking-databases-xmla.md)|Detalla cómo usar los comandos [Lock](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla) y [Unlock para](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla) bloquear y desbloquear una [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] base de datos.|  
|[Procesar objetos &#40;XMLA&#41;](processing-objects-xmla.md)|Describe cómo usar el comando [Process](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla) para procesar un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] objeto.|  
|[Mezclar particiones &#40;&#41;XMLA](merging-partitions-xmla.md)|Describe cómo usar el comando [MergePartitions](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/mergepartitions-element-xmla) para mezclar particiones en una [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instancia de.|  
|[Diseñar agregaciones &#40;XMLA&#41;](designing-aggregations-xmla.md)|Describe cómo usar el comando [DesignAggregations](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/designaggregations-element-xmla) , ya sea en modo iterativo o por lotes, para diseñar agregaciones para un diseño de agregaciones en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[Restaurar, sincronizar y realizar copias de seguridad de bases de datos &#40;XMLA&#41;](backing-up-restoring-and-synchronizing-databases-xmla.md)|Describe cómo usar los comandos [backup](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/backup-element-xmla) y [restore](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla) para realizar copias de seguridad y restaurar una [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] base de datos desde un archivo de copia de seguridad.<br /><br /> También describe cómo usar el comando [Synchronize](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla) para sincronizar una [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] base de datos con una base de datos existente en la misma instancia o en una instancia diferente.|  
|[Insertar, actualizar y quitar miembros &#40;XMLA&#41;](inserting-updating-and-dropping-members-xmla.md)|Describe cómo usar los comandos [Insert](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/insert-element-xmla), [Update](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)y [Drop](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/drop-element-xmla) para agregar, cambiar o eliminar miembros de una dimensión habilitada para escritura.|  
|[Actualizar celdas &#40;XMLA&#41;](updating-cells-xmla.md)|Describe cómo usar el comando [UpdateCells](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/updatecells-element-xmla) para cambiar los valores de las celdas de una partición habilitada para escritura.|  
|[Administrar cachés &#40;XMLA&#41;](managing-caches-xmla.md)|Detalla cómo usar el comando [ClearCache](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/clearcache-element-xmla) para borrar las memorias caché de los [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] objetos.|  
|[Seguimientos de supervisión &#40;XMLA&#41;](monitoring-traces-xmla.md)|Describe cómo usar el comando [subscribe](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/subscribe-element-xmla) para suscribirse a un seguimiento existente y supervisarlo en una [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instancia de.|  
  
## <a name="data-mining-with-xmla"></a>Minería de datos con XMLA  
 XML for Analysis es totalmente compatible con los conjuntos de filas de esquema de minería de datos. Estos conjuntos de filas proporcionan información para consultar modelos de minería de datos mediante el método [Discover](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover) . Para obtener más información acerca de los conjuntos de filas de esquema de minería de datos, vea [conjuntos de filas de esquema de minería de datos](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/data-mining-schema-rowsets) 
  
 Para obtener más información acerca de DMX, consulte [extensiones de minería de datos &#40;referencia de dmx&#41;](/sql/dmx/data-mining-extensions-dmx-reference).  
  
## <a name="namespace-and-schema"></a>Espacio de nombres y esquema  
  
### <a name="namespace"></a>Espacio de nombres  
 El esquema definido en esta especificación usa el espacio de nombres XML `https://schemas.microsoft.com/AnalysisServices/2003/Engine` y la abreviatura estándar "DDL".  
  
### <a name="schema"></a>Schema  
 La definición de un esquema de lenguaje de definición de esquema XML (XSD) para el lenguaje de definición de objeto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se basa en la definición de la jerarquía y los elementos del esquema en esta sección.  
  
## <a name="extensibility"></a>Extensibilidad  
 La extensibilidad del esquema de lenguaje de definición de objeto se proporciona por medio de un elemento `Annotation` que se incluye en todos los objetos. Este elemento puede contener XML válido de cualquier espacio de nombres XML (excepto el espacio de nombres de destino que define el DDL), sujeto a las reglas siguientes:  
  
-   El XML solo puede contener elementos.  
  
-   Cada elemento debe tener un nombre único. Se recomienda que el valor de `Name` haga referencia al espacio de nombres de destino.  
  
 Estas reglas se imponen para que el contenido de la etiqueta `Annotation` pueda exponerse como un conjunto de pares nombre/valor a través de la versión 9.0 de DSO (Objetos de ayuda para la toma de decisiones).  
  
 No se pueden conservar los comentarios y los espacios en blanco dentro de la etiqueta `Annotation` que no se incluyen dentro de un elemento secundario. Además, todos los elementos deben ser de lectura y escritura; los elementos de solo lectura se omiten.  
  
 El esquema de lenguaje de definición de objeto es de tipo cerrado; el servidor no permite la sustitución de tipos derivados de los elementos definidos en el esquema. Por lo tanto, el servidor solamente acepta el conjunto de elementos aquí definidos y ningún otro elemento o atributo. Los elementos desconocidos hacen que el motor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] genere un error.  
  
## <a name="see-also"></a>Consulte también  
 [Desarrollo con Analysis Services lenguaje de scripting &#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [Descripción de la arquitectura OLAP de Microsoft](../multidimensional-models/olap-physical/understanding-microsoft-olap-architecture.md)  
  
  
