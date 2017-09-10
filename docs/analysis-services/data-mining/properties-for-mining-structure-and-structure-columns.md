---
title: "Propiedades de la estructura de minería de datos y columnas de la estructura | Documentos de Microsoft"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mining structures [Analysis Services], column properties
- data mining [Analysis Services], properties
- columns [data mining], properties
- properties [data mining]
ms.assetid: ce90f684-bb8c-4eca-b9e6-000794dbee16
caps.latest.revision: 23
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4b342f6466a757ce2705d97680ed0e0460c0031f
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="properties-for-mining-structure-and-structure-columns"></a>Propiedades de estructuras de minería de datos y columnas de estructuras
  Puede establecer o cambiar las propiedades de una estructura de minería de datos, y de sus columnas y tablas anidadas asociadas, mediante la pestaña **Estructura de minería de datos** del Diseñador de minería de datos. Las propiedades que se configuran en esta pestaña se propagan a todos los modelos de minería de datos asociados con la estructura.  
  
> [!NOTE]  
>  Si cambia el valor de cualquier propiedad de la estructura de minería de datos, incluso los metadatos como un nombre o una descripción, es necesario volver a procesar la estructura de minería de datos y sus modelos para ver o consultar el modelo.  
  
## <a name="properties-of-mining-structures-and-mining-structure-columns"></a>Propiedades de estructuras de minería de datos y columnas de estructura de minería de datos  
 La tabla siguiente describe las propiedades para la estructura de minería de datos y las columnas de estructura de minería de datos específicas de la minería de datos, y que puede ver o configurar en la pestaña **Estructura de minería de datos** . Para ver o configurar estas propiedades, haga clic con el botón derecho en un elemento de la vista de árbol y, después, haga clic en **Propiedades**.  
  
-   Para ver las propiedades de la estructura, haga clic en el título de la estructura de minería de datos.  
  
-   Para ver las propiedades de una columna o una tabla anidada, haga clic en el nombre de columna.  
  
### <a name="properties-of-the-mining-structure"></a>Propiedades de la estructura de minería de datos  
  
|Propiedad|Description|  
|--------------|-----------------|  
|**CacheMode**|Especifica si los casos utilizados en entrenamiento deberían almacenarse en memoria caché o descartarse una vez completado el entrenamiento. **Nota:**  Esta propiedad se debe establecer en **KeepTrainingCases** para habilitar la obtención de detalles y la exclusión.|  
|**Intercalación**|Especifica la intercalación predeterminada de columna. Si no se especifica ninguna intercalación, se usa la del servidor.|  
|**Description**|Describe la estructura de minería de datos. Como práctica recomendada, la descripción debería indicar el propósito y la composición de los datos de la estructura.|  
|**ErrorConfiguration (valor predeterminado)**|Especifica las opciones para el control especial de errores, de existir alguno.|  
|**HoldoutMaxCases**|Especifica el número máximo de casos de estructura que se pueden reservar como un conjunto de datos de prueba.  Si se especifican valores tanto para **HoldoutMaxCases** como para **HoldoutPercent**, se combinan las condiciones. **Nota:**  Para establecer esta propiedad, <xref:Microsoft.AnalysisServices.MiningStructure.CacheMode%2A> debe establecerse en **KeepTrainingCases**.|  
|**HoldoutPercent**|Especifica el porcentaje de los casos de estructura para reservar como un conjunto de datos de prueba. Si se especifican valores tanto para **HoldoutMaxCases** como para **HoldoutPercent**, se combinan las condiciones. **Nota:**  Para establecer esta propiedad, <xref:Microsoft.AnalysisServices.MiningStructure.CacheMode%2A> debe establecerse en **KeepTrainingCases**.|  
|**HoldoutSeed**|Especifica un valor de inicialización para inicializar la creación de particiones del conjunto de prueba de exclusión, para asegurarse de que se puede volver a crear el conjunto de datos de prueba. **Nota:**  Para establecer esta propiedad, <xref:Microsoft.AnalysisServices.MiningStructure.CacheMode%2A> debe establecerse en **KeepTrainingCases**.|  
|**ID**|Muestra el identificador único de la estructura de minería de datos.<br /><br /> El nombre que asignó a la estructura de minería de datos cuando creó la estructura se usa como Id. Si cambia posteriormente el nombre escribiendo un nuevo valor para la propiedad **Name** , el nuevo nombre solamente se usa como un alias; el Id. no cambia.|  
|**Lenguaje**|Especifica el idioma para los títulos de la estructura de minería de datos.|  
|**Name**|Especifica el nombre o el alias de la estructura de minería de datos.<br /><br /> Si cambia el valor para la propiedad Name,el nuevo nombre se usa solo como un título o alias; el identificador para la estructura de minería de datos no cambia.|  
|**Source**|Muestra el nombre del origen de datos y el tipo de origen de datos.|  
  
### <a name="properties-of-the-mining-structure-columns"></a>Propiedades de las columnas de la estructura de minería de datos.  
  
|Propiedad|Description|  
|--------------|-----------------|  
|**ClassifiedColumns**|Identifica la columna que describe una columna clasificada.|  
|**Contenido**|El tipo de contenido de la columna.|  
|**Description**|Describe la columna. Como práctica recomendada, la descripción de la columna debería proporcionar información sobre cómo se han obtenido los datos de la columna o se han modificado para la minería de datos.|  
|**DiscretizationBucketCount**|Muestra el número de cubos de la columna de datos discretos.<br /><br /> Se habilita solo si el tipo de contenido se establece en **Discretized**.<br /><br /> Esta propiedad es de solo lectura.|  
|**DiscretizationMethod**|Muestra el método usado para discretizar la columna.<br /><br /> Se habilita solo si el tipo de contenido se establece en **Discretized**.<br /><br /> Esta propiedad es de solo lectura.|  
|**Distribución**|Especifica la distribución del contenido de la columna.|  
|**ID**|Muestra el identificador de la columna.<br /><br /> Si cambia el valor de la propiedad Name de la columna, no afecta al valor de la propiedad ID.|  
|**IsKey**|Indica si la columna es una columna de clave.|  
|**KeyColumns**|Contiene la definición de una columna que es la clave o parte de la clave de un atributo.|  
|**ModelingFlags**|Establece parámetros adicionales que el algoritmo establece como disponibles.|  
|**Name**|Nombre de la columna.|  
|**NameColumn**|Identifica la columna que proporciona el nombre del elemento primario.|  
|**Source**|Muestra el origen de la columna.<br /><br /> Para los orígenes de datos no relacionales, el valor siempre es **(ninguno)**.<br /><br /> Para las estructuras que se basan en un cubo OLAP, el valor es la instrucción MDX que define el segmento que se usa como origen para la tabla anidada.|  
|**SourceMeasureGroup**|Muestra el origen del grupo de medida.<br /><br /> Para los orígenes de datos no relacionales, el valor siempre es **(ninguno)**.<br /><br /> Para las estructuras que se basan en un cubo OLAP, el valor es la instrucción MDX que define el segmento que se usa como origen para la tabla anidada.|  
|**Tipo**|El tipo de datos del contenido de la columna.|  
  
 Para obtener más información sobre cómo establecer o modificar las propiedades, vea [Tareas y procedimientos de las estructuras de minería de datos](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md).  
  
## <a name="see-also"></a>Vea también  
 [Crear una estructura de minería de datos relacional](../../analysis-services/data-mining/create-a-relational-mining-structure.md)   
 [Columnas de la estructura de minería de datos](../../analysis-services/data-mining/mining-structure-columns.md)  
  
  
