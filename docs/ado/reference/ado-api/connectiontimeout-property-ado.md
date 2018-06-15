---
title: Propiedad ConnectionTimeout (ADO) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::ConnectionTimeout
helpviewer_keywords:
- ConnectionTimeout property [ADO]
ms.assetid: 8904a403-1383-4b4b-b53d-5c01d6f5deac
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a1f90890b8f48a4a00fe9469ed978d42d3f6a86a
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35277014"
---
# <a name="connectiontimeout-property-ado"></a>Propiedad ConnectionTimeout (ADO)
Indica cuánto tiempo debe para esperar al establecer una conexión antes de terminar el intento y generar un error.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **largo** valor que indica, en segundos, cuánto tiempo debe para esperar para que se abra la conexión. Valor predeterminado es 15.  
  
## <a name="remarks"></a>Notas  
 Utilice la **ConnectionTimeout** propiedad en un [conexión](../../../ado/reference/ado-api/connection-object-ado.md) si retrasos frente al uso del servidor de tráfico o a la sobrecarga de red exijan abandonar un intento de conexión del objeto. Si el tiempo desde el **ConnectionTimeout** valor de la propiedad transcurre antes de la apertura de la conexión, se produce un error y ADO cancela el intento. Si establece la propiedad en cero, ADO esperará indefinidamente hasta que se abre la conexión. Asegúrese de que el proveedor al que está escribiendo código admite la **ConnectionTimeout** funcionalidad.  
  
 El **ConnectionTimeout** propiedad es de lectura/escritura cuando la conexión está cerrada y de solo lectura cuando se abre.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [ConnectionString, ConnectionTimeout y ejemplo de las propiedades de estado (VB)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [ConnectionString, ConnectionTimeout y ejemplo de las propiedades de estado (VC ++)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
 [CommandTimeout (propiedad, ADO)](../../../ado/reference/ado-api/commandtimeout-property-ado.md)
