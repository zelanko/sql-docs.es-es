---
title: Características de cursor y bloqueo | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- locks [ADO], characteristics
- adOpenDynamic [ADO]
- cursors [ADO], characteristics
ms.assetid: 459c29cb-4230-42bf-8cc2-f3132ccc7aba
author: rothja
ms.author: jroth
ms.openlocfilehash: 02f4be413ddcfc9215cdbf12142b883ade644f41
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761121"
---
# <a name="cursor-and-lock-characteristics"></a>Cursor y las características de bloqueo
Aunque las características de un cursor dependen de las capacidades del proveedor, las siguientes ventajas y desventajas suelen aplicarse a los distintos tipos de cursores y bloqueos.  
  
|Cursor o tipo de bloqueo|Ventajas|Desventajas|  
|-------------------------|----------------|-------------------|  
|**adOpenForwardOnly**|-Requisitos de recursos insuficientes|-No se puede desplazar hacia atrás<br />-Sin simultaneidad de datos|  
|**adOpenStatic**|-Desplazable|-Sin simultaneidad de datos|  
|**adOpenKeyset**|-Parte de la simultaneidad de datos<br />-Desplazable|-Requisitos de recursos más altos<br />-No disponible en escenario desconectado|  
|**adOpenDynamic**|-Simultaneidad de datos alta<br />-Desplazable|-Requisitos de recursos más altos<br />-No disponible en escenario desconectado|  
|**adLockReadOnly**|-Requisitos de recursos insuficientes<br />-Muy escalable|-Los datos no se pueden actualizar a través del cursor|  
|**adLockBatchOptimistic**|-Actualizaciones por lotes<br />-Permite escenarios desconectados<br />-Otros usuarios que pueden tener acceso a los datos|-Los datos pueden ser modificados por varios usuarios a la vez.|  
|**adLockPessimistic**|-Otros usuarios no pueden cambiar los datos mientras están bloqueados|-Impide que otros usuarios tengan acceso a los datos mientras están bloqueados|  
|**adLockOptimistic**|-Otros usuarios que pueden tener acceso a los datos|-Los datos pueden ser modificados por varios usuarios a la vez.|
