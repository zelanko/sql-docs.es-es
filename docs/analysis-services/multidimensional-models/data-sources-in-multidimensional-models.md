---
title: "Orígenes de datos en modelos multidimensionales | Documentos de Microsoft"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- metadata [Analysis Services]
- Analysis Services objects, data sources
- storing data [Analysis Services], data sources
- data sources [Analysis Services], about data sources
- security [Analysis Services], data sources
- data sources [Analysis Services]
- storage [Analysis Services], data sources
ms.assetid: a16469d9-9d53-4e35-9982-fc06327a9d33
caps.latest.revision: 45
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fb419325bc8490fdfb62fb044cb81c81e111e6e3
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="data-sources-in-multidimensional-models"></a>Orígenes de datos en modelos multidimensionales
  Todos los datos que se importan o se cargan en un modelo multidimensional se originan en un origen de datos externo. Normalmente, los datos de origen son de un almacenamiento de datos diseñado para el informe de errores, pero pueden proceder de cualquier base de datos relacional a la que se acceda directa o indirectamente mediante un intermediario, como un paquete de [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Un objeto de **origen de datos** en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] especifica una conexión directa a un origen de datos externo. Además de la ubicación física, un objeto de origen de datos especifica la cadena de conexión, el proveedor de datos, las credenciales y otras propiedades que controlan el comportamiento de la conexión.  
  
 La información proporcionada por el objeto de origen de datos se utiliza durante las operaciones siguientes:  
  
-   Obtener información del esquema y otros metadatos utilizados para generar vistas del origen de datos en un modelo.  
  
-   Consultar o cargar los datos en un modelo durante el procesamiento.  
  
-   Ejecutar consultas con modelos de minería de datos o multidimensionales que usan el modo de almacenamiento ROLAP.  
  
-   Leer o escribir en particiones remotas.  
  
-   Conectar a objetos vinculados así como sincronizar desde el destino al origen.  
  
-   Realizar operaciones de reescritura que actualizan los datos de la tabla de hechos almacenados en una base de datos relacional.  
  
 Al generar un modelo multidimensional de abajo arriba, empiece por crear el objeto de origen de datos y luego uśelo para generar el objeto a continuación, una **vista del origen de datos**. Una vista del origen de datos es la capa de abstracción de datos del modelo. Se suele crear tras el objeto de origen de datos, usando el esquema de la base de datos de origen como base. No obstante, puede elegir otras maneras de crear un modelo, por ejemplo, comenzar con cubos y dimensiones y generar el esquema que mejor admite el diseño.  
  
 Independientemente de cómo se generan, cada modelo requiere al menos un objeto de origen de datos que especifique una conexión al origen de datos. Puede crear objetos de origen de datos en un único modelo para usar los datos de orígenes diferentes o variar las propiedades de conexión de objetos específicos.  
  
 Los objetos de origen de datos se pueden administrar independientemente de otros objetos del modelo. Después de crear un origen de datos, puede cambiar sus propiedades más tarde y después procesar previamente el modelo para asegurarse de que los datos se recuperan de forma correcta.  
  
## <a name="related-topics-and-tasks"></a>Temas y tareas relacionados  
  
|Tema|Description|  
|-----------|-----------------|  
|[Orígenes de datos admitidos &#40;SSAS - Multidimensionales&#41;](../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)|Describe los tipos de orígenes de datos que puede usar en un modelo multidimensional.|  
|[Crear un origen de datos &#40;SSAS multidimensional&#41;](../../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md)|Explica cómo agregar un objeto de origen de datos a un modelo multidimensional.|  
|[Eliminar un origen de datos en el Explorador de soluciones &#40;SSAS multidimensional&#41;](../../analysis-services/multidimensional-models/delete-a-data-source-in-solution-explorer-ssas-multidimensional.md)|Use este procedimiento para eliminar un objeto de origen de datos de un modelo multidimensional.|  
|[Establecer propiedades de origen de datos &#40;SSAS multidimensional&#41;](../../analysis-services/multidimensional-models/set-data-source-properties-ssas-multidimensional.md)|Describe cada propiedad y explica cómo configurar cada una.|  
|[Establezca las opciones de suplantación &#40;SSAS - multidimensional&#41;](../../analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional.md)|Explica cómo configurar opciones en el cuadro de diálogo información de suplantación.|  
  
## <a name="see-also"></a>Vea también  
 [Objetos de base de datos &#40;Analysis Services - Datos multidimensionales&#41;](../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)   
 [Arquitectura lógica &#40;Analysis Services - Datos multidimensionales&#41;](../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [Vistas del origen de datos en modelos multidimensionales](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [Orígenes de datos y enlaces &#40; SSAS Multidimensional &#41;](../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)  
  
  
