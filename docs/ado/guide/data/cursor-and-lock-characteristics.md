---
title: Cursor y las características de bloqueo | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c4d6f86539e1abc7ee74087b130e0186322346e8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925677"
---
# <a name="cursor-and-lock-characteristics"></a>Cursor y las características de bloqueo
Aunque las características de un cursor dependen de las capacidades del proveedor, las ventajas y desventajas siguientes generalmente se aplican a los distintos tipos de cursores y bloqueos.  
  
|Tipo de cursor o bloqueo|Ventajas|Desventajas|  
|-------------------------|----------------|-------------------|  
|**adOpenForwardOnly**|-Los requisitos de recursos baja|-No se puede desplazar hacia atrás<br />-No hay coincidencia de datos|  
|**adOpenStatic**|-Desplazable|-No hay coincidencia de datos|  
|**adOpenKeyset**|-Algunos simultaneidad de datos<br />-Desplazable|-Mayores requisitos de recursos<br />-No está disponible en el escenario sin conexión|  
|**adOpenDynamic**|-Simultaneidad de datos alta<br />-Desplazable|-Más altos requisitos de recursos<br />-No está disponible en el escenario sin conexión|  
|**adLockReadOnly**|-Los requisitos de recursos baja<br />-Altamente escalable|: No se puede actualizar a través de cursor de datos|  
|**adLockBatchOptimistic**|: Las actualizaciones por lotes<br />-Permite escenarios desconectados<br />-Otros usuarios pueden tener acceso a datos|-Los datos se pueden cambiar por varios usuarios a la vez|  
|**adLockPessimistic**|-Los datos no se puede cambiar por otros usuarios mientras bloqueado|-Impide que otros usuarios tengan acceso a datos bloqueado|  
|**adLockOptimistic**|-Otros usuarios pueden tener acceso a datos|-Los datos se pueden cambiar por varios usuarios a la vez|
