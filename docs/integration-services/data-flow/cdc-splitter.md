---
title: Divisor CDC | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.cdcsplitter.f1
ms.assetid: 167bc5c6-fa36-439d-987c-b20acd1a77e2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 38a72f9628e621f5ed960a125800451badd180e6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65727144"
---
# <a name="cdc-splitter"></a>Divisor CDC

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  El divisor CDC divide un único flujo de filas de un flujo de datos de origen de CDC en varios flujos de datos para las operaciones de inserción, actualización y eliminación. El flujo de datos se divide según la columna obligatoria `__$operation` y sus valores estándar en las tablas de cambios de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
|Valor de la operación|Salida|Descripción|  
|------------------------|------------|-----------------|  
|1|DELETE|Fila eliminada|  
|2|Insert|Fila insertada (no está disponible cuando se usa el modo CDC **Neto con combinación** )|  
|3|Update|Fila antes de la actualización (disponible solo cuando se usa el modo CDC **Todo con los valores antiguos** )|  
|4|Update|Fila después de la actualización (sigue a la de antes de la actualización)|  
|5|Update|Fila de mezcla (solo disponible cuando se usa el modo CDC **Neto con combinación** )|  
|Otros|Error||  
  
 Puede usar el divisor para conectarse a los resultados predefinidos de INSERT, UPDATE, DELETE y UPDATE para un procesamiento posterior.  
  
 La transformación divisor CDC tiene una entrada normal y una salida de error.  
  
## <a name="error-handling"></a>Tratamiento de errores  
 La transformación divisor CDC tiene una salida de error. Las filas de entrada con un valor no válido de la columna $operation se consideran erróneas y se administran según la propiedad **ErrorRowDisposition** de la entrada.  
  
 La salida de error del componente incluye las columnas de salida siguientes:  
  
-   **Código de error**: establézcalo en 1.  
  
-   **Columna de error**: la columna de origen que produce el error (para los errores de conversión).  
  
-   **Columnas de fila de error**: las columnas de entrada de la fila que produjo el error.  
  
## <a name="configuring-the-cdc-splitter"></a>Configuración del divisor CDC  
 No hay propiedades configurables del divisor CDC.  
  
 Para obtener más información sobre cómo usar el divisor CDC, vea Componentes CDC para Microsoft SQL Server Integration Services.  
  
 El cuadro de diálogo **Editor avanzado** contiene las propiedades que se pueden establecer mediante programación.  
  
 Para abrir el cuadro de diálogo **Editor avanzado** :  
  
-   En la pantalla **Flujo de datos** del proyecto de [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] , haga clic con el botón secundario en el divisor CDC y seleccione **Mostrar editor avanzado**.  
  
## <a name="see-also"></a>Consulte también  
 [Dirigir el flujo CDC según el tipo de cambio](../../integration-services/data-flow/direct-the-cdc-stream-according-to-the-type-of-change.md)  
  
  
