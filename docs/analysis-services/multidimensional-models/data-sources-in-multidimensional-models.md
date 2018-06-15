---
title: Orígenes de datos en modelos multidimensionales | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 149ac1e36eb07d40223ffc97fba1646932ab0093
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34022832"
---
# <a name="data-sources-in-multidimensional-models"></a>Orígenes de datos en modelos multidimensionales
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
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
|[Crear un origen de datos & #40; SSAS Multidimensional & #41;](../../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md)|Explica cómo agregar un objeto de origen de datos a un modelo multidimensional.|  
|[Eliminar un origen de datos en el Explorador de soluciones & #40; SSAS Multidimensional & #41;](../../analysis-services/multidimensional-models/delete-a-data-source-in-solution-explorer-ssas-multidimensional.md)|Use este procedimiento para eliminar un objeto de origen de datos de un modelo multidimensional.|  
|[Establecer propiedades del origen de datos & #40; SSAS Multidimensional & #41;](../../analysis-services/multidimensional-models/set-data-source-properties-ssas-multidimensional.md)|Describe cada propiedad y explica cómo configurar cada una.|  
|[Establecer opciones de suplantación & #40; SSAS - Multidimensional & #41;](../../analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional.md)|Explica cómo configurar opciones en el cuadro de diálogo información de suplantación.|  
  
## <a name="see-also"></a>Vea también  
 [Objetos de base de datos & #40; Analysis Services - datos multidimensionales & #41;](../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)   
 [Arquitectura lógica & #40; Analysis Services - datos multidimensionales & #41;](../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [Vistas del origen de datos en modelos multidimensionales](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [Orígenes de datos y enlaces & #40; SSAS Multidimensional & #41;](../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)  
  
  
