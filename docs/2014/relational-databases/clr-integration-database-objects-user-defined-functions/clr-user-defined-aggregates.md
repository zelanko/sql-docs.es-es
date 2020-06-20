---
title: Agregados definidos por el usuario CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- aggregate functions [CLR integration]
- custom aggregates [CLR integration]
- calculations [CLR integration]
- user-defined functions [CLR integration]
ms.assetid: bad9b7e8-5967-4afa-8dc8-6d840faf9372
author: rothja
ms.author: jroth
ms.openlocfilehash: d1ef5d07fe082d0eeb2c3484d6e99572d8fc80e5
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84954629"
---
# <a name="clr-user-defined-aggregates"></a>Agregados definidos por el usuario de CLR
  Las funciones de agregado realizan un cálculo en un conjunto de valores y devuelven un valor único. Tradicionalmente, [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo ha admitido funciones de agregado integradas, como `SUM` o `MAX` , que operan en un conjunto de valores escalares de entrada y generan un valor de agregado único a partir de ese conjunto. La integración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con Common Language Runtime (CLR) de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework permite ahora a los desarrolladores crear funciones de agregado personalizadas en código administrado y hacer que estas funciones estén accesibles para [!INCLUDE[tsql](../../includes/tsql-md.md)] u otro código administrado.  
  
 En la siguiente tabla se muestran los temas de esta sección.  
  
 [Requisitos para agregados definidos por el usuario de CLR](clr-user-defined-aggregates-requirements.md)  
 Proporciona información general sobre los requisitos para implementar funciones de agregado definidas por el usuario de CLR.  
  
 [Invocar funciones de agregado definidas por el usuario de CLR](clr-user-defined-aggregate-invoking-functions.md)  
 Explica cómo invocar los agregados definidos por el usuario.  
  
  
