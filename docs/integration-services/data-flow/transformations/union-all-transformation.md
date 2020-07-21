---
title: Transformación Unión | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.unionalltrans.f1
- sql13.dts.designer.unionalltransformation.f1
helpviewer_keywords:
- merging datasets [Integration Services]
- combining datasets
- Union All transformation
- datasets [Integration Services], merging
ms.assetid: 942e4b90-9c41-4e9c-a6f3-80b3afe57f2f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0b9f629126dcd5a8f81eeab444aef50456589e4a
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "71291005"
---
# <a name="union-all-transformation"></a>Unión de todo, transformación

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La transformación Unión de todo combina varias entradas en una salida. Por ejemplo, las salidas de cinco orígenes de archivos planos distintos pueden ser entradas de la transformación Unión de todo y combinarse en una salida.  
  
## <a name="inputs-and-outputs"></a>Entradas y salidas  
 Las entradas de la transformación se agregan una detrás de otra a la salida de transformación; las filas no se reordenan. Si el paquete requiere una salida ordenada, debe usar la transformación Combinar en lugar de la transformación Unión de todo.  
  
 La primera entrada que se puede conectar a la transformación Unión de todo es la entrada a partir de la cual la transformación crea su salida. Las columnas de las entradas que se conecten posteriormente a la transformación se asignarán a las columnas de la salida de transformación.  
  
 Para combinar entradas, debe asignar columnas de las entradas a columnas de la salida. Se debe asignar una columna con al menos una entrada a cada columna de salida. La asignación entre dos columnas requiere que los metadatos de las columnas coincidan. Por ejemplo, las columnas asignadas deben tener el mismo tipo de datos.  
  
 Si las columnas asignadas contienen datos de cadena y la columna de salida es de menor longitud que la columna de entrada, se aumenta automáticamente la longitud de la columna de salida para que pueda contener la columna de entrada. Las columnas de entrada que no se asignan a columnas de salida se establecen en valores NULL en las columnas de salida.  
  
 Esta transformación tiene varias entradas y una salida. No admite una salida de error.  
  
## <a name="configuration-of-the-union-all-transformation"></a>Configuración de la transformación Unión de todo  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer mediante programación, vea [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796).  
  
 Para obtener más información sobre cómo establecer valores de propiedades, haga clic en uno de los temas siguientes:  
  
-   [Establecer las propiedades de un componente de flujo de datos](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="union-all-transformation-editor"></a>Editor de transformación Unión de todo
  Use el cuadro de diálogo **Editor de transformación Unión de todo** para combinar varios conjuntos de filas de entrada en un solo conjunto de filas de salida. Al incluir la transformación Unión de todo en un flujo de datos, puede combinar datos de varios flujos, crear conjuntos de datos complejos anidando transformaciones Unión de todo y volver a combinar filas después de corregir errores en los datos.  
  
### <a name="options"></a>Opciones  
 **Nombre de la columna de salida**  
 Escriba un alias para cada columna. El valor predeterminado es el nombre de la columna de entrada de la primera entrada (referencia); no obstante, puede elegir un nombre descriptivo único.  
  
 **Entrada de Unión de todo 1**  
 Seleccione la primera entrada (referencia) de la lista de columnas de entrada disponibles. Los metadatos de las columnas asignadas deben coincidir.  
  
 **Entrada de Unión de todo n**  
 Seleccione la segunda entrada y las adicionales de la lista de columnas de entrada disponibles. Los metadatos de las columnas asignadas deben coincidir.  
  
## <a name="related-tasks"></a>Related Tasks  
 [Combinación de datos con la transformación Unión de todo](../../../integration-services/data-flow/transformations/merge-data-by-using-the-union-all-transformation.md)  
  
  
