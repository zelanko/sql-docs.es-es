---
title: Asignar columnas a dominios compuestos | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d9422412-8a3d-45ae-af7f-072c902a09ba
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4db874af0599526ceca5f7a8648436ec88b7f074
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
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
  
6.  Si fuera necesario, establezca propiedades en la pestaña **Avanzadas** . Para obtener más información acerca de las propiedades, vea [DQS Cleansing Transformation Editor Dialog Box](../../../integration-services/data-flow/transformations/dqs-cleansing-transformation-editor-dialog-box.md).  
  
### <a name="to-map-a-column-with-delimited-values-to-a-composite-domain"></a>Para asignar una columna con valores delimitados a un dominio compuesto  
  
1.  Haga clic con el botón derecho en la transformación Limpieza de DQS y, después, haga clic en **Editar**.  
  
2.  En la pestaña **Administrador de conexiones** , asegúrese de que el dominio compuesto aparece en la lista de dominios disponibles.  
  
3.  En la pestaña **Asignación** , seleccione la columna en el área **Columnas de entrada disponibles** .  
  
4.  Para la columna que aparece en el campo **Columna de entrada** , seleccione el dominio compuesto en el campo **Dominio** .  
  
5.  Si fuera necesario, modifique los nombres que aparecen en los campos **Alias de origen**, **Alias de salida**y **Alias de estado** .  
  
6.  Si fuera necesario, establezca propiedades en la pestaña **Avanzadas** . Para obtener más información acerca de las propiedades, vea [DQS Cleansing Transformation Editor Dialog Box](../../../integration-services/data-flow/transformations/dqs-cleansing-transformation-editor-dialog-box.md).  
  
## <a name="see-also"></a>Ver también  
 [Transformación Limpieza de DQS](../../../integration-services/data-flow/transformations/dqs-cleansing-transformation.md)  
  
  
