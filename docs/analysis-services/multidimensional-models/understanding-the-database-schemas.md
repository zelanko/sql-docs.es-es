---
title: Descripción de los esquemas de base de datos | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 91a54be06727a674a16f12295fa886f869b188e4
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="understanding-the-database-schemas"></a>Descripción de esquemas de base de datos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  El Asistente para generar esquemas genera un esquema relacional sin normalizar para la base de datos del área de asunto basado en las dimensiones y grupos de medida de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. El asistente genera una tabla relacional por dimensión para almacenar los datos de dimensión que se denomina tabla de dimensión y una tabla relacional por grupo de medida para almacenar los datos de hechos que se denomina tabla de hechos. Al generar las tablas relacionales, el asistente omite las dimensiones vinculadas, los grupos de medida vinculados y las dimensiones de tiempo de servidor.  
  
## <a name="validation"></a>Validación  
 Antes de comenzar a generar el esquema relacional subyacente, el Asistente para generar esquemas valida los cubos y dimensiones de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Si el asistente detecta errores, se interrumpe e informa de los errores en la ventana Lista de tareas de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Entre los ejemplos de errores que evitan la generación se incluyen los siguientes:  
  
-   Dimensiones que tienen más de un atributo clave  
  
-   Atributos primarios que tienen tipos de datos distintos de los atributos clave  
  
-   Grupos de medida que no tienen medidas  
  
-   Dimensiones o medidas degeneradas configuradas incorrectamente  
  
-   Claves suplentes configuradas incorrectamente, como varios atributos que utilizan el tipo de atributo **ScdOriginalID** o un atributo que utiliza **ScdOriginalID** sin estar enlazado a una columna que utiliza el tipo de datos entero.  
  
## <a name="dimension-tables"></a>Tablas de dimensión  
 En cada dimensión, el Asistente para generar esquemas genera una tabla de dimensión que debe incluirse en la base de datos del área de asunto. La estructura de una tabla de dimensión depende de las selecciones realizadas al diseñar la dimensión en la que se basa.  
  
 Columnas  
 El asistente genera una columna para los enlaces asociados a cada atributo de la dimensión en la que se basa la tabla de dimensiones, como los enlaces para las propiedades **KeyColumns**, **NameColumn**, **ValueColumn**, **CustomRollupColumn**, **CustomRollupPropertiesColumn**y **UnaryOperatorColumn** de cada atributo.  
  
 Relaciones  
 El asistente genera una relación entre la columna de cada atributo primario y la clave principal de la tabla de dimensión.  
  
 El asistente también genera una relación con la clave principal en cada tabla de dimensión adicional definida como una dimensión a la que se hace referencia en el cubo, si procede.  
  
 Restricciones  
 El asistente genera de manera predeterminada una restricción de clave principal por tabla de dimensión basada en el atributo clave de la dimensión. Si se genera una restricción de clave principal, se genera de forma predeterminada una columna de nombres independiente. Se creará una clave principal lógica en la vista del origen de datos aunque no cree la clave principal en la base de datos.  
  
> [!NOTE]  
>  Se producirá un error si se especifica más de un atributo clave en la dimensión en la que se basa la tabla de dimensión.  
  
 Traducciones  
 El asistente genera una tabla independiente para contener los valores traducidos de los atributos que requieran una columna de traducción. El asistente también crea una columna independiente para cada idioma necesario.  
  
## <a name="fact-tables"></a>Tablas de hechos  
 En cada grupo de medida de un cubo, el Asistente para generar esquemas genera una tabla de hechos que debe incluirse en la base de datos del área de asunto. La estructura de la tabla de hechos depende de las selecciones realizadas al diseñar el grupo de medida en el que se basa y las relaciones establecidas entre el grupo de medida y las dimensiones incluidas.  
  
 Columnas  
 El asistente genera una columna por medida, excepto para las medidas que usan la función de agregación **Count** . Dichas medidas no precisan una columna correspondiente en la tabla de hechos.  
  
 El asistente también genera una columna para cada columna de atributo de granularidad de cada relación de dimensión normal en el grupo de medida y una o más columnas para los enlaces asociados a cada atributo de una dimensión que tiene una relación de dimensión de hechos con el grupo de medida en el que se basa la tabla, si procede.  
  
 Relaciones  
 El asistente genera una relación por relación de dimensión normal de la tabla de hechos con el atributo de granularidad de la tabla de dimensión. Si la granularidad se basa en el atributo clave de la tabla de dimensión, la relación se crea en la base de datos y en la vista del origen de datos. Si la granularidad se basa en otro atributo, la relación solo se crea en la vista del origen de datos.  
  
 Si decide generar índices en el asistente, se generará un índice no clúster para cada una de las columnas de la relación.  
  
 Restricciones  
 Las claves principales no se generan en las tablas de hechos.  
  
 Si decide reforzar la integridad referencial, se generan restricciones de integridad referencial entre las tablas de dimensión y las tablas de hechos en los casos necesarios.  
  
 Traducciones  
 El asistente genera una tabla independiente para contener los valores traducidos de las propiedades en el grupo de medida que requieran una columna de traducción. El asistente también crea una columna independiente para cada idioma necesario.  
  
## <a name="data-type-conversion-and-default-lengths"></a>Conversión de tipo de datos y longitudes predeterminadas  
 El Asistente para generar esquemas omite los tipos de datos en todos los casos, excepto para las columnas que usan el tipo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **wchar** data type. El tamaño de datos **wchar** traduce directamente al tipo de datos **nvarchar** . Sin embargo, si la longitud especificada de una columna que utiliza el tamaño **wchar** es superior a 4.000 bytes, el Asistente para generar esquemas registrará un error.  
  
 Si un elemento de datos, como el enlace de un atributo, no posee una longitud especificada, se utilizará en la columna la longitud predeterminada que se muestra en la siguiente tabla.  
  
|Elemento de datos|Longitud predeterminada (bytes)|  
|---------------|------------------------------|  
|KeyColumn|50|  
|NameColumn|50|  
|CustomRollupColumn|3000|  
|CustomRollupPropertiesColumn|500|  
|UnaryOperatorColumn|1|  
  
## <a name="see-also"></a>Vea también  
 [Descripción de la generación Incremental](../../analysis-services/multidimensional-models/understanding-incremental-generation.md)   
 [Administrar los cambios en las vistas del origen de datos y orígenes de datos](../../analysis-services/multidimensional-models/manage-changes-to-data-source-views-and-data-sources.md)  
  
  
