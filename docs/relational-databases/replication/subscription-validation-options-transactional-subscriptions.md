---
title: "Opciones de validación de suscripciones (suscripciones transaccionales) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.validate.options.f1
helpviewer_keywords:
- Subscription Validation Options dialog box
ms.assetid: fd66ad1f-df01-4240-9e89-8f41bff12c1e
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: da21a38bf0797bf5368ddba1d1c2a47824bad369
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

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
 [Validar datos en el suscriptor](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [Validar datos replicados](../../relational-databases/replication/validate-replicated-data.md)  
  
  
