---
title: Asignar columnas a dominios compuestos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: d9422412-8a3d-45ae-af7f-072c902a09ba
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9ce189688bd33f3cb63280e4fa44bb2284ee9e8d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62900041"
---
# <a name="map-columns-to-composite-domains"></a>Asignar columnas a dominios compuestos
  Un dominio compuesto consta de dos o más dominios individuales. Es posible asignar varias columnas, o una sola con valores delimitados, al dominio.  
  
 Si opta por varias columnas, deberá asignar una columna a cada dominio individual del dominio compuesto para aplicar las reglas de este último para la limpieza de datos. Para seleccionar los dominios individuales incluidos en el dominio compuesto, utilice Data Quality Client. Para más información, consulte [Crear un dominio compuesto](../../../data-quality-services/create-a-composite-domain.md).  
  
 Si dispone de una sola columna con valores delimitados, deberá asignarla al dominio compuesto. Los valores deben aparecer en el mismo orden en el que aparecen los dominios individuales en el dominio compuesto. El delimitador del origen de datos debe coincidir con el delimitador utilizado para analizar los valores del dominio compuesto. Para seleccionar el delimitador para el dominio compuesto, así como para establecer otras propiedades, utilice Data Quality Client. Para más información, consulte [Crear un dominio compuesto](../../../data-quality-services/create-a-composite-domain.md).  
  
### <a name="to-map-multiple-columns-to-a-composite-domain"></a>Para asignar varias columnas a un dominio compuesto  
  
1.  Haga clic con el botón derecho en la transformación Limpieza de DQS y, después, haga clic en **Editar**.  
  
2.  En la pestaña **Administrador de conexiones** , asegúrese de que el dominio compuesto aparece en la lista de dominios disponibles.  
  
3.  En la pestaña **Asignación** , seleccione las columnas en el área **Columnas de entrada disponibles** .  
  
4.  Para cada columna que aparezca en el campo **Columna de entrada** , seleccione un dominio individual en el campo **Dominio** . Seleccione solo dominios individuales que estén incluidos en el dominio compuesto.  
  
5.  Si fuera necesario, modifique los nombres que aparecen en los campos **Alias de origen**, **Alias de salida**y **Alias de estado** .  
  
6.  Si fuera necesario, establezca propiedades en la pestaña **Avanzadas** . Para obtener más información acerca de las propiedades, vea [DQS Cleansing Transformation Editor Dialog Box](../../dqs-cleansing-transformation-editor-dialog-box.md).  
  
### <a name="to-map-a-column-with-delimited-values-to-a-composite-domain"></a>Para asignar una columna con valores delimitados a un dominio compuesto  
  
1.  Haga clic con el botón derecho en la transformación Limpieza de DQS y, después, haga clic en **Editar**.  
  
2.  En la pestaña **Administrador de conexiones** , asegúrese de que el dominio compuesto aparece en la lista de dominios disponibles.  
  
3.  En la pestaña **Asignación** , seleccione la columna en el área **Columnas de entrada disponibles** .  
  
4.  Para la columna que aparece en el campo **Columna de entrada** , seleccione el dominio compuesto en el campo **Dominio** .  
  
5.  Si fuera necesario, modifique los nombres que aparecen en los campos **Alias de origen**, **Alias de salida**y **Alias de estado** .  
  
6.  Si fuera necesario, establezca propiedades en la pestaña **Avanzadas** . Para obtener más información acerca de las propiedades, vea [DQS Cleansing Transformation Editor Dialog Box](../../dqs-cleansing-transformation-editor-dialog-box.md).  
  
## <a name="see-also"></a>Consulte también  
 [Transformación Limpieza de DQS](dqs-cleansing-transformation.md)  
  
  
