---
title: Varias transacciones | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- transactions [Integration Services], multiple
- multiple transactions
ms.assetid: c3664a94-be89-40c0-a3a0-84b74a7fedbe
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: c98fa7454a1a01ee6879a514f369e6fb6c1a0570
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107278"
---
# <a name="multiple-transactions"></a>Varias transacciones
  Un paquete puede incluir transacciones no relacionadas en un paquete de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Cuando un contenedor situado en medio de una jerarquía de contenedores anidados no admite transacciones, los contenedores situados en un nivel superior o inferior de la jerarquía inician transacciones independientes, si están configurados para admitir transacciones. Las transacciones se confirman o se revierten en orden, desde la tarea más interna en la jerarquía de contenedores anidados hasta el paquete. Sin embargo, una vez confirmada la transacción interna, no se revierte aunque se anule una transacción externa.  
  
## <a name="illustration-of-multiple-transactions"></a>Ilustración de varias transacciones  
 Por ejemplo, un paquete tiene un contenedor de secuencias con dos contenedores de bucles Foreach y cada contenedor incluye dos tareas Ejecutar SQL. El contenedor de secuencias y las tareas Ejecutar SQL admiten transacciones, pero los contenedores de bucles Foreach no las admiten. En este ejemplo, cada tarea Ejecutar SQL iniciaría su propia transacción, que no se revertiría aunque se anulara la tarea de secuencia.  
  
 Las propiedades de TransactionOption del contenedor de secuencias, el contenedor de bucles Foreach y las tareas Ejecutar SQL se establecen de la siguiente forma:  
  
-   La propiedad TransactionOption del contenedor de secuencias se establece en **Required**.  
  
-   Las propiedades TransactionOption de los contenedores de bucles Foreach se establecen en **NotSupported**.  
  
-   Las propiedades de TransactionOption las tareas Ejecutar SQL se establecen en **Required**.  
  
 En el diagrama siguiente se muestran las cinco transacciones no relacionadas del paquete. El contenedor de secuencias inicia una transacción y las tareas Ejecutar SQL inician las otras cuatro.  
  
 ![Implementación de varias transacciones](media/mw-dts-trans2.gif "Implementation of multiple transactions")  
  
## <a name="related-tasks"></a>Related Tasks  
 [Configurar un paquete para que utilice transacciones](../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
  