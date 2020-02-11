---
title: Administrar un dominio | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: c5ab71a3-0dac-45b1-be8e-93bf7e0e03ce
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 93b5666bd2d57fb0a8ffae435818a02ba152217c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "65484127"
---
# <a name="managing-a-domain"></a>Administrar un dominio
  En este tema se describe el uso de los dominios en [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Un dominio contiene una representación semántica de los datos de un campo determinado del origen de datos que se va a analizar. Un dominio forma parte de la base de conocimiento creada para un origen de datos, y todo el conocimiento obtenido mediante el análisis de un origen de datos de ejemplo o la importación de datos se agrega a los dominios definidos en ella. El conocimiento de dichos dominios se utiliza posteriormente para realizar las tareas de limpieza y de búsqueda de coincidencias en un proyecto de calidad de datos. Los dominios son el núcleo de todas las actividades de Data Quality Services.  
  
 Un dominio se asigna a un campo del origen de datos, y se rellena en las actividades de detección de conocimiento, administración de dominios y búsqueda de coincidencias. La forma en la que se cargan los datos desde el origen de datos y se muestran en un informe se define en las propiedades del dominio. Si se utiliza un proveedor de datos de referencia para limpiar los datos, se debe adjuntar un servicio de datos de referencia a un dominio único o a uno compuesto. Puede crear reglas, así como relaciones basadas en términos, que se aplicarán a los datos del dominio. Puede ver y corregir los datos del dominio.  
  
 También puede crear un dominio compuesto formado por dos o más dominios individuales que contengan conocimiento sobre datos comunes. Para más información, vea [Administrar un dominio compuesto](../../2014/data-quality-services/managing-a-composite-domain.md).  
  
## <a name="domain-properties"></a>Propiedades del dominio  
 Al crear un dominio, tendrá las opciones siguientes para rellenarlo a partir de los datos de origen y mostrar los valores del dominio. Para más información, consulte [Conjunto propiedades de dominio](../../2014/data-quality-services/set-domain-properties.md).  
  
-   Seleccione el tipo de los datos con los que va a rellenar el dominio. Para obtener más información acerca de los tipos de datos admitidos para cada uno de los tipos de datos de dominio, vea [Compatibilidad con los tipos de datos en SQL Server y SSIS para dominios DQS](../../2014/data-quality-services/supported-sql-server-and-ssis-data-types-for-dqs-domains.md).  
  
-   Especifique que solo se mostrarán los valores iniciales del dominio, no sus sinónimos.  
  
-   Especifique que los valores de dominio se mostrarán en un formato determinado, dependiendo del tipo de datos.  
  
-   Si los datos son de tipo cadena, puede normalizar la cadena quitando los caracteres especiales al cargarla en el dominio desde el origen de datos.  
  
-   Si los datos son de tipo cadena, puede ejecutar el corrector ortográfico de DQS para comprobar la sintaxis, la ortografía y la estructura de las frases, e indicar los posibles errores en la página **Valores del dominio** de **Administración de dominios**. Esto incluye la especificación del idioma en el que se ejecutará el corrector ortográfico.  
  
-   Si los datos son de tipo cadena, puede especificar que DQS no identifique los errores de sintaxis cuando sepa que no existen errores de este tipo en las cadenas.  
  
## <a name="in-this-section"></a>En esta sección  
 El uso de un dominio le permite hacer lo siguiente:  
  
|||  
|-|-|  
|Crear una representación semántica de un campo de datos con un tipo de datos específico, especificar cómo se rellena el dominio y dar formato a los resultados del dominio|[Crear un dominio](../../2014/data-quality-services/create-a-domain.md)|  
|Vincular un dominio a otro, permitiéndole compartir los mismos valores y configuración|[Crear dominio vinculado](../../2014/data-quality-services/create-a-linked-domain.md)|  
|Adjuntar un servicio de datos de referencia a un dominio único o compuesto|[Adjuntar un dominio o un dominio compuesto a datos de referencia](../../2014/data-quality-services/attach-a-domain-or-composite-domain-to-reference-data.md)|  
|Cambiar o aumentar los valores de una base de conocimiento|[Cambiar valores de dominio](../../2014/data-quality-services/change-domain-values.md)|  
|Utilizar reglas de validación y normalización|[Cree una regla de dominio](../../2014/data-quality-services/create-a-domain-rule.md)|  
|Utilizar relaciones para corregir un término que forma parte de un valor de un dominio|[Crear relaciones basadas en términos](../../2014/data-quality-services/create-term-based-relations.md)|  
|Completar, cerrar o cancelar la actividad de administración de dominios|[Finalizar la actividad Administración de dominios](../../2014/data-quality-services/end-the-domain-management-activity.md)|  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Generar una base de conocimiento ejecutando la detección de conocimiento y administrando el conocimiento de forma interactiva|[Crear una base de conocimiento](../../2014/data-quality-services/building-a-knowledge-base.md)|  
|Importar conocimiento en una base de conocimiento o exportarlo desde esta.|[Importar y exportar conocimiento](../../2014/data-quality-services/importing-and-exporting-knowledge.md)|  
|Crear un dominio compuesto y agregarle conocimiento.|[Administrar un dominio compuesto](../../2014/data-quality-services/managing-a-composite-domain.md)|  
  
  
