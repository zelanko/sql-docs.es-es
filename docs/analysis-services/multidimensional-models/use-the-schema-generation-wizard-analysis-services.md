---
title: "Usar el Asistente para generación de esquemas (Analysis Services) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Schema Generation Wizard, steps
- relational schema [Analysis Services], Schema Generation Wizard
ms.assetid: 8c710745-d41d-4c31-b6a2-2956229df75a
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d8cae9fd297d0ae2946cccab69a9a273a2cf85b4
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="use-the-schema-generation-wizard-analysis-services"></a>Usar el Asistente para generar esquemas (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]El Asistente para generar esquemas requiere una cantidad limitada de información durante la fase de generación. La mayoría de la información que el Asistente para generar esquemas requiere para generar esquemas relacionales se extrae de los cubos y las dimensiones de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que se han creado previamente en el proyecto. Además, puede personalizar el modo en que se genera el esquema de la base de datos del área de asunto y cómo se asignan nombres a los objetos del esquema.  
  
## <a name="start-the-wizard"></a>Iniciar el asistente  
 Puede abrir el Asistente para generar esquemas desde [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] de varias formas:  
  
-   Haga clic con el botón derecho en el objeto de proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y, después, haga clic en **Generar esquema relacional** en el menú contextual.  
  
-   Haga clic en el objeto de proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y, a continuación, en **Generar esquema relacional** en el menú **Base de datos** .  
  
-   Inicie el asistente desde el Asistente para dimensiones haciendo clic en la casilla **Generar el esquema ahora** en la última página del asistente.  
  
## <a name="step-1-specify-targets"></a>Paso 1: especificar los destinos  
 Debe especificar la vista del origen de datos (DSV) en que desea que el Asistente para generar esquemas genere el esquema para la base de datos del área de asunto. Aunque puede seleccionar una DSV existente, lo habitual es crear una nueva basada en un origen de datos. El origen de datos se puede crear en función de una conexión nueva o una existente, o bien basándose en otro objeto. El Asistente para generar esquemas crea el esquema para la base de datos del área de asunto en la base de datos a la que se hace referencia en el origen de datos, así como en la vista del origen de datos. El Asistente para generar esquemas no crea la propia base de datos del área de asunto; lo que hace es crear el esquema relacional para que los cubos y las dimensiones sean compatibles con la base de datos existente que se especifique.  
  
 Cuando el Asistente para generar esquemas crea los objetos subyacentes, enlaza las dimensiones y los cubos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a las tablas y las columnas generadas mediante enlaces con estilo de vista del origen de datos.  
  
> [!NOTE]  
>  Para cancelar el enlace entre las dimensiones y los cubos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de los objetos generados previamente, elimine la vista del origen de datos a la que están enlazados los cubos y las dimensiones de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y, a continuación, defina una nueva vista del origen de datos para los cubos y las dimensiones mediante el Asistente para generar esquemas.  
  
## <a name="step-3-specify-schema-options-for-the-subject-area-database"></a>Paso 3: especificar opciones de esquema para la base de datos del área de asunto  
 El Asistente para generar esquemas proporciona una serie de opciones para definir el esquema que se genera para la base de datos del área de asunto. Estas opciones se pueden especificar en la página **Opciones de esquema de la base de datos del área de asunto** del asistente.  
  
### <a name="specifying-the-schema-owner"></a>Especificar el propietario del esquema  
 Para especificar el propietario del esquema, establezca el valor de **Esquema de propiedad** en una cadena válida. El propietario predeterminado del esquema es el proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , pero puede especificar el propietario que desee.  
  
### <a name="specifying-primary-keys-indexes-and-constraints"></a>Especificar claves principales, índices y restricciones  
 El Asistente para generar esquemas crea de forma predeterminada una restricción de clave principal en cada tabla de dimensiones de la base de datos del área de asunto. La clave principal corresponde al atributo que se designa como atributo clave en la dimensión de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] correspondiente. Esta restricción mejora el rendimiento del procesamiento en la mayoría de entornos, con un costo mínimo. Las claves principales lógicas siempre se crean en la vista del origen de datos, incluso aunque se elija no crear la clave principal en la base de datos del área de asunto. Para definir restricciones de clave principal en tablas de dimensiones, seleccione **Crear claves principales en tablas de dimensiones**.  
  
 De forma predeterminada, el asistente también crea índices en las columnas de clave externa de cada tabla de hechos. Estos índices mejoran el rendimiento del procesamiento en la mayoría de entornos. El rendimiento mejora habitualmente porque las consultas de procesamiento que genera [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para recuperar nuevos datos de la base de datos del área de asunto suelen incluir un número importante de instrucciones de combinación entre la tabla de hechos y las tablas de dimensiones. Para definir índices en las columnas de clave externa de cada tabla de hechos, seleccione **Crear índices**.  
  
 Por último, de forma predeterminada el asistente impone la integridad referencial entre la tabla de hechos y cada una de las tablas de dimensiones. Aunque decida no imponer la integridad referencial, el Asistente para generar esquemas creará estas relaciones en la base de datos y la vista del origen de datos. Para imponer la integridad referencial, seleccione **Exigir integridad referencial**.  
  
### <a name="preserving-data-for-incremental-generation"></a>Conservar datos para la generación incremental  
 De forma predeterminada, el Asistente para generar esquemas trata de conservar los datos cuando se vuelve a generar el esquema de una base de datos. Si el Asistente para generar esquemas tiene que eliminar alguna fila debido a un cambio en el esquema, se muestra una advertencia antes de hacerlo. Por ejemplo, es posible que haya que eliminar filas para resolver problemas de integridad referencial por haber quitado una dimensión o porque haya cambiado un tipo de datos al modificar un atributo de dimensión. Para conservar los datos cuando se vuelve a generar el esquema de la base de datos, seleccione **Mantener los datos al volver a generar**.  
  
## <a name="step-4-specify-naming-conventions"></a>Paso 4: especificar convenciones de nomenclatura  
 En la página **Especificar convenciones de nomenclatura** del Asistente para generar esquemas, puede definir las convenciones de nomenclatura que usará el asistente a la hora de crear ciertos objetos de la base de datos del área de asunto. Para obtener más información sobre las opciones disponibles en la página **Especificar convenciones de nomenclatura**, vea [Especificar convenciones de nomenclatura &#40;Asistente para generar esquemas&#41; &#40;Analysis Services - Datos multidimensionales&#41;](http://msdn.microsoft.com/library/02d830ea-5b1f-4485-9f94-d64b8bea592b).  
  
  
