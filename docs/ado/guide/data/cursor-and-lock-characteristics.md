---
title: Cursor y las características de bloqueo | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- locks [ADO], characteristics
- adOpenDynamic [ADO]
- cursors [ADO], characteristics
ms.assetid: 459c29cb-4230-42bf-8cc2-f3132ccc7aba
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: be9f5c9576e92f2169af03ef27d61776ab65f735
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35271094"
---
# <a name="cursor-and-lock-characteristics"></a>Cursor y las características de bloqueo
Aunque las características de un cursor dependen de las capacidades del proveedor, las siguientes ventajas y desventajas normalmente se aplican a los distintos tipos de cursores y bloqueos.  
  
|Tipo de cursor o bloqueo|Ventajas|Inconvenientes|  
|-------------------------|----------------|-------------------|  
|**adOpenForwardOnly**|-Pocos requisitos de recursos|-No se puede desplazar hacia atrás<br />-No hay coincidencia de datos|  
|**adOpenStatic**|-Desplazable|-No hay coincidencia de datos|  
|**adOpenKeyset**|-Alguna coincidencia de datos<br />-Desplazable|-Mayores requisitos de recursos<br />-No está disponible en la situación sin conexión|  
|**adOpenDynamic**|-Simultaneidad de datos alta<br />-Desplazable|-Más altos requisitos de recursos<br />-No está disponible en la situación sin conexión|  
|**adLockReadOnly**|-Pocos requisitos de recursos<br />-Altamente escalable|: No puede actualizar mediante el cursor de datos|  
|**adLockBatchOptimistic**|: Las actualizaciones por lotes<br />: Permite escenarios desconectados<br />-Otros usuarios pueden tener acceso a datos|-Los datos se pueden cambiar por varios usuarios a la vez|  
|**adLockPessimistic**|-Los datos no se puede cambiar por otros usuarios bloqueado|-Impide que otros usuarios tengan acceso a los datos mientras están bloqueados|  
|**adLockOptimistic**|-Otros usuarios pueden tener acceso a datos|-Los datos se pueden cambiar por varios usuarios a la vez|
