---
title: Método STAT | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Stat
helpviewer_keywords:
- Stat method [ADO]
ms.assetid: 99a2b2d4-e6b1-4205-b011-72d024ea7240
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0538a3afae1e4c0bf4159d8ef6a42872f21ff6ed
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67916869"
---
# <a name="stat-method"></a>Stat (método)
Recupera información sobre un objeto de [flujo](../../../ado/reference/ado-api/stream-object-ado.md) .  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Long stream.Stat(StatStg, StatFlag)  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor **largo** que indica el estado de la operación.  
  
#### <a name="parameters"></a>Parámetros  
 *StatStg*  
 Una estructura STATSTG que se rellenará con información sobre la secuencia. La implementación del método **STAT** utilizada por el objeto de secuencia de ADO no rellena todos los campos de la estructura.  
  
 *StatFlag*  
 Especifica que este método no devuelve algunos de los miembros de la estructura STATSTG, con lo que se guarda una operación de asignación de memoria. Los valores se toman de la enumeración STATFLAG. La enumeración STATFLAG tiene dos valores  
  
|Constante|Value|  
|--------------|-----------|  
|STATFLAG_DEFAULT|0|  
|STATFLAG_NONAME|1|  
  
## <a name="remarks"></a>Observaciones  
 La versión del método STAT implementado para el objeto de secuencia de ADO rellena los campos siguientes de la estructura STATSTG:  
  
 *pwcsName*  
 Cadena que contiene el nombre de la secuencia, si hay una disponible y no se ha especificado el valor de StatFlag STATFLAG_NONAME.  
  
 *cbSize*  
 Especifica el tamaño en bytes de la secuencia o de la matriz de bytes.  
  
 *mtime*  
 Indica la hora de la última modificación de este almacenamiento, secuencia o matriz de bytes.  
  
 *ctime*  
 Indica la hora de creación de este almacenamiento, secuencia o matriz de bytes.  
  
 *atime*  
 Indica la hora del último acceso a este almacenamiento, secuencia o matriz de bytes.  
  
 Si se especifica STATFLAG_NONAME en el parámetro StatFlag, no se devuelve el nombre de la secuencia.  
  
 Si no se especificó STATFLAG_NONAME en el parámetro StatFlag y no hay ningún nombre disponible para la secuencia actual, este valor se E_NOTIMPL.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
