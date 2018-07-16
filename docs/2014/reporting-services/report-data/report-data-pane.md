---
title: Panel Datos de informe | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.reportdata.f1
- "10039"
helpviewer_keywords:
- Report Data pane
ms.assetid: aa9614a3-12e7-4e17-9de2-fafccd1f5f9d
caps.latest.revision: 27
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 464bdb206986b01de68b018b8b6128956aee7036
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37270571"
---
# <a name="report-data-pane"></a>panel Datos de informe
  Use el panel **Datos de informe** para ver los parámetros, los orígenes de datos, los conjuntos de datos, las colecciones de campos y las imágenes que se han definido en el informe. El panel de informe muestra una vista jerárquica de los elementos que representan datos en el informe. Los nodos de nivel superior representan campos integrados, parámetros, imágenes y referencias a orígenes de datos. Expanda cada nodo para ver los elementos de datos. Por ejemplo, al expandir un nodo de origen de datos, aparecen los conjuntos de datos definidos para ese origen de datos. Al expandir un conjunto de datos, aparece su colección de campos. Arrastre los elementos hasta la superficie de diseño del informe para vincular los datos con los elementos de informe en la página de informe.  
  
## <a name="options"></a>Opciones  
 **Campos integrados**  
 Representa campos de Reporting Services que habitualmente se usan en un informe, como el nombre del informe o el número de página. Para obtener más información, vea [Colecciones integradas en expresiones &#40;Generador de informes y SSRS&#41;](../report-design/built-in-collections-in-expressions-report-builder.md).  
  
 **Parámetros**  
 Representa la colección de parámetros de informe. Cada uno de ellos puede tener uno o varios valores. Para obtener más información, vea [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../report-design/report-parameters-report-builder-and-report-designer.md).  
  
 **Imágenes**  
 Representa el conjunto de imágenes usadas en el informe. Para obtener más información, vea [Imágenes &#40;Generador de informes y SSRS&#41;](../report-design/images-report-builder-and-ssrs.md).  
  
 **Origen de datos**  
 Representa una única referencia a un origen de datos incrustado o a un origen de datos compartido. En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], los orígenes de datos compartidos aparecen en el Explorador de soluciones, debajo de la carpeta Orígenes de datos compartidos. Un origen de datos especifica uno de los tipos de orígenes de datos compatibles con Reporting Services. Un origen de datos es el nodo primario para la colección de conjuntos de datos que está basada en él. Para obtener más información, consulte [conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md) .  
  
 **Conjunto de datos**  
 Representa un único conjunto de datos. Un conjunto de datos es el nodo primario para la colección de campos especificados por la consulta e incluye cualquier campo calculado. Reporting Services admite el uso de diseñadores de consultas para ayudarle a especificar las consultas. Para obtener más información, consulte [agregar datos a un informe &#40;generador de informes y SSRS&#41; ](report-datasets-ssrs.md) y [herramientas de diseño de consulta de SQL Server Data Tools de diseñador de informes &#40;SSRS&#41;](query-design-tools-ssrs.md).  
  
## <a name="see-also"></a>Vea también  
 [Colección Campos del conjunto de datos &#40;Generador de informes y SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)   
 [Panel de agrupación](../tools/grouping-pane.md)  
  
  
