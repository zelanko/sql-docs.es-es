---
title: Solución de problemas de diseño de informes con Reporting Services | Microsoft Docs
ms.date: 02/27/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
ms.assetid: a0d103da-5a3e-475c-a71a-9e23476095e2
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b3eb298bc6b359b0df92566f9add8d7011cdc907
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "65573850"
---
# <a name="troubleshoot-report-design-issues-with-reporting-services"></a>Solución de problemas de diseño de informes con Reporting Services
Los problemas de diseño se pueden producir al crear un diseño de un informe en la vista Diseño en una aplicación de creación de informes. Utilice este tema como ayuda para solucionar estos problemas.   
  
## <a name="why-does-my-text-box-show-only-a-single-value-and-not-repeat-for-every-row"></a>¿Por qué el cuadro de texto muestra solamente un valor y no se repite para cada fila?  
Un cuadro de texto con una referencia del campo de conjunto de datos solamente se representa una vez y muestra el primer valor en el conjunto de datos.   
  
**El contenedor primario del cuadro de texto es el cuerpo del informe**  
  
  
Un cuadro de texto agregado directamente a la superficie de diseño puede mostrar solamente un valor agregado para un conjunto de datos.  
  
Para comprobar el contenedor principal de un cuadro de texto, seleccione el cuadro de texto y en el panel Propiedades, desplácese a **Principal**.   
  
Si desea que los cuadros de texto muestren cada valor en un conjunto de datos, utilice una región de datos, como una tabla o matriz. De forma predeterminada, cada celda de una tabla o matriz contiene un cuadro de texto. Arrastre los campos del conjunto de datos hasta cada celda.   
  
## <a name="why-cant-i-add-total-pages-to-my-report"></a>¿Por qué no puedo agregar Total de páginas a mi informe?  
Los campos integrados `[&PageNumber]` y `[&TotalPages]` no son válidos en el cuerpo del informe.   
  
PageNumber y TotalPages solo son válidos en el encabezado de página y en el pie de página.  
  
  
Los campos integrados [&PageNumber] y [&TotalPages] solo son válidos en el encabezado de página y en el pie de página.   
  
Para agregar los campos [&PageNumber] o [&TotalPages] a un informe, primero debe agregar un encabezado de página o un pie de página. Para más información, consulte [Agregar o quitar un encabezado](../../reporting-services/report-design/add-or-remove-a-page-header-or-footer-report-builder-and-ssrs.md).  
  
> [!NOTE]  
> Incluir [&TotalPages] en el encabezado de página o el pie de página puede tener consecuencias para el procesamiento del informe. Para más información, consulte Solucionar problemas: informes exportados a un formato de archivo específico.  
[Solución de problemas de procesamiento de informes de Reporting Services](../../reporting-services/troubleshooting/troubleshoot-processing-of-reporting-services-reports.md).  
  
## <a name="how-do-i-design-two-tables-or-a-chart-and-a-table-to-display-side-by-side"></a>¿Cómo diseño dos tablas o un gráfico y una tabla de forma que se muestren en paralelo?  
Diseñar un informe no es una experiencia WYSISYG ("lo que se ve es lo que se obtiene"). El procesador del informe combina datos, elementos de informe e información de diseño del informe como el espacio en blanco, contenedores y expresiones para generar un informe compilado que se pasa a continuación a un representador de informes que "dispone" ese informe según la experiencia de visualización especificada: de forma interactiva para un explorador HTML o como formato de archivo. Los algoritmos de diseño automático pueden generar un diseño de informe que desee cambiar.   
  
### <a name="rendering-rules-use-page-size-containers-peer-objects-relative-placement-and-white-space-to-determine-layout"></a>Representar el uso de reglas tamaño de página, contenedores, objetos del mismo nivel, posición relativa y espacio en blanco para determinar el diseño  
En general, un informe crece para alojar sus datos e insertar otros elementos de informe al lado.   
  
Para agrupar varias regiones de datos o elementos de informe, colóquelos en el mismo contenedor primario. Por ejemplo, coloque un gráfico y una tabla en un contenedor de rectángulo y alinee sus bordes superiores para mostrarlos en paralelo. Para más información, consulte [Comportamientos de la representación (Generador de informes y SSRS)](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte también  
[Solución de problemas de recuperación de datos de informes de Reporting Services](../../reporting-services/troubleshooting/troubleshoot-data-retrieval-issues-with-reporting-services-reports.md)  
[Solución de problemas de suscripciones y entrega de Reporting Services](../../reporting-services/troubleshooting/troubleshoot-reporting-services-subscriptions-and-delivery.md)  
  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

