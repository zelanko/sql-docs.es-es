---
title: Validar guías de planes tras una actualización | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- plan guides [SQL Server], validating after upgrade
ms.assetid: a55ebd88-6f58-454d-b1c4-991b88add522
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: d325ac1d922956c92bd27eb099c655f72e5b2631
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53366417"
---
# <a name="validate-plan-guides-after-upgrade"></a>Validar guías de planes tras una actualización
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Se recomienda volver a evaluar y probar las definiciones de guías de plan al actualizar la aplicación a una nueva versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los requisitos de optimización del rendimiento y el comportamiento de la coincidencia de las guías de plan pueden cambiar. Aunque una guía de plan no válida no hará que una consulta provoque un error, el plan se compilada sin utilizar la guía de plan y posiblemente no sea la mejor opción. Después de actualizar una base de datos a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], es recomendable que realice las tareas siguientes:  
  
-   Valide las guías de plan existentes con la función [sys.fn_validate_plan_guide](../../relational-databases/system-functions/sys-fn-validate-plan-guide-transact-sql.md) .  
  
-   Utilice eventos extendido para supervisar los planes equivocados durante un cierto período de tiempo con el evento [Guía de plan incorrecta](../../relational-databases/event-classes/plan-guide-unsuccessful-event-class.md) .  
  
  
