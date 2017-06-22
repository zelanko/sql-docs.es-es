---
title: "Configuración de filtro (Explorador de objetos y Explorador de Utilidad) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.common.filtersettings.f1
- sql13.ag.job.filtersettings.f1
ms.assetid: 4aab04bc-e1ab-4d4b-ab74-b287fc805bc2
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 68c03b5f5fd4fc9a4ca371331309e971dcc540c0
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="filter-settings-object-explorer-and-utility-explorer"></a>Configuración de filtro (Explorador de objetos y Explorador de la utilidad)
Utilice este cuadro de diálogo para especificar un filtro. Un filtro permite configurar el Explorador de objetos y el Explorador de la utilidad para mostrar únicamente los elementos que cumplen criterios específicos. Por ejemplo, puede utilizar un filtro para mostrar solo los trabajos con nombres que contienen la palabra "Mantenimiento". El encabezado del cuadro de diálogo **Configuración del filtro** contiene el nombre del servidor y puede contener el nombre de la base de datos.  
  
## <a name="uielement-list"></a>Lista de UIElement  
**Propiedad**  
Muestra la propiedad que se va filtrar.  
  
**Operador**  
Seleccione la forma en que el filtro va a aplicar el valor a la propiedad. Existen las siguientes opciones:  
  
-   **Es igual a**  
  
    El filtro muestra los elementos en los que la propiedad y el valor coinciden plenamente.  
  
-   **Contiene**  
  
    El filtro muestra los elementos en los que la propiedad contiene el valor. La propiedad puede contener otro texto.  
  
-   **No contiene**  
  
    El filtro muestra los elementos en los que la propiedad no contiene el valor.  
  
-   **Menor que**  
  
    Disponible para fechas; este filtro muestra los elementos cuya fecha es anterior al valor proporcionado.  
  
-   **Menor que o igual a**  
  
    Disponible para fechas; este filtro muestra los elementos cuya fecha es igual o anterior al valor proporcionado.  
  
-   **Mayor que**  
  
    Disponible para fechas; este filtro muestra los elementos cuya fecha es posterior al valor proporcionado.  
  
-   **Mayor que o igual a**  
  
    Disponible para fechas; este filtro muestra los elementos cuya fecha es igual o posterior al valor proporcionado.  
  
-   **Entre**  
  
    Disponible para fechas; este filtro muestra los elementos cuya fecha se encuentra entre dos fechas proporcionadas. Seleccione **Entre** y presione la tecla TAB para agregar otra fila a fin de escribir la segunda fecha.  
  
-   **No entre**  
  
    Disponible para fechas; este filtro muestra los elementos cuya fecha es anterior o posterior a dos fechas proporcionadas. Seleccione **No entre** y salga de la columna **Operador** para agregar otra fila a fin de escribir la segunda fecha.  
  
**Value**  
Escriba el valor que va a compararse con la propiedad. Para seleccionar una fecha, haga clic en la flecha abajo para que aparezca un calendario donde seleccionarla.  
  
**Borrar filtro**  
Elimina toda la configuración actual del filtro.  
  
## <a name="see-also"></a>Vea también  
[Usar SQL Server Management Studio](../../ssms/use-sql-server-management-studio.md)  
[Información general de la Utilidad de SQL Server](http://msdn.microsoft.com/en-us/6e6cbd25-6b1c-4e21-9ade-4584e243fd8f)  
  

