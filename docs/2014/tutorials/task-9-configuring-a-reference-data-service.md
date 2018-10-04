---
title: 'Tarea 9: Configurar un servicio de datos de referencia | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: d0535fce-2bf5-4f6d-b517-ffe6fa13738d
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 23832b226bb9408ab4e5b2fbb50718e1ead710b4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48217295"
---
# <a name="task-9-configuring-a-reference-data-service"></a>Tarea 9: configurar un servicio de datos de referencia
  En esta tarea, configurará DQS para que use un servicio de datos de referencia de Windows Azure Marketplace. En la siguiente tarea, configurará la **validación de direcciones** dominio para usar este servicio. En tiempo de ejecución, durante la actividad de limpieza, DQS pasa los valores de dominios en el **validación de direcciones** dominio al servicio para la limpieza. Consulte [configurar DQS para utilizar datos de referencia](http://msdn.microsoft.com/library/hh213070.aspx) para obtener más detalles.  
  
1.  En la página principal de **cliente DQS**, en el **administración** panel, haga clic en **configuración**.  
  
2.  Asegúrese de que **datos de referencia** pestaña está activa.  
  
3.  En el **configuración de red** área, escriba los valores adecuados en el **servidor Proxy** y **puerto** campos si necesita usar un servidor proxy para conectarse a Internet.  
  
4.  Tipo de su **clave de cuenta de Windows Azure Marketplace** para el **Id. de cuenta de DataMarket** campo.  
  
     ![Cuenta de servicio de datos de referencia de mercado de datos de Azure](../../2014/tutorials/media/et-configuringareferencedataservice.jpg "cuenta de servicio de datos de referencia de mercado de datos de Azure")  
  
5.  Haga clic en **validar** situado junto al cuadro de texto para validar el identificador de cuenta.  
  
6.  Haga clic en **Aceptar** en el cuadro de mensaje.  
  
7.  Haga clic en **cerrar** en la parte inferior de la página para cambiar a la página principal del cliente de DQS.  
  
## <a name="next-task"></a>Tarea siguiente  
 [Tarea 10: Configurar un dominio compuesto para que use un servicio de datos de referencia](../../2014/tutorials/task-10-configuring-composite-domain-to-use-reference-data-service.md)  
  
  
