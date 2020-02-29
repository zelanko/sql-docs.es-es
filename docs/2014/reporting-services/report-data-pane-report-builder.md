---
title: Panel datos de informe (Generador de informes) | Microsoft Docs
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
ms.openlocfilehash: 2a77024e62402cea0a37b945e0539274fee9a3c6
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/28/2020
ms.locfileid: "78173334"
---
# <a name="report-data-pane-report-builder"></a>Panel Datos de informe (Generador de informes)
  Use el panel **Datos de informe** para ver los parámetros, los orígenes de datos, los conjuntos de datos, las colecciones de campos y las imágenes que se han definido en el informe. El panel de informe muestra una vista jerárquica de los elementos que representan datos en el informe. Los nodos de nivel superior representan campos integrados, parámetros, imágenes y referencias a orígenes de datos. Expanda cada nodo para ver los elementos de datos. Por ejemplo, al expandir un nodo de origen de datos, aparecen los conjuntos de datos definidos para ese origen de datos. Al expandir un conjunto de datos, aparece su colección de campos. Arrastre los elementos a la superficie de diseño del informe o al Panel de agrupación para vincular los datos con los elementos de informe seleccionados en la página del informe. Para más información, vea [Vista de diseño de informe &#40;Generador de informes&#41;](report-builder/report-design-view-report-builder.md).

## <a name="options"></a>Opciones
 **Campos integrados** Representa campos de uso frecuente en un informe, como el nombre del informe o el número de página. Para obtener más información, vea [Colecciones integradas en expresiones &#40;Generador de informes y SSRS&#41;](report-design/built-in-collections-in-expressions-report-builder.md).

 **Parámetros** de Representa la colección de parámetros de informe, cada uno de los cuales puede ser de un solo valor o de varios valores. Para más información, vea [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](report-design/report-parameters-report-builder-and-report-designer.md).

 **Imágenes** de Representa el conjunto de imágenes usadas en el informe. Para obtener más información, vea [Imágenes &#40;Generador de informes y SSRS&#41;](report-design/images-report-builder-and-ssrs.md).

 **Orígenes de datos** Representa un origen de datos incrustado o una referencia a un origen de datos compartido. Un origen de datos representa un origen de los datos correspondientes al informe. Un origen de datos es el nodo primario de la colección de conjuntos de datos que lo usa. Para obtener más información, vea [Agregar datos a un informe &#40;generador de informes y SSRS&#41;](report-data/report-datasets-ssrs.md) y [conexiones de datos, orígenes de datos y cadenas de conexión en generador de informes](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md).

 **Conjuntos de valores** Representa los datos que se recuperan de un origen de datos mediante la ejecución de un comando, [!INCLUDE[tsql](../includes/tsql-md.md)] por ejemplo, una consulta que recupera [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] datos de una base de datos. Un conjunto de datos es el nodo primario para la colección de campos especificados por la consulta e incluye también cualquier campo calculado. El Generador de informes admite el uso de diseñadores de consultas, que ayudan a especificar las consultas. Para obtener más información, vea [Agregar datos a un informe &#40;generador de informes y SSRS&#41;](report-data/report-datasets-ssrs.md).

## <a name="see-also"></a>Consulte también
 [Colección de campos de conjunto de &#40;generador de informes y SSRS&#41;](report-data/dataset-fields-collection-report-builder-and-ssrs.md) [generador de informes la ayuda de los cuadros de diálogo, paneles y asistentes de](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md) [agrupación](report-design/grouping-pane-report-builder.md) &#40;generador de informes&#41;[buscar, ver y administrar informes &#40;generador de informes y SSRS &#41;](report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)


