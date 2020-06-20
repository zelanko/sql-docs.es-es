---
title: Seleccionar tablas y vistas (Asistente para vistas del origen de datos) (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.datasourceviewwizard.selecttablesandviews.f1
ms.assetid: ea7d1232-f213-46e9-90d9-0fd616ca003d
author: minewiskan
ms.author: owend
ms.openlocfilehash: 6b1b878935ffc0dee51c112581a130dde99043e2
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940816"
---
# <a name="select-tables-and-views-data-source-view-wizard-analysis-services"></a>Seleccionar las tablas y vistas (Asistente para vistas del origen de datos) (Analysis Services)
  Utilice la página **Seleccionar tablas y vistas** para seleccionar las tablas o las vistas del origen de datos que desea incluir en la vista del origen de datos.  
  
## <a name="options"></a>Opciones  
 **Available objects**  
 Enumera las tablas y vistas del esquema del origen de datos. Si se enumera más de un objeto, el nombre del esquema utiliza un prefijo en el nombre de cada objeto. Si solo se enumera uno, el nombre del esquema no utiliza ningún prefijo en los nombres de objeto.  
  
 Para ordenar la lista en sentido ascendente o descendente, haga clic en **Nombre** o **Tipo**.  
  
 **Included objects**  
 Enumera las tablas y vistas que deben incluirse en la vista del origen de datos.  
  
 Para ordenar la lista en sentido ascendente o descendente, haga clic en **Nombre** o **Tipo**.  
  
 **Filter**  
 Filtra los objetos que se indican en **Objetos disponibles**. Escriba una cadena y haga clic en **Filtro** para obtener una lista de los elementos que contienen la cadena especificada. Para buscar una cadena exacta de caracteres, especifique la cadena entre comillas dobles. El filtro no distingue entre mayúsculas y minúsculas.  
  
 En cualquier punto de la cadena del filtro puede incluir los caracteres comodín que se indican en la tabla siguiente.  
  
|Carácter comodín|Value|  
|------------------------|-----------|  
|**\***|Cualquier cadena de caracteres|  
|**%**|Cualquier cadena de caracteres|  
|**?**|Un único carácter|  
|**"** *cadena* **"**|Cadena literal de caracteres. Este carácter comodín establecerá una correspondencia con cualquier subcadena del nombre de objeto.|  
  
 **Show system objects**  
 Muestra los objetos del sistema en **Objetos disponibles**. Esta opción solo está disponible si el proveedor del origen de datos expone objetos del sistema. Esta opción se selecciona automáticamente al eliminar un objeto del sistema de la lista **Objetos incluidos** .  
  
 **Add related tables**  
 Agrega todas las tablas que están relacionadas con las indicadas en **Objetos incluidos**. Esta opción no agrega vistas. No obstante, sí agrega tablas con particiones. Si selecciona criterios de coincidencia de nombres en la página **Coincidencia de nombres** del asistente, esta opción también incluye tablas relacionadas lógicamente de acuerdo con los criterios seleccionados. Las tablas también se incluyen si están relacionadas con las tablas relacionadas que se acaban de agregar, y si su estructura es idéntica a la de la tabla original.  
  
## <a name="see-also"></a>Consulte también  
 [Asistente para vistas del origen de datos &#40;de ayuda F1 Analysis Services&#41;](data-source-view-wizard-f1-help-analysis-services.md)   
 [Vistas del origen de datos en modelos multidimensionales](multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
