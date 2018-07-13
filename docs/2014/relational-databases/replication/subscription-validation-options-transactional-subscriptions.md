---
title: Opciones de validación de suscripciones (suscripciones transaccionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.rep.validate.options.f1
helpviewer_keywords:
- Subscription Validation Options dialog box
ms.assetid: fd66ad1f-df01-4240-9e89-8f41bff12c1e
caps.latest.revision: 17
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 37fdbafa1f6dbdbc593277e4e5d4df37ad054d82
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37230665"
---
# <a name="subscription-validation-options-transactional-subscriptions"></a>Opciones de validación de suscripciones (suscripciones transaccionales)
  Utilice el cuadro de diálogo **Opciones de validación de suscripciones** para especificar si la validación debe utilizar solo un número de fila o un número de fila y una suma de comprobación binaria.  
  
## <a name="options"></a>Opciones  
 **Comprobar que el suscriptor tiene el mismo número de filas de datos replicados que el publicador**  
 Seleccione el tipo de validación de número de fila que debe realizarse. Para publicaciones de Oracle, la única opción disponible es **Calcular un recuento de filas real consultando las tablas directamente**.  
  
 **Comparar las sumas de comprobación para comprobar los datos de las filas**  
 Además de llevar a cabo un recuento de filas en el publicador y en el suscriptor, se calcula una suma de comprobación de todos los datos utilizando el algoritmo binario de suma de comprobación. Si el número de filas da un error, no se lleva a cabo la suma de comprobación.  
  
 **Detener el Agente de distribución después de finalizar la validación**  
 De forma predeterminada, el Agente de distribución se ejecuta sin interrupción. Seleccione esta opción para detener el agente una vez realizada la validación. Esto permite comprobar si la validación ha sido correcta antes de continuar replicando datos en el suscriptor.  
  
## <a name="see-also"></a>Vea también  
 [Validar datos en el suscriptor](validate-data-at-the-subscriber.md)   
 [Validar datos replicados](validate-replicated-data.md)  
  
  
