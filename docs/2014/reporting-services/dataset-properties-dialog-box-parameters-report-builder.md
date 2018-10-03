---
title: Cuadro de diálogo Propiedades del conjunto de datos, parámetros (generador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10023"
ms.assetid: 3a0672ad-c969-455b-b952-585164ce1dda
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bb8ac0237fc9175f29471a66b7e3916122b55707
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48082295"
---
# <a name="dataset-properties-dialog-box-parameters-report-builder"></a>Propiedades del conjunto de datos (cuadro de diálogo), Parámetros (Generador de informes)
  Seleccione **parámetros** en el **las propiedades del conjunto de datos** cuadro de diálogo para agregar, cambiar y eliminar parámetros de consulta.  
  
 Para un conjunto de datos incrustado, las opciones se aplican al conjunto de datos de la definición de informe.  
  
 Para un conjunto de datos compartido, las opciones se aplican a la definición del conjunto de datos compartido del servidor de informes.  
  
 Para más información, vea [Conjuntos de datos incrustados y compartidos &#40;Generador de informes y SSRS&#41;](report-data/embedded-and-shared-datasets-report-builder-and-ssrs.md).  
  
## <a name="options"></a>Opciones  
 **Agregar**  
 Agrega un parámetro nuevo a la lista.  
  
 **Eliminar**  
 Quita el parámetro seleccionado de la lista.  
  
 **Flecha arriba**  
 Mueve el parámetro seleccionado hacia arriba en la lista.  
  
 **Flecha abajo**  
 Mueve el parámetro seleccionado hacia abajo en la lista.  
  
 **Nombre del parámetro**  
 Escriba el nombre de un parámetro de consulta que agregó al conjunto de datos en la pestaña **Consulta** del cuadro de diálogo **Propiedades del conjunto de datos** .  
  
 **Valor de parámetro**  
 Para conjuntos de datos incrustados únicamente.  
  
 Escriba un valor para el parámetro de la consulta. Puede ser un valor estático o una expresión que haga referencia a un objeto del informe, pero no puede hacer referencia a elementos o campos de informe. De forma predeterminada, **Valor** contiene una expresión que apunta a un parámetro de informe.  
  
 **Valor predeterminado**  
 Para conjuntos de datos compartidos únicamente.  
  
 Active la casilla para especificar un valor predeterminado.  
  
 Escriba un valor predeterminado. Puede ser un valor estático o una expresión que haga referencia a un objeto del informe. La expresión no puede hacer referencia a elementos de informe, parámetros de informe ni campos.  
  
 Para especificar un espacio en blanco, deje el cuadro de texto vacío.  
  
 Para especificar un valor nulo, seleccione la opción de aceptación de valores NULL.  
  
 **Solo lectura**  
 Para conjuntos de datos compartidos únicamente.  
  
 Seleccione esta opción para marcar este parámetro como de solo lectura en la definición del conjunto de datos compartido. Cuando el conjunto de datos compartido se agrega a un informe, el parámetro no aparece en las propiedades. Cuando el conjunto de datos compartido está almacenado en la memoria caché del servidor de informes, el valor no se puede cambiar.  
  
 **Admisión de valores NULL**  
 Para conjuntos de datos compartidos únicamente.  
  
 Seleccione esta opción para admitir un valor nulo.  
  
 **Omitir en la consulta**  
 Para conjuntos de datos compartidos únicamente.  
  
 Seleccione esta opción cuando una referencia a un parámetro de informe esté en una expresión en el filtro del conjunto de datos compartido y no en la consulta. Al seleccionar esta opción, no necesita especificar un valor predeterminado para este parámetro cuando se ejecuta la consulta.  
  
## <a name="see-also"></a>Vea también  
 [Ayuda del Generador de informes para cuadros de diálogo, paneles y asistentes](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [Cuadro de diálogo de propiedades de conjunto de datos, la consulta &#40;generador de informes&#41;](report-data/dataset-properties-dialog-box-query-report-builder.md)   
 [Expresiones &#40;Generador de informes y SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)   
 [Tutorial: Agregar un parámetro a un informe &#40;Generador de informes&#41;](tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](report-design/report-parameters-report-builder-and-report-designer.md)   
 [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Diseñadores de consultas &#40;Generador de informes&#41;](../../2014/reporting-services/query-designers-report-builder.md)   
 [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Crear un conjunto de datos compartido o un conjunto de datos incrustado &#40;Generador de informes y SSRS&#41;](report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
  
