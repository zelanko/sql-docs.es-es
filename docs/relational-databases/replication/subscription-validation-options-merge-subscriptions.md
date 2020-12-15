---
title: Opciones de validación de suscripciones (combinación)
description: Describe el cuadro de diálogo "Opciones de validación de suscripciones" en SQL Server Management Studio (SSMS).
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.validate.mergeoptions.f1
helpviewer_keywords:
- Subscription Validation Options dialog box
ms.assetid: 4958c4ab-2025-42ce-b836-6fb4e9e6f24d
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016
ms.openlocfilehash: 7552433c0c291fca53164bf5919e3dea3d23b4ec
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97406624"
---
# <a name="subscription-validation-options-merge-subscriptions"></a>Opciones de validación de suscripciones (Suscripciones de mezcla)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Use el cuadro de diálogo **Opciones de validación de suscripciones** para especificar si la validación debe utilizar solamente recuento de filas o recuento de filas y suma de comprobación binaria.  
  
## <a name="options"></a>Opciones  
 **Solo comprobar recuentos de filas**  
 Seleccione esta opción para validar si la tabla del suscriptor tiene el mismo número de filas que la tabla del publicador. Este método no valida si el contenido de las filas coincide. La validación del recuento de filas proporciona una idea sobre validación que puede ponerle al corriente de problemas con los datos.  
  
 **Comprobar los recuentos de filas y comparar las sumas de comprobación para comprobar los datos de las filas**  
 Además de llevar a cabo un recuento de filas en el publicador y en el suscriptor, se calcula una suma de comprobación de todos los datos utilizando el algoritmo binario de suma de comprobación. Si el número de filas da un error, no se lleva a cabo la suma de comprobación. Esta opción no es válida para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)].  
  
## <a name="see-also"></a>Consulte también  
 [Validar datos en el suscriptor](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [Validar datos replicados](../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  
