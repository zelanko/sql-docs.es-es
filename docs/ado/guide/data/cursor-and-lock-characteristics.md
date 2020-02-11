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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c4d6f86539e1abc7ee74087b130e0186322346e8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67925677"
---
# <a name="cursor-and-lock-characteristics"></a>Cursor y las características de bloqueo
Aunque las características de un cursor dependen de las capacidades del proveedor, las siguientes ventajas y desventajas suelen aplicarse a los distintos tipos de cursores y bloqueos.  
  
|Cursor o tipo de bloqueo|Ventajas|Inconvenientes|  
|-------------------------|----------------|-------------------|  
|**adOpenForwardOnly**|-Requisitos de recursos insuficientes|-No se puede desplazar hacia atrás<br />-Sin simultaneidad de datos|  
|**adOpenStatic**|-Desplazable|-Sin simultaneidad de datos|  
|**adOpenKeyset**|-Parte de la simultaneidad de datos<br />-Desplazable|-Requisitos de recursos más altos<br />-No disponible en escenario desconectado|  
|**adOpenDynamic**|-Simultaneidad de datos alta<br />-Desplazable|-Requisitos de recursos más altos<br />-No disponible en escenario desconectado|  
|**adLockReadOnly**|-Requisitos de recursos insuficientes<br />-Muy escalable|-Los datos no se pueden actualizar a través del cursor|  
|**adLockBatchOptimistic**|-Actualizaciones por lotes<br />-Permite escenarios desconectados<br />-Otros usuarios que pueden tener acceso a los datos|-Los datos pueden ser modificados por varios usuarios a la vez.|  
|**adLockPessimistic**|-Otros usuarios no pueden cambiar los datos mientras están bloqueados|-Impide que otros usuarios tengan acceso a los datos mientras están bloqueados|  
|**adLockOptimistic**|-Otros usuarios que pueden tener acceso a los datos|-Los datos pueden ser modificados por varios usuarios a la vez.|
