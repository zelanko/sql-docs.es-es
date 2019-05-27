---
title: Buscar texto, números o fechas en un informe (Reporting Services en modo integrado de SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- searching reports
ms.assetid: 309dffe5-00f5-404f-bb63-9e6046253ae0
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6cf40f4d3baa60caa0d9d44f372e41521497e33e
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66102666"
---
# <a name="find-text-numbers-or-dates-in-a-report-reporting-services-in-sharepoint-integrated-mode"></a>Buscar texto, números o fechas en un informe (Reporting Services en el modo integrado de SharePoint)
  Puede buscar contenido del informe si escribe una palabra o una frase que se desee encontrar (el valor máximo de un término de búsqueda es 256 caracteres). La búsqueda es una técnica de navegación que encuentra un valor coincidente en el informe y se centra en la parte del informe que contiene ese valor.  
  
 La búsqueda distingue entre mayúsculas y minúsculas, y empieza en la página o sección seleccionada. Solo el contenido que está visible en el informe se incluye en la operación de búsqueda. Si el informe contiene áreas que se expanden o se contraen, los valores que están en un área contraída se omiten durante la búsqueda. Solo puede buscar texto, números o fechas que están en el informe actual. Si está usando un informe click-through autogenerado para explorar datos, no puede buscar un término que vio en un informe generado anteriormente ni usar la búsqueda para localizar un término que pueda aparecer en un informe más hacia abajo en la ruta de datos.  
  
 Al especificar el valor que desee buscar, escríbalo como prevé que aparezca en el informe. No plantee ninguna pregunta del tipo "¿cuál es el beneficio medio de este mes?", salvo que esté buscando una frase con todas estas palabras en el informe.  
  
 Solo puede buscar un término o un valor a la vez. No se pueden usar operadores de búsqueda (como AND u OR) ni símbolos y comodines. No puede realizar una búsqueda en una sección transversal de los datos (por ejemplo, no puede buscar el total de ventas de un producto determinado en un mes concreto). Para ese tipo de análisis, use el Generador de informes para crear o usar informes click-through.  
  
 La configuración de seguridad de modelos y bases de datos que restringe el acceso a los datos de informe se aplica a las operaciones de búsqueda. Si está buscando un valor en un informe click-through que utiliza un modelo como origen de datos y no dispone de acceso a parte del modelo, los datos representados por dicha parte del modelo se excluirán de la búsqueda.  
  
### <a name="to-find-data-in-a-report"></a>Para buscar los datos en un informe  
  
1.  Abra el informe.  
  
2.  En la barra de herramientas del informe, escriba el texto, el número o la fecha que desee buscar.  
  
     Si la barra de herramientas del informe no se encuentra visible, significa que se ha ocultado intencionadamente y que no puede usar sus funciones. Las propiedades del elemento web Visor de informes determinan si la barra de herramientas está visible.  
  
3.  Haga clic en **Buscar**.  
  
4.  Para buscar más repeticiones del mismo valor, haga clic en **Siguiente**.  
  
## <a name="see-also"></a>Vea también  
 [Agregar el elemento web Visor de informes a una página web &#40;Reporting Services en el modo integrado de SharePoint&#41;](../report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)  
  
  
