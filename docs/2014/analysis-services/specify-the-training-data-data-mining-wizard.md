---
title: Especificar los datos de entrenamiento (Asistente para minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.dmwizard.specifytrainingdata.f1
ms.assetid: cb04deeb-0f89-4bba-b3f1-efccada16825
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c3bbeb708cdb0c2882b85d55081446b3dc12b56b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66068064"
---
# <a name="specify-the-training-data-data-mining-wizard"></a>Especificar los datos de entrenamiento (Asistente para minería de datos)
  Utilice la página **Especificar los datos de aprendizaje** para identificar las columnas que se van a incluir en la estructura de minería de datos. Puede seleccionar columnas para que se incluyan en la estructura aunque no las utilice en todos los modelos. Por ejemplo, si desea obtener detalles de las columnas del modelo de minería, puede incluirlas en la estructura pero no en el modelo.  
  
 Se requiere al lo menos una columna de clave para cada tabla que está incluida en la estructura. La columna elegida como clave depende de que la tabla sea una tabla de casos o una tabla anidada. Si la tabla es una tabla anidada, la clave es a menudo también la columna de predicción, no la clave externa relacional. Para más información sobre las claves anidadas, vea [Tablas anidadas &#40;Analysis Services - Minería de datos&#41;](data-mining/nested-tables-analysis-services-data-mining.md).  
  
> [!NOTE]  
>  Los diferentes algoritmos de minería utilizan las claves de forma diferente. Para más información sobre los diferentes tipos de claves, vea [Tipos de contenido &#40;minería de datos&#41;](data-mining/content-types-data-mining.md).  
  
 **Para más información:** [Estructuras de minería de datos &#40;Analysis Services - Minería de datos&#41;](data-mining/mining-structures-analysis-services-data-mining.md), [Columnas del modelo de minería de datos](data-mining/mining-model-columns.md), [Asistente para minería de datos &#40;Analysis Services - Minería de datos&#41;](data-mining/data-mining-wizard-analysis-services-data-mining.md), [Crear una estructura de minería de datos relacional](data-mining/create-a-relational-mining-structure.md)  
  
## <a name="options"></a>Opciones  
 **Tablas y columnas**  
 Muestra las tablas y columnas seleccionadas en la página anterior del asistente.  
  
 **\<>casilla**  
 Seleccione las columnas que desea incluir en la estructura de minería de datos.  
  
 Si su origen de datos incluye tablas anidadas o vistas múltiples, expanda la lista de columnas para ver las tablas anidadas.  
  
 **Clave**  
 Seleccione esta opción para utilizar la columna como un identificador único para los datos.  
  
 Para una tabla de casos, la clave es normalmente el identificador único.  
  
 Para la tabla anidada, la **Clave** indica el identificador de una fila en el contexto del caso asociado.  
  
 **Entrada**  
 Seleccione esta opción para utilizar la columna para crear predicciones.  
  
> [!NOTE]  
>  Esta columna solo está disponible cuando se crea un modelo de minería junto con la estructura de minería de datos.  
  
 **Predicción**  
 Seleccione esta opción para permitir que la tabla o la columna se puedan predecir a partir de una entrada futura adicional.  
  
 Si también marca una tabla anidada como de predicción, la tabla anidada completa se convierte en una tabla de predicción. Si ninguna columna de la tabla anidada está marcada como de entrada o predicción, la tabla anidada aparecerá en la estructura de minería de datos, pero se omitirá en el modelo.  
  
 **Nota** : esta columna solo está disponible cuando se crea un modelo de minería junto con la estructura de minería de datos.  
  
 **Propone**  
 Haga clic para abrir el cuadro de diálogo **Sugerir columnas relacionadas** , que realiza un análisis de una muestra de datos para identificar las columnas de entrada más relacionadas con la columna **Predicción** seleccionada según la entropía. Este análisis también se aplica a las columnas de la tabla anidada o a las estructuras de minería basadas en orígenes OLAP.  
  
 **Nota** : esta columna solo está disponible cuando se crea un modelo de minería junto con la estructura de minería de datos.  
  
## <a name="see-also"></a>Consulte también  
 [Asistente para minería de datos (ayuda F1) &#40;Analysis Services: minería de datos&#41;](data-mining-wizard-f1-help-analysis-services-data-mining.md)   
 [Sugerir columnas relacionadas &#40;Asistente para minería de datos&#41;](suggest-related-columns-data-mining-wizard.md)   
 [Especificar tipos de tablas &#40;Asistente para minería de datos&#41;](specify-table-types-data-mining-wizard.md)   
 [Especifique el contenido y el tipo de datos de la columna &#40;Asistente para minería de datos&#41;](specify-the-column-s-content-and-data-type-data-mining-wizard.md)  
  
  
