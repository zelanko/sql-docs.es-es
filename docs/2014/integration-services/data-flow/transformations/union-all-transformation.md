---
title: Transformación Unión | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.unionalltrans.f1
helpviewer_keywords:
- merging datasets [Integration Services]
- combining datasets
- Union All transformation
- datasets [Integration Services], merging
ms.assetid: 942e4b90-9c41-4e9c-a6f3-80b3afe57f2f
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 27547f95d50bd4552e766184f163dcd3b94a3bb8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36204435"
---
# <a name="union-all-transformation"></a>Unión de todo, transformación
  La transformación Unión de todo combina varias entradas en una salida. Por ejemplo, las salidas de cinco orígenes de archivos planos distintos pueden ser entradas de la transformación Unión de todo y combinarse en una salida.  
  
## <a name="inputs-and-outputs"></a>Entradas y salidas  
 Las entradas de la transformación se agregan una detrás de otra a la salida de transformación; las filas no se reordenan. Si el paquete requiere una salida ordenada, debe usar la transformación Combinar en lugar de la transformación Unión de todo.  
  
 La primera entrada que se puede conectar a la transformación Unión de todo es la entrada a partir de la cual la transformación crea su salida. Las columnas de las entradas que se conecten posteriormente a la transformación se asignarán a las columnas de la salida de transformación.  
  
 Para combinar entradas, debe asignar columnas de las entradas a columnas de la salida. Se debe asignar una columna con al menos una entrada a cada columna de salida. La asignación entre dos columnas requiere que los metadatos de las columnas coincidan. Por ejemplo, las columnas asignadas deben tener el mismo tipo de datos.  
  
 Si las columnas asignadas contienen datos de cadena y la columna de salida es de menor longitud que la columna de entrada, se aumenta automáticamente la longitud de la columna de salida para que pueda contener la columna de entrada. Las columnas de entrada que no se asignan a columnas de salida se establecen en valores NULL en las columnas de salida.  
  
 Esta transformación tiene varias entradas y una salida. No admite una salida de error.  
  
## <a name="configuration-of-the-union-all-transformation"></a>Configuración de la transformación Unión de todo  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el cuadro de diálogo **Editor de transformación Unión de todo** , vea [Union All Transformation Editor](../../union-all-transformation-editor.md).  
  
 Para obtener más información acerca de las propiedades que puede establecer mediante programación, vea [Common Properties](../../common-properties.md).  
  
 Para obtener más información sobre cómo establecer valores de propiedades, haga clic en uno de los temas siguientes:  
  
-   [Establecer las propiedades de un componente de flujo de datos](../set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 [Combinación de datos con la transformación Unión de todo](union-all-transformation.md)  
  
  