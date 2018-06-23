---
title: Cuadro de diálogo de propiedades de conjunto de datos, campos (generador de informes) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- "10021"
ms.assetid: 75c7e54a-3d20-4c9a-88da-ab36dce2ce42
caps.latest.revision: 14
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 8e9fa18bb0edfc2edac3e58e22467ba49a01cf50
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107137"
---
# <a name="dataset-properties-dialog-box-fields-report-builder"></a>Propiedades del conjunto de datos (cuadro de diálogo), Campos (Generador de informes)
  Seleccione **Campos** en el cuadro de diálogo **Propiedades del conjunto de datos** para cambiar la colección de campos para el conjunto de datos del informe. La lista de campos se rellena automáticamente, pero puede utilizar **Campos** para agregar, editar y eliminar campos calculados y de consulta.  
  
 Los campos calculados solo se admiten en conjuntos de datos insertados. Para más información, vea [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  
  
## <a name="options"></a>Opciones  
 **Agregar**  
 Agrega un nuevo campo calculado o de consulta al conjunto de datos.  
  
 **Eliminar**  
 Elimina el campo seleccionado del conjunto de datos.  
  
 **Nombre de campo**  
 Escriba el nombre del campo. El campo debe ser único en el conjunto de datos. Para cada campo existente en el conjunto de datos, el nombre se rellena previamente.  
  
 **Origen del campo**  
 Escriba un valor para el campo.  
  
 Para un campo calculado, el origen del campo debe ser el nombre de un campo existente recuperado por la consulta del conjunto de datos o por una expresión que cree personalmente. Por ejemplo, para crear un campo que representa 10 veces el valor en el campo de consulta Sales, utilice la expresión `=10 * Fields!Sales.Value`.  
  
 En el caso de un campo de consultas, el origen del campo debe ser el nombre de un campo existente recuperado por la consulta de conjunto de datos.  
  
 **Expresión (fx)**  
 Agregue o cambie una expresión para el nuevo campo calculado. Este botón solamente aparece cuando se hace clic en **Agregar** y se selecciona **Campo calculado**.  
  
## <a name="see-also"></a>Vea también  
 [Colección Campos del conjunto de datos &#40;Generador de informes y SSRS&#41;](report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [Crear un conjunto de datos compartido o un conjunto de datos incrustado &#40;Generador de informes y SSRS&#41;](report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)   
 [Ayuda del Generador de informes para cuadros de diálogo, paneles y asistentes](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [Cuadro de diálogo de propiedades de conjunto de datos, las opciones de &#40;generador de informes&#41;](report-data/dataset-properties-dialog-box-options-report-builder.md)   
 [Cuadro de diálogo de propiedades de conjunto de datos, filtros &#40;generador de informes&#41;](../../2014/reporting-services/dataset-properties-dialog-box-filters-report-builder.md)   
 [Cuadro de diálogo de propiedades de conjunto de datos, los parámetros de &#40;generador de informes&#41;](../../2014/reporting-services/dataset-properties-dialog-box-parameters-report-builder.md)   
 [Cuadro de diálogo de propiedades de conjunto de datos, realice una consulta &#40;generador de informes&#41;](report-data/dataset-properties-dialog-box-query-report-builder.md)   
 [Expresiones &#40;Generador de informes y SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)   
 [Conexiones de datos, orígenes de datos y cadenas de conexión en el Generador de informes](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md)  
  
  