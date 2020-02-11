---
title: 'Tarea 9: configuración de un servicio de datos de referencia | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: d0535fce-2bf5-4f6d-b517-ffe6fa13738d
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: e4c756463c43ede8c6dae0cda0a184f0ec7f9956
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "70154932"
---
# <a name="task-9-configuring-a-reference-data-service"></a>Tarea 9: configurar un servicio de datos de referencia
  En esta tarea, se configura DQS para usar un servicio de datos de referencia en Azure Marketplace. En la tarea siguiente, configurará el dominio de **validación de direcciones** para utilizar este servicio. En tiempo de ejecución, durante la actividad de limpieza, DQS pasa los valores de los dominios del dominio de **validación de direcciones** al servicio para su limpieza. Vea [configurar DQS para usar datos de referencia](https://msdn.microsoft.com/library/hh213070.aspx) para obtener más detalles.  
  
1.  En la Página principal del **cliente DQS**, en el panel **Administración** , haga clic en **configuración**.  
  
2.  Asegúrese de que la pestaña **datos de referencia** está activa.  
  
3.  En el área **configuración de red** , escriba los valores adecuados en los campos **servidor proxy** y **Puerto** si necesita usar un servidor proxy para conectarse a Internet.  
  
4.  Escriba la **clave de la cuenta de Azure Marketplace** para el campo ID. de **cuenta de datamarket** .  
  
     ![Cuenta de servicio de datos de referencia de Azure Data Market](../../2014/tutorials/media/et-configuringareferencedataservice.jpg "Cuenta de servicio de datos de referencia de Azure Data Market")  
  
5.  Haga clic en el botón **validar** junto al cuadro de texto para validar el identificador de la cuenta.  
  
6.  Haga clic en **Aceptar** en el cuadro de mensaje.  
  
7.  Haga clic en **cerrar** en la parte inferior de la página para cambiar a la Página principal del cliente DQS.  
  
## <a name="next-task"></a>Tarea siguiente  
 [Tarea 10: configurar un dominio compuesto para que use un servicio de datos de referencia](../../2014/tutorials/task-10-configuring-composite-domain-to-use-reference-data-service.md)  
  
  
