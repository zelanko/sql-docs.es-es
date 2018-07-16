---
title: Agregados definidos por el usuario CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: clr
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
ms.openlocfilehash: cbc2929f11b37d58745af6ca5b25bf34221b9478
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37352477"
---
# <a name="clr-user-defined-aggregates"></a>Agregados definidos por el usuario de CLR
  Las funciones de agregado realizan un cálculo sobre un conjunto de valores y devuelven un solo valor. Tradicionalmente, [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha admitido solo funciones de agregado integradas, como `SUM` o `MAX`, que operan en un conjunto valores escalares de entrada y generan un único valor agregado de dicho conjunto. La integración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con Common Language Runtime (CLR) de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework permite ahora a los desarrolladores crear funciones de agregado personalizadas en código administrado y hacer que estas funciones estén accesibles para [!INCLUDE[tsql](../../includes/tsql-md.md)] u otro código administrado.  
  
 En la siguiente tabla se muestran los temas de esta sección.  
  
 [Requisitos para agregados definidos por el usuario de CLR](clr-user-defined-aggregates-requirements.md)  
 Proporciona información general sobre los requisitos para implementar funciones de agregado definidas por el usuario de CLR.  
  
 [Invocar funciones de agregado definidas por el usuario de CLR](clr-user-defined-aggregate-invoking-functions.md)  
 Explica cómo invocar los agregados definidos por el usuario.  
  
  
