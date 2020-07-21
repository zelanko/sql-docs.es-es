---
title: Opciones de validación de suscripciones, cuadro de diálogo (transaccional)
description: Describe el cuadro de diálogo "Opciones de validación de suscripciones" para la replicación transaccional en SQL Server Management Studio (SSMS).
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.validate.options.f1
helpviewer_keywords:
- Subscription Validation Options dialog box
ms.assetid: fd66ad1f-df01-4240-9e89-8f41bff12c1e
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 390f82aeb965e6031682b524544e12c613518af7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85729307"
---
# <a name="subscription-validation-options-transactional-subscriptions"></a>Opciones de validación de suscripciones (suscripciones transaccionales)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../../includes/applies-to-version/sql-asdb.md)]
  Utilice el cuadro de diálogo **Opciones de validación de suscripciones** para especificar si la validación debe utilizar solo un número de fila o un número de fila y una suma de comprobación binaria. 

[!INCLUDE[azure-sql-db-replication-supportability-note](../../includes/azure-sql-db-replication-supportability-note.md)]
  
## <a name="options"></a>Opciones  
 **Comprobar que el suscriptor tiene el mismo número de filas de datos replicados que el publicador**  
 Seleccione el tipo de validación de número de fila que debe realizarse. Para publicaciones de Oracle, la única opción disponible es **Calcular un recuento de filas real consultando las tablas directamente**.  
  
 **Comparar las sumas de comprobación para comprobar los datos de las filas**  
 Además de llevar a cabo un recuento de filas en el publicador y en el suscriptor, se calcula una suma de comprobación de todos los datos utilizando el algoritmo binario de suma de comprobación. Si el número de filas da un error, no se lleva a cabo la suma de comprobación.  
  
 **Detener el Agente de distribución después de finalizar la validación**  
 De forma predeterminada, el Agente de distribución se ejecuta sin interrupción. Seleccione esta opción para detener el agente una vez realizada la validación. Esto permite comprobar si la validación ha sido correcta antes de continuar replicando datos en el suscriptor.  
  
## <a name="see-also"></a>Consulte también  
 [Validar datos en el suscriptor](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [Validar datos replicados](../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  
