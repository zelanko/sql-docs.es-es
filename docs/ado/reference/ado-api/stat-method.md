---
title: "Método Stat | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: _Stream::Stat
helpviewer_keywords: Stat method [ADO]
ms.assetid: 99a2b2d4-e6b1-4205-b011-72d024ea7240
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c33383de27f2685849034cec79c6b4589dfb0a79
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="stat-method"></a>Stat (método)
Recupera información sobre un [flujo](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Long stream.Stat(StatStg, StatFlag)  
```  
  
## <a name="return-value"></a>Valor devuelto  
 A **largo** valor que indica el estado de la operación.  
  
#### <a name="parameters"></a>Parámetros  
 *StatStg*  
 Estructura STATSTG que se rellenará con información sobre la secuencia. La implementación de la **Stat** método utilizado por el objeto de secuencia de ADO no rellena todos los campos de la estructura.  
  
 *StatFlag*  
 Especifica que este método no devuelve algunos de los miembros de la estructura STATSTG, evitando así una operación de asignación de memoria. Valores se toman de la enumeración STATFLAG. La enumeración STATFLAG tiene dos valores  
  
|Constante|Valor|  
|--------------|-----------|  
|STATFLAG_DEFAULT|0|  
|STATFLAG_NONAME|1|  
  
## <a name="remarks"></a>Comentarios  
 La versión del método Stat implementada para el objeto Stream de ADO rellena los campos siguientes de la estructura STATSTG:  
  
 *pwcsName*  
 No se especificó una cadena que contiene el nombre de la secuencia, si está disponible y el valor STATFLAG_NONAME de StatFlag.  
  
 *cbSize*  
 Especifica el tamaño en bytes de la secuencia o matriz de bytes.  
  
 *mtime*  
 Indica la última hora de modificación de este almacenamiento, secuencia o matriz de bytes.  
  
 *CTime*  
 Indica la hora de creación de este almacenamiento, secuencia o matriz de bytes.  
  
 *atime*  
 Indica la última hora de acceso de este almacenamiento, secuencia o matriz de bytes.  
  
 Si se especifica STATFLAG_NONAME en el parámetro StatFlag, no se devuelve el nombre de la secuencia.  
  
 Si no se especifica STATFLAG_NONAME en el parámetro StatFlag y no hay ningún nombre disponible para la secuencia actual, este valor será E_NOTIMPL.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
