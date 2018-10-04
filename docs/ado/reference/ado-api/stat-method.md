---
title: Stat (método) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 127aab5e00247ce5550f25e2a281e190472b0186
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47828233"
---
# <a name="stat-method"></a>Stat (método)
Recupera información sobre un [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Long stream.Stat(StatStg, StatFlag)  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un **largo** valor que indica el estado de la operación.  
  
#### <a name="parameters"></a>Parámetros  
 *StatStg*  
 Una estructura STATSTG que se rellenará con información sobre la secuencia. La implementación de la **Stat** método utilizado por el objeto ADO Stream no rellene todos los campos de la estructura.  
  
 *StatFlag*  
 Especifica que este método no devuelve algunos de los miembros de la estructura STATSTG, ahorrando así una operación de asignación de memoria. Los valores se toman de la enumeración STATFLAG. La enumeración STATFLAG tiene dos valores  
  
|Constante|Valor|  
|--------------|-----------|  
|STATFLAG_DEFAULT|0|  
|STATFLAG_NONAME|1|  
  
## <a name="remarks"></a>Comentarios  
 La versión del método Stat implementada para el objeto Stream de ADO rellena los campos siguientes de la estructura STATSTG:  
  
 *pwcsName*  
 No se especificó una cadena que contiene el nombre de la secuencia, si está disponible y el valor de StatFlag STATFLAG_NONAME.  
  
 *cbSize*  
 Especifica el tamaño en bytes de la secuencia o matriz de bytes.  
  
 *mtime*  
 Indica la última hora de modificación de este almacenamiento, secuencia o matriz de bytes.  
  
 *CTime*  
 Indica la hora de creación de este almacenamiento, secuencia o matriz de bytes.  
  
 *atime*  
 Indica la última hora de acceso a este almacenamiento, secuencia o matriz de bytes.  
  
 Si se especifica STATFLAG_NONAME en el parámetro StatFlag, no se devuelve el nombre de la secuencia.  
  
 Si no se especificó STATFLAG_NONAME en el parámetro StatFlag y hay ningún nombre de la secuencia actual, este valor será E_NOTIMPL.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
