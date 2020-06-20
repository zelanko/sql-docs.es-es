---
title: Editor de transformación Unión de todo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.unionalltransformation.f1
helpviewer_keywords:
- Union All Transformation Editor
ms.assetid: 32fbc1c1-da83-4684-9479-31fc3e2df98c
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 6414b887ee88ddc0281ee86fd3236f026b8a3f28
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84972645"
---
# <a name="union-all-transformation-editor"></a>Editor de transformación Unión de todo
  Use el cuadro de diálogo **Editor de transformación Unión de todo** para combinar varios conjuntos de filas de entrada en un solo conjunto de filas de salida. Al incluir la transformación Unión de todo en un flujo de datos, puede combinar datos de varios flujos, crear conjuntos de datos complejos anidando transformaciones Unión de todo y volver a combinar filas después de corregir errores en los datos.  
  
 Para obtener más información acerca de la transformación Unión de todo, vea [Union All Transformation](data-flow/transformations/union-all-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Nombre de columna de salida**  
 Escriba un alias para cada columna. El valor predeterminado es el nombre de la columna de entrada de la primera entrada (referencia); no obstante, puede elegir un nombre descriptivo único.  
  
 **Entrada de Unión de todo 1**  
 Seleccione la primera entrada (referencia) de la lista de columnas de entrada disponibles. Los metadatos de las columnas asignadas deben coincidir.  
  
 **Entrada de Unión de todo n**  
 Seleccione la segunda entrada y las adicionales de la lista de columnas de entrada disponibles. Los metadatos de las columnas asignadas deben coincidir.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Combinar datos mediante la transformación Unión de todo](data-flow/transformations/merge-data-by-using-the-union-all-transformation.md)   
 [Transformación mezclar](data-flow/transformations/merge-transformation.md)   
 [Transformación Combinación de mezcla](data-flow/transformations/merge-join-transformation.md)  
  
  
