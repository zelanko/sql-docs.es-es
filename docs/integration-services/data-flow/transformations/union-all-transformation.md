---
title: "Transformaci&#243;n Uni&#243;n de todo | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.unionalltrans.f1"
helpviewer_keywords: 
  - "conjuntos de datos, combinar [Integration Services]"
  - "combinar conjuntos de datos"
  - "Unión de todo, transformación"
  - "conjuntos de datos [Integration Services], combinar"
ms.assetid: 942e4b90-9c41-4e9c-a6f3-80b3afe57f2f
caps.latest.revision: 39
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 39
---
# Transformaci&#243;n Uni&#243;n de todo
  La transformación Unión de todo combina varias entradas en una salida. Por ejemplo, las salidas de cinco orígenes de archivos planos distintos pueden ser entradas de la transformación Unión de todo y combinarse en una salida.  
  
## Entradas y salidas  
 Las entradas de la transformación se agregan una detrás de otra a la salida de transformación; las filas no se reordenan. Si el paquete requiere una salida ordenada, debe usar la transformación Combinar en lugar de la transformación Unión de todo.  
  
 La primera entrada que se puede conectar a la transformación Unión de todo es la entrada a partir de la cual la transformación crea su salida. Las columnas de las entradas que se conecten posteriormente a la transformación se asignarán a las columnas de la salida de transformación.  
  
 Para combinar entradas, debe asignar columnas de las entradas a columnas de la salida. Se debe asignar una columna con al menos una entrada a cada columna de salida. La asignación entre dos columnas requiere que los metadatos de las columnas coincidan. Por ejemplo, las columnas asignadas deben tener el mismo tipo de datos.  
  
 Si las columnas asignadas contienen datos de cadena y la columna de salida es de menor longitud que la columna de entrada, se aumenta automáticamente la longitud de la columna de salida para que pueda contener la columna de entrada. Las columnas de entrada que no se asignan a columnas de salida se establecen en valores NULL en las columnas de salida.  
  
 Esta transformación tiene varias entradas y una salida. No admite una salida de error.  
  
## Configuración de la transformación Unión de todo  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el cuadro de diálogo **Editor de transformación Unión de todo** , vea [Union All Transformation Editor](../../../integration-services/data-flow/transformations/union-all-transformation-editor.md).  
  
 Para obtener más información acerca de las propiedades que puede establecer mediante programación, vea [Common Properties](../Topic/Common%20Properties.md).  
  
 Para obtener más información sobre cómo establecer valores de propiedades, haga clic en uno de los temas siguientes:  
  
-   [Establecer las propiedades de un componente de flujo de datos](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## Tareas relacionadas  
 [Combinar datos mediante la transformación Unión de todo](../../../integration-services/data-flow/transformations/merge-data-by-using-the-union-all-transformation.md)  
  
  