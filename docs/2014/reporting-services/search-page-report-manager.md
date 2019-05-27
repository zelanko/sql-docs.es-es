---
title: Buscar página (Administrador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 51ffdc07-e1b9-4ed7-acb3-dd98d7cce273
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 12413c103230d8c085a9701e3fb83db15135895a
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66102262"
---
# <a name="search-page-report-manager"></a>Buscar (página del Administrador de informes)
  Use la página Resultados de la búsqueda para ver los resultados de una operación de búsqueda especificada para un informe, un informe vinculado, un modelo de informe, un origen de datos compartido, una carpeta o un recurso. Los resultados de la búsqueda se muestran ordenados alfabéticamente. Se pueden ordenar por tipo, nombre o descripción.  
  
 En una operación de búsqueda no se incluyen los elementos siguientes: instantáneas de informe incluidas en un historial de informes, suscripciones y programaciones compartidas. De manera similar, si no se tienen permisos suficientes para ver una carpeta o un informe, ese elemento se excluye de la búsqueda.  
  
 No puede buscar el texto dentro de un informe o modelo. Para buscar texto específico dentro de un informe, use la barra de herramientas situada en la parte superior del informe.  
  
## <a name="navigation"></a>Navegación  
 Utilice el procedimiento siguiente para navegar hasta esta ubicación en la interfaz de usuario (IU).  
  
###### <a name="to-open-the-search-results-page"></a>Para abrir la página Resultados de la búsqueda  
  
1.  Abra el Administrador de informes.  
  
2.  En la parte superior de la página, escriba sus criterios de búsqueda en el cuadro **Buscar** . A continuación, presione Entrar o haga clic en la flecha Buscar.  
  
## <a name="options"></a>Opciones  
 **Eliminar**  
 Haga clic para quitar un elemento de una base de datos del servidor de informes.  
  
> [!NOTE]  
>  Este botón solo está disponible en la vista **Detalles**. Sin embargo, puede mantener el mouse sobre un elemento y utilizar el menú para obtener acceso a la funcionalidad de eliminar en la vista **Detalles** o en la **Vista de lista**.  
  
 **Mover**  
 Haga clic para cambiar la ubicación de un elemento. Al hacerlo, se abre la página para mover elementos, en la que puede seleccionar una nueva ubicación de carpeta.  
  
> [!NOTE]  
>  Este botón solo está disponible en la vista **Detalles**. Sin embargo, puede desplazar el mouse sobre un elemento y utilizar el menú para obtener acceso a la funcionalidad de mover en la vista **Detalles** o en la **Vista de lista**.  
  
 Cuadro Buscar  
 Escriba la totalidad o parte del nombre de un elemento que desee ubicar y, a continuación, haga clic en **Ir** para iniciar la búsqueda. La longitud máxima de una cadena de búsqueda es 128 caracteres.  
  
 En los resultados de la búsqueda, se incluyen los nombres o las descripciones de los elementos que contengan la cadena de búsqueda completa en cualquier lugar del valor de texto.  
  
 No se admiten operadores booleanos, como el signo más (+).  
  
 **Vista de detalles**  
 Haga clic para mostrar la página Resultados de la búsqueda en una lista que contiene información adicional sobre los elementos, como el tipo de elemento, nombre, la descripción, la carpeta en la que se encuentra y la última vez que se ejecutó. En la vista **Detalles**puede utilizar los botones **Eliminar** y **Mover** para quitar y reubicar los elementos de una carpeta.  
  
 Mantenga el mouse sobre un elemento y haga clic en la flecha de lista desplegable para abrir el menú desplegable donde podrá obtener acceso a las propiedades del elemento seleccionado y configurarlas.  
  
 **Vista de lista**  
 Haga clic para mostrar la página Resultados de la búsqueda sin detalles como en la vista **Detalles**. Vista de lista es la vista predeterminada que se utiliza al abrir la página Resultados de la búsqueda.  
  
 Mantenga el mouse sobre un elemento y haga clic en la flecha de lista desplegable para abrir el menú desplegable donde podrá obtener acceso a las propiedades del elemento seleccionado y configurarlas.  
  
## <a name="see-also"></a>Vea también  
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Administrador de informes (Ayuda F1)](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
