---
title: Planear un informe (Generador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- getting started
- report design
ms.assetid: 79113505-1ce8-4f8c-9260-d861838f7813
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9c659362e7b5ddba500c2e48df1b11a27a4bf0a5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66105460"
---
# <a name="planning-a-report-report-builder"></a>Planear un informe (Generador de informes)
  El Generador de informes permite crear muchos tipos de informes. Por ejemplo, puede crear informes que muestren los datos de ventas detallados o resumidos, las tendencias de marketing y de ventas, los informes de operaciones o los paneles. También puede crear informes que aprovechen el texto de formato enriquecido, por ejemplo, para pedidos de ventas, catálogos de productos o circulares. Todos estos informes se crean utilizando combinaciones diferentes de los mismos bloques de creación básicos en el Generador de informes. Para crear un informe útil, de fácil comprensión, sirve de ayuda planearlo primero. A continuación se detallan algunos de los aspectos que quizá desee considerar antes de empezar:  
  
-   **¿En qué formato desea que aparezca el informe?**  
  
     Puede representar en línea los informes en un explorador, como el Administrador de informes, o exportarlos a otros formatos como Excel, Word o PDF. La forma final que adopta el informe es una consideración importante porque no todas las características están disponibles en todos los formatos de exportación. Para obtener más información, vea [exportar informes &#40;generador de informes y SSRS&#41;](../report-builder/export-reports-report-builder-and-ssrs.md).  
  
-   **¿Qué estructura desea utilizar para presentar los datos en el informe?**  
  
     Tiene varias opciones entre las que elegir para presentar los datos, como formato tabular, matriz (similar a un informe de tabla de referencias cruzadas o de tabla dinámica), gráfico, las estructuras de forma libre, o cualquier combinación de estos. Para obtener más información, vea [las listas &#40;generador de informes y ssrs&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md) y [gráficos &#40;Generador de informes y SSRS&#41;](charts-report-builder-and-ssrs.md).  
  
-   **¿Qué aspecto desea que tenga el informe?**  
  
     El Generador de informes proporciona muchos elementos de informe que puede agregar al informe para que sea más fácil de leer, resaltar la información clave, ayudar a sus usuarios a navegar por el informe, etc. Si tiene clara la apariencia que desea para el diseño del informe, puede determinar si necesita elementos de informe como cuadros de texto, rectángulos, imágenes y líneas. Es posible que desee también mostrar u ocultar elementos, agregar un mapa del documento, incluir informes detallados o subinformes, o crear vínculos con otros informes. Para más información, vea [Imágenes, cuadros de texto rectángulos y líneas &#40;Generador de informes y SSRS&#41;](rectangles-and-lines-report-builder-and-ssrs.md) y [Ordenación interactiva, mapas de documento y vínculos &#40;Generador de informes y SSRS&#41;](interactive-sort-document-maps-and-links-report-builder-and-ssrs.md).  
  
-   **¿Qué datos desea que se presenten a sus lectores? ¿Quiere filtrar los datos o el formato para destinatarios distintos?**  
  
     Quizá prefiera restringir el ámbito del informe a ubicaciones o usuarios concretos, o a un período de tiempo determinado. Para filtrar los datos del informe, utilice los parámetros para recuperar y mostrar solo los datos que desea. Para más información, vea [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](report-parameters-report-builder-and-report-designer.md).  
  
-   **¿Necesita crear sus propios cálculos?**  
  
     A veces, el origen de datos y los conjuntos de datos no contienen los campos exactos que necesita para su informe. En esa situación, puede que tenga que crear sus propios campos calculados. Por ejemplo, quizá desee multiplicar la cantidad por el precio por las unidades de tiempo para obtener un importe de ventas de un artículo de línea. Las expresiones se utilizan también para proporcionar formato condicional y otras características avanzadas. Para más información, vea [Expresiones &#40;Generador de informes y SSRS&#41;](expressions-report-builder-and-ssrs.md).  
  
-   **¿Desea ocultar inicialmente los elementos del informe?**  
  
     Considere si desea ocultar los elementos del informe, incluidos los grupos, las regiones de datos y las columnas, cuando se ejecuta el informe por primera vez. Por ejemplo, puede presentar inicialmente una tabla de resumen y, a continuación, explorar en profundidad los datos detallados. Para más información, vea [Acción de obtención de detalles &#40;Generador de informes y SSRS&#41;](drilldown-action-report-builder-and-ssrs.md).  
  
-   **¿Cómo va a distribuir el informe?**  
  
     Puede guardar el informe en el equipo local y continuar trabajando en él, o ejecutarlo localmente para obtener su propia información. Sin embargo, para compartir el informe con otros usuarios, tendrá que guardarlo en un servidor de informes configurado en el modo nativo o en un servidor de informes en el modo integrado de SharePoint. Guardarlo en un servidor permite a otros usuarios ejecutarlo cuando lo deseen. Como alternativa, el administrador del servidor de informes puede configurar una suscripción al informe o configurar la distribución del informe por correo electrónico a otros individuos. Puede hacer que el informe se entregue en un formato de exportación concreto si lo prefiere. Para obtener más información, vea [Buscar, ver y administrar informes &#40;Generador de informes y SSRS&#41;](../report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte también  
 [Generador de informes en SQL Server 2014](../report-builder/report-builder-in-sql-server-2016.md)   
 [Conceptos de creación de informes &#40;Generador de informes y SSRS&#41;](report-authoring-concepts-report-builder-and-ssrs.md)   
 [Tutoriales &#40;Generador de informes&#41;](../report-builder-tutorials.md)  
  
  
