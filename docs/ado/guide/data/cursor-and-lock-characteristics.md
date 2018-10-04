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
manager: craigg
ms.openlocfilehash: a8507be55ae84a3a03fd75871106bc39e0631d89
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47678433"
---
# <a name="cursor-and-lock-characteristics"></a>Cursor y las características de bloqueo
Aunque las características de un cursor dependen de las capacidades del proveedor, las ventajas y desventajas siguientes generalmente se aplican a los distintos tipos de cursores y bloqueos.  
  
|Tipo de cursor o bloqueo|Ventajas|Inconvenientes|  
|-------------------------|----------------|-------------------|  
|**adOpenForwardOnly**|-Los requisitos de recursos baja|-No se puede desplazar hacia atrás<br />-No hay coincidencia de datos|  
|**adOpenStatic**|-Desplazable|-No hay coincidencia de datos|  
|**adOpenKeyset**|-Algunos simultaneidad de datos<br />-Desplazable|-Mayores requisitos de recursos<br />-No está disponible en el escenario sin conexión|  
|**adOpenDynamic**|-Simultaneidad de datos alta<br />-Desplazable|-Más altos requisitos de recursos<br />-No está disponible en el escenario sin conexión|  
|**adLockReadOnly**|-Los requisitos de recursos baja<br />-Altamente escalable|: No se puede actualizar a través de cursor de datos|  
|**adLockBatchOptimistic**|: Las actualizaciones por lotes<br />-Permite escenarios desconectados<br />-Otros usuarios pueden tener acceso a datos|-Los datos se pueden cambiar por varios usuarios a la vez|  
|**adLockPessimistic**|-Los datos no se puede cambiar por otros usuarios mientras bloqueado|-Impide que otros usuarios tengan acceso a datos bloqueado|  
|**adLockOptimistic**|-Otros usuarios pueden tener acceso a datos|-Los datos se pueden cambiar por varios usuarios a la vez|
