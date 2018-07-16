---
title: Conectar componentes de un flujo de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- components [Integration Services], connections
- connections [Integration Services], data flow components
ms.assetid: 70616a58-8921-4218-85bf-f3e90c5a9dbf
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ba40d229725cb247c54119c59d8aa1f8de9e0331
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37223695"
---
# <a name="connect-components-in-a-data-flow"></a>Conectar componentes de un flujo de datos
  Este procedimiento describe cómo conectar la salida de los componentes de un flujo de datos con otros componentes dentro del mismo flujo de datos.  
  
### <a name="to-connect-components-in-a-data-flow"></a>Para conectar los componentes de un flujo de datos  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de control** y luego haga doble clic en la tarea Flujo de datos que contiene el flujo de datos donde quiere conectar componentes.  
  
4.  En la superficie de diseño de la pestaña **Flujo de datos** , seleccione la transformación u origen que desea conectar.  
  
5.  Arrastre la flecha verde de salida de una transformación o un origen a una transformación o a un destino. Algunos componentes de flujo de datos tienen salidas de error que se pueden conectar de la misma manera.  
  
    > [!NOTE]  
    >  Algunos componentes de flujo de datos pueden tener varias salidas y cada una de ellas se puede conectar con una transformación o destino diferente.  
  
6.  Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados**, en el menú **Archivo**.  
  
## <a name="see-also"></a>Vea también  
 [Agregar o eliminar un componente en un flujo de datos](data-flow.md)   
 [Configurar una salida de Error en un componente de flujo de datos](../configure-an-error-output-in-a-data-flow-component.md)   
 [Flujo de datos](data-flow.md)  
  
  
