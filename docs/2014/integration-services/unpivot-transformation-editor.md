---
title: Editor de transformación Anulación de dinamización | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.unpivottransformation.f1
helpviewer_keywords:
- Unpivot Transformation Editor
ms.assetid: 72a36ef0-4070-4f6c-9c74-0720109617dd
caps.latest.revision: 34
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2864345230b02bc16756c82116dc40a53b2a7264
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37199665"
---
# <a name="unpivot-transformation-editor"></a>Editor de transformación Anulación de dinamización
  Use el cuadro de diálogo **Editor de transformación Anulación de dinamización** para seleccionar las columnas que se van a dinamizar en filas y especificar la columna de datos y la nueva columna de salida del valor dinámico.  
  
> [!NOTE]  
>  Este tema usa el escenario Anulación de dinamización descrito en [Transformación Anulación de dinamización](data-flow/transformations/unpivot-transformation.md) para mostrar el uso de las opciones.  
  
 Para obtener más información acerca de la transformación Anulación de dinamización, vea [Unpivot Transformation](data-flow/transformations/unpivot-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Columnas de entrada disponibles**  
 Especifique las columnas que deben pasar a ser filas mediante las casillas.  
  
 **Nombre**  
 Muestra el nombre de la columna de entrada disponible.  
  
 **Paso a través**  
 Indique si desea incluir la columna en la salida de anulación de dinamización.  
  
 **Columna de entrada**  
 Seleccione de la lista de entradas disponibles las columnas para cada fila. Las selecciones se reflejan en las casillas activadas en la tabla **Columnas de entrada disponibles** .  
  
 En el escenario Anulación de dinamización descrito en [Unpivot Transformation](data-flow/transformations/unpivot-transformation.md), las columnas de entrada son las columnas **Ham**, **Soda**, **Milk**, **Beer**y **Chips** .  
  
 **Columna de destino**  
 Escriba un nombre para la columna de datos.  
  
 En el escenario Anulación de dinamización descrito en [Transformación Anulación de dinamización](data-flow/transformations/unpivot-transformation.md), la columna de destino es la columna de cantidad (**Qty**).  
  
 **Valor de clave dinámica**  
 Escriba el nombre del valor de dinamización. El nombre predeterminado es el de la columna de entrada, pero puede elegir cualquier nombre descriptivo único.  
  
 Puede especificar el valor de esta propiedad con una expresión de propiedad.  
  
 En el escenario Anulación de dinamización descrito en [Unpivot Transformation](data-flow/transformations/unpivot-transformation.md), los valores de dinamización se mostrarán como valores de texto en la nueva columna Product, designada en la opción **Nombre de la columna del valor de clave dinámica** , como los valores de texto **Ham**, **Soda**, **Milk**, **Beer**y **Chips**.  
  
 **Nombre de la columna del valor de clave dinámica**  
 Escriba un nombre para la columna del valor de dinamización. El valor predeterminado es "Valor de clave dinámica", pero podrá elegir cualquier nombre descriptivo único.  
  
 En el escenario Anulación de dinamización descrito en [Unpivot Transformation](data-flow/transformations/unpivot-transformation.md), el Nombre de la columna del valor de clave dinámica es **Product** y designa la nueva columna **Product** en la que se anula la dinamización de las columnas **Ham**, **Soda**, **Milk**, **Beer**y **Chips** .  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Transformación dinámica](data-flow/transformations/pivot-transformation.md)  
  
  
