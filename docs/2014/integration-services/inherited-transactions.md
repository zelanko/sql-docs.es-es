---
title: Transacciones heredadas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- transactions [Integration Services], inherited
- child packages
- inherited transactions [Integration Services]
ms.assetid: 90db5564-d41e-4cfe-8c9e-4e68d41eff1c
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 929624cf85f7146fa668632fa586a47caca743f0
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965475"
---
# <a name="inherited-transactions"></a>Transacciones heredadas
  Un paquete puede ejecutar otro paquete, utilizando la tarea Ejecutar paquete. El paquete secundario, que es el que ejecuta la tarea Ejecutar paquete, puede crear su propia transacción de paquete o heredar la del paquete primario.  
  
 Un paquete secundario hereda la transacción de paquete primario si se cumplen las dos condiciones siguientes:  
  
-   Una tarea Ejecutar paquete invoca al paquete.  
  
-   La tarea Ejecutar paquete que invocó al paquete también se combina con la transacción del paquete primario.  
  
 Los contenedores y tareas del paquete secundario no se pueden combinar con la transacción del paquete primario, a menos que el propio paquete secundario se combine con la transacción.  
  
## <a name="illustration-of-package-transactions"></a>Ilustración de transacciones de paquetes  
 En el diagrama siguiente, hay tres paquetes que utilizan transacciones. Cada paquete contiene varias tareas. Para resaltar el comportamiento de las transacciones, solo se muestran las tareas Ejecutar paquete. El paquete A ejecuta los paquetes B y C. A su vez, el paquete B ejecuta los paquetes D y E, y el paquete C ejecuta el paquete F.  
  
 Los paquetes y las tareas tienen los siguientes atributos de transacción:  
  
-   **TransactionOption** se establece en **Required** en los paquetes A y C  
  
-   **TransactionOption** se establece en **Supported** en los paquetes B y D, y en las tareas Ejecutar paquete B, Ejecutar paquete D y Ejecutar paquete F.  
  
-   **TransactionOption** se establece en **NotSupported** en el paquete E y en las tareas Ejecutar paquete C y Ejecutar paquete E.  
  
 ![Flujo de transacciones heredadas](media/mw-dts-executepack.gif "Flujo de transacciones heredadas")  
  
 Solo los paquetes B, D y F pueden heredar transacciones de sus paquetes primarios.  
  
 Los paquetes B y D heredan la transacción iniciada por el paquete A.   
  
 El paquete F hereda la transacción iniciada por el paquete C.  
  
 Los paquetes A y C controlan sus propias transacciones.  
  
 El paquete E no utiliza transacciones.  
  
## <a name="related-tasks"></a>Related Tasks  
 [Configurar un paquete para el uso de transacciones](../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
  
