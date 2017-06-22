---
title: Panel datos de informe | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10039"
- sql13.rtp.rptdesigner.reportdata.f1
- "10435"
helpviewer_keywords:
- Report Data pane
ms.assetid: aa9614a3-12e7-4e17-9de2-fafccd1f5f9d
caps.latest.revision: 28
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a832dfb9d5e5e3fc57519b8f694bd47fa755852e
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="report-data-pane"></a>panel Datos de informe
  Use el panel **Datos de informe** para ver los parámetros, los orígenes de datos, los conjuntos de datos, las colecciones de campos y las imágenes que se han definido en el informe. El panel de informe muestra una vista jerárquica de los elementos que representan datos en el informe. Los nodos de nivel superior representan campos integrados, parámetros, imágenes y referencias a orígenes de datos. Expanda cada nodo para ver los elementos de datos. Por ejemplo, al expandir un nodo de origen de datos, aparecen los conjuntos de datos definidos para ese origen de datos. Al expandir un conjunto de datos, aparece su colección de campos. Arrastre los elementos hasta la superficie de diseño del informe para vincular los datos con los elementos de informe en la página de informe.  
  
## <a name="options"></a>Opciones  
 **Campos integrados**  
 Representa campos de Reporting Services que habitualmente se usan en un informe, como el nombre del informe o el número de página. Para obtener más información, vea [Colecciones integradas en expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md).  
  
 **Parámetros**  
 Representa la colección de parámetros de informe. Cada uno de ellos puede tener uno o varios valores. Para más información, vea [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
 **Imágenes**  
 Representa el conjunto de imágenes usadas en el informe. Para obtener más información, vea [Imágenes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md).  
  
 **Origen de datos**  
 Representa una única referencia a un origen de datos incrustado o a un origen de datos compartido. En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], los orígenes de datos compartidos aparecen en el Explorador de soluciones, debajo de la carpeta Orígenes de datos compartidos. Un origen de datos especifica uno de los tipos de orígenes de datos compatibles con Reporting Services. Un origen de datos es el nodo primario para la colección de conjuntos de datos que está basada en él. Para obtener más información, vea [Conexiones de datos, orígenes de datos y cadenas de conexión &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).  
  
 **Conjunto de datos**  
 Representa un único conjunto de datos. Un conjunto de datos es el nodo primario para la colección de campos especificados por la consulta e incluye cualquier campo calculado. Reporting Services admite el uso de diseñadores de consultas para ayudarle a especificar las consultas. Para obtener más información, vea [Conjuntos de datos de informe &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md) y [Herramientas de diseño de consulta &#40;SSRS&#41;](../../reporting-services/report-data/query-design-tools-ssrs.md).  
  
## <a name="see-also"></a>Vea también  
 [Colección Campos del conjunto de datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [Panel de agrupación](../../reporting-services/tools/grouping-pane.md)  
  
  
