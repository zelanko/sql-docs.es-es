---
title: Dirigir el flujo CDC según el tipo de cambio | Microsoft Docs
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
ms.assetid: 3afa531e-f425-40a4-a1bf-1c3e1727287e
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 451e07f8bb2b5861ac56b88f7ca17b5e19ef9095
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="direct-the-cdc-stream-according-to-the-type-of-change"></a>Dirigir el flujo CDC según el tipo de cambio
  Para agregar y configurar una transformación Divisor CDC, el paquete debe contener por lo menos una tarea Flujo de datos y un origen de CDC.  
  
 El origen de CDC agregado al paquete debe tener seleccionado un modo de procesamiento de NetCDC. Para obtener más información sobre cómo seleccionar los modos de procesamiento, vea [Editor de origen de CDC &#40;página Administrador de conexiones&#41;](../../integration-services/data-flow/cdc-source-editor-connection-manager-page.md).  
  
### <a name="to-direct-the-cdc-stream-according-to-the-type-of-change"></a>Para dirigir el flujo CDC según el tipo de cambio  
  
1.  En [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra el proyecto de [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de datos** y, a continuación, desde el **cuadro de herramientas**, arrastre el divisor CDC a la superficie de diseño.  
  
4.  Conéctese al origen de CDC que se incluye en el paquete al divisor CDC.  
  
5.  Conecte el divisor CDC a uno o varios destinos. Puede conectarse hasta a tres salidas diferentes.  
  
6.  Seleccione una de las siguientes salidas:  
  
    -   Salida Delete: la salida donde se dirigen las filas de cambios DELETE.  
  
    -   Salida Insert: la salida donde se dirigen las filas de cambios INSERT.  
  
    -   Salida Update: la salida donde se dirigen las filas de cambios UPDATE antes o después y las filas de cambios Merge.  
  
7.  Opcionalmente, puede configurar las propiedades avanzadas mediante el cuadro de diálogo **Editor avanzado** .  
  
     El cuadro de diálogo **Editor avanzado** contiene las propiedades que se pueden establecer mediante programación.  
  
     Para abrir el cuadro de diálogo **Editor avanzado** :  
  
    -   En la pantalla **Flujo de datos** del proyecto de [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] , haga clic con el botón secundario en el divisor CDC y seleccione **Mostrar editor avanzado**.  
  
     Para obtener más información sobre cómo usar el divisor CDC, vea Componentes CDC para Microsoft SQL Server Integration Services.  
  
## <a name="see-also"></a>Ver también  
 [Divisor CDC](../../integration-services/data-flow/cdc-splitter.md)  
  
  
