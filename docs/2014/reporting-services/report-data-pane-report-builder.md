---
title: Informes de panel de datos (generador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10435"
helpviewer_keywords:
- Report Data pane
ms.assetid: 1492aa39-aeb1-4509-ab97-b9edd0901b7e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fa8ae6d36ddd7c23b48ec65f8fab387e690f1d83
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66107558"
---
# <a name="report-data-pane-report-builder"></a>Panel Datos de informe (Generador de informes)
  Use el panel **Datos de informe** para ver los parámetros, los orígenes de datos, los conjuntos de datos, las colecciones de campos y las imágenes que se han definido en el informe. El panel de informe muestra una vista jerárquica de los elementos que representan datos en el informe. Los nodos de nivel superior representan campos integrados, parámetros, imágenes y referencias a orígenes de datos. Expanda cada nodo para ver los elementos de datos. Por ejemplo, al expandir un nodo de origen de datos, aparecen los conjuntos de datos definidos para ese origen de datos. Al expandir un conjunto de datos, aparece su colección de campos. Arrastre los elementos a la superficie de diseño del informe o al Panel de agrupación para vincular los datos con los elementos de informe seleccionados en la página del informe. Para más información, vea [Vista de diseño de informe &#40;Generador de informes&#41;](report-builder/report-design-view-report-builder.md).  
  
## <a name="options"></a>Opciones  
 **Campos integrados**  
 Representa los campos más usados en un informe, como el nombre del informe o el número de página. Para obtener más información, vea [Colecciones integradas en expresiones &#40;Generador de informes y SSRS&#41;](report-design/built-in-collections-in-expressions-report-builder.md).  
  
 **Parámetros**  
 Representa la colección de parámetros de informe. Cada uno de ellos puede tener uno o varios valores. Para más información, vea [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](report-design/report-parameters-report-builder-and-report-designer.md).  
  
 **Imágenes**  
 Representa el conjunto de imágenes usadas en el informe. Para obtener más información, vea [Imágenes &#40;Generador de informes y SSRS&#41;](report-design/images-report-builder-and-ssrs.md).  
  
 **Orígenes de datos**  
 Representa un origen de datos incrustado o una referencia a un origen de datos compartido. Un origen de datos representa un origen de los datos correspondientes al informe. Un origen de datos es el nodo primario de la colección de conjuntos de datos que lo usa. Para obtener más información, consulte [agregar datos a un informe &#40;generador de informes y SSRS&#41; ](report-data/report-datasets-ssrs.md) y [conexiones de datos, orígenes de datos y cadenas de conexión en el generador de informes](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md).  
  
 **Conjuntos de datos**  
 Representa los datos que se recuperan de un origen de datos ejecutando un comando, por ejemplo, una consulta [!INCLUDE[tsql](../includes/tsql-md.md)] que recupera los datos de una base de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Un conjunto de datos es el nodo primario para la colección de campos especificados por la consulta e incluye también cualquier campo calculado. El Generador de informes admite el uso de diseñadores de consultas, que ayudan a especificar las consultas. Para obtener más información, consulte [agregar datos a un informe &#40;generador de informes y SSRS&#41;](report-data/report-datasets-ssrs.md).  
  
## <a name="see-also"></a>Vea también  
 [Colección Campos del conjunto de datos &#40;Generador de informes y SSRS&#41;](report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [Ayuda del Generador de informes para cuadros de diálogo, paneles y asistentes](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [Panel de agrupación &#40;Generador de informes&#41;](report-design/grouping-pane-report-builder.md)   
 [Buscar, ver y administrar informes &#40;Generador de informes y SSRS&#41;](report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  
