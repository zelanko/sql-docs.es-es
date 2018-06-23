---
title: Agregados definidos por el usuario CLR | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: reference
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- aggregate functions [CLR integration]
- custom aggregates [CLR integration]
- calculations [CLR integration]
- user-defined functions [CLR integration]
ms.assetid: bad9b7e8-5967-4afa-8dc8-6d840faf9372
caps.latest.revision: 35
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 456e550022912fe2b1e344b82dc405cb648288ab
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2018
ms.locfileid: "35700656"
---
# <a name="clr-user-defined-aggregates"></a>Agregados definidos por el usuario de CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Las funciones de agregado realizan un cálculo sobre un conjunto de valores y devuelven un solo valor. Tradicionalmente, [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se admite solo funciones de agregado integradas, como **suma** o **MAX**, que funcionan en un conjunto de valores escalares de entrada y generar un único agregado valor de ese conjunto. La integración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con Common Language Runtime (CLR) de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework permite ahora a los desarrolladores crear funciones de agregado personalizadas en código administrado y hacer que estas funciones estén accesibles para [!INCLUDE[tsql](../../includes/tsql-md.md)] u otro código administrado.  
  
 En la siguiente tabla se muestran los temas de esta sección.  
  
 [Requisitos para agregados definidos por el usuario CLR](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates-requirements.md)  
 Proporciona información general sobre los requisitos para implementar funciones de agregado definidas por el usuario de CLR.  
  
 [Invocar funciones de agregado definidas por el usuario CLR](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregate-invoking-functions.md)  
 Explica cómo invocar los agregados definidos por el usuario.  
  
  
