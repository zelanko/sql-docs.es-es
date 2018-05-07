---
title: Tablas y columnas | Documentos de Microsoft
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c428d717-05de-436c-b9dc-e8c1925a60ca
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 927eafada0d5f4905e24ec90d5594859bc2210f6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="tables-and-columns"></a>Tablas y columnas 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Después de haber agregado tablas y datos a un modelo mediante el Asistente para la importación de tablas, puede empezar a trabajar con las tablas agregando nuevas columnas de datos, creando relaciones entre las tablas, definiendo cálculos que amplían los datos y filtrando y ordenando datos en las tablas para facilitar su visualización.  
  
 Secciones de este tema:  
  
-   [Ventajas](#bkmk_benefits)  
  
-   [Trabajar con tablas y columnas](#bkmk_working)  
  
-   [Tareas relacionadas](#bkmk_related_tasks)  
  
##  <a name="bkmk_benefits"></a> Ventajas  
 En los modelos tabulares, las tablas proporcionan el marco en el que se definen las columnas y otros metadatos. Las tablas incluyen:  
  
 **Definición de tabla**  
 La definición de tabla incluye el conjunto de columnas. Las columnas se pueden importar desde un origen de datos o agregar manualmente, como en el caso de las columnas calculadas.  
  
 **Metadatos de la tabla**  
 Las relaciones, las medidas, los roles, las perspectivas y los datos pegados son los metadatos que definen los objetos en el contexto de una tabla.  
  
 **Datos**  
 Los datos se rellenan en las columnas de las tablas la primera vez que se importan las tablas usando el Asistente para la importación de tablas o creando nuevos datos en columnas calculadas. Cuando los datos cambian en el origen, o cuando se quita un modelo de la memoria, es necesario ejecutar una operación de proceso para volver a rellenar los datos en las tablas.  
  
##  <a name="bkmk_working"></a> Trabajar con tablas y columnas  
 No se pueden crear tablas de modelos directamente en el diseñador de modelos. Se crea automáticamente una pestaña nueva cada vez que se importan o copian datos de otro origen de datos. Cada pestaña (en el diseñador de modelos) contiene una tabla de datos, que puede incluir lo siguiente:  
  
-   Una tabla o vista única de una base de datos relacional, o de otros orígenes no relacionales, como un cubo de Analysis Services.  
  
-   Un conjunto tabular de datos importado de una fuente o archivo de texto.  
  
-   Una combinación de datos relacionales y de datos tabulares (HTML) copiados y pegados en la tabla.  
  
 Al importar datos, cada tabla o vista, hoja o archivo de datos se agrega como una tabla en el diseñador de modelos. Normalmente, los datos de varios orígenes se agregan en pestañas independientes, pero puede combinar datos en una única tabla usando **Pegar** y **Pegar y anexar**. Para obtener más información, consulte [copiar y pegar datos](../../analysis-services/tabular-models/ssas-import-data-copy-and-paste-data.md).  
  
 Después de agregar los datos que necesita, puede crear relaciones adicionales entre las tablas, buscar o hacer referencia a los valores relacionados en otras tablas, o crear valores derivados agregando nuevas columnas calculadas.  
  
 Si trabaja con conjuntos de datos muy grandes, es posible que necesite filtrar determinados datos para que no sean visibles. Puede que también desee ordenar los datos en un orden diferente. El diseñador de modelos le permite usar las características de filtrado, ordenación y ocultación para mostrar, o no mostrar, columnas completas o determinados datos.  
  
##  <a name="bkmk_related_tasks"></a> Tareas relacionadas  
  
|Tema|Description|  
|-----------|-----------------|  
|[Agregar columnas a una tabla](../../analysis-services/tabular-models/add-columns-to-a-table-ssas-tabular.md)|Describe cómo agregar una columna de origen a una definición de tabla.|  
|[Eliminar una columna](../../analysis-services/tabular-models/delete-a-column-ssas-tabular.md)|Describe cómo eliminar una columna de la tabla modelo mediante el diseñador de modelos o mediante el cuadro de diálogo Propiedades de la tabla.|  
|[Cambiar las asignaciones de filtros de tabla, columna o fila](../../analysis-services/tabular-models/change-table-column-or-row-filter-mappings-ssas-tabular.md)|Describe cómo cambiar las asignaciones de filtros de tabla, columna o fila mediante la vista previa de tabla o el Editor de consultas de SQL en el cuadro de diálogo Editar propiedades de tabla.|  
|[Especificar Marcar como tabla de fechas con inteligencia de tiempo](../../analysis-services/tabular-models/specify-mark-as-date-table-for-use-with-time-intelligence-ssas-tabular.md)|Describe cómo se usa el cuadro de diálogo Marcar como tabla de fechas para especificar una tabla de fechas y una columna de identificador único. Es necesario especificar una tabla de fechas y un identificador único de fecha cuando se utilizan funciones de inteligencia de tiempo en fórmulas DAX.|  
|[Agregar una tabla](../../analysis-services/tabular-models/add-a-table-ssas-tabular.md)|Describe cómo se agrega una tabla desde un origen de datos utilizando una conexión de origen de datos existente.|  
|[Eliminar una tabla](../../analysis-services/tabular-models/delete-a-table-ssas-tabular.md)|Describe cómo eliminar tablas que ya no necesita de la base de datos del área de trabajo del modelo.|  
|[Cambiar el nombre de una tabla o una columna](../../analysis-services/tabular-models/rename-a-table-or-column-ssas-tabular.md)|Describe cómo cambiar el nombre de una tabla o una columna para que sea más identificable en el modelo.|  
|[Establecer el tipo de datos de una columna](../../analysis-services/tabular-models/set-the-data-type-of-a-column-ssas-tabular.md)|Describe cómo modificar el tipo de datos de una columna. El tipo de datos define cómo se almacenan y presentan los datos de la columna.|  
|[Ocultar o inmovilizar columnas](../../analysis-services/tabular-models/hide-or-freeze-columns-ssas-tabular.md)|Describe cómo ocultar columnas que no desea mostrar y cómo mantener visible un área de un modelo mientras se desplaza a otra área del modelo inmovilizando (bloqueando) columnas específicas en un área.|  
|[Columnas calculadas](../../analysis-services/tabular-models/ssas-calculated-columns.md)|En los temas de esta sección se describe cómo usar las columnas calculadas para incorporar datos agregados al modelo.|  
|[Filtrar y ordenar datos](http://msdn.microsoft.com/library/55ebd7a6-2458-4398-911f-fcfeb2413f1b)|En los temas de esta sección se describe cómo filtrar u ordenar los datos usando los controles del diseñador de modelos.|  
  
  
