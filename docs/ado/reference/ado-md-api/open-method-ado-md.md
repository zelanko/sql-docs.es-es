---
description: Open (método) (ADO MD)
title: Método Open (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Open
- Cellset::Open
helpviewer_keywords:
- Open method [ADO MD]
ms.assetid: a87d8080-a238-45e5-bc80-9a8625b3810f
author: rothja
ms.author: jroth
ms.openlocfilehash: 56d6a216b7d21723d84d374b09a9c0b8c6c4806b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440827"
---
# <a name="open-method-ado-md"></a>Open (método) (ADO MD)
Recupera los resultados de una consulta multidimensional y devuelve los resultados a un [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Cellset.Open Source, ActiveConnection  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Origen*  
 Opcional. Una **variante** que se evalúa como una consulta multidimensional válida, como una consulta de expresión multidimensional (MDX). El argumento de *origen* corresponde a la propiedad de [origen](../../../ado/reference/ado-md-api/source-property-ado-md.md) . Para obtener más información acerca de MDX, consulte la documentación del [OLE DB para el procesamiento analítico en línea (OLAP)](https://msdn.microsoft.com/8a7673c6-3ca1-4411-9f1e-adf1e47df4f3) en el SDK de Microsoft Data Access Components.  
  
 *ActiveConnection*  
 Opcional. Una **variante** que se evalúa como una cadena que especifica un nombre de variable de objeto de [conexión](../../../ado/reference/ado-api/connection-object-ado.md) ADO válido o una definición para una conexión. El argumento *ActiveConnection* especifica la conexión en la que se va a abrir el objeto [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) . Si pasa una definición de conexión para este argumento, ADO abrirá una nueva conexión con los parámetros especificados. El argumento *ActiveConnection* corresponde a la propiedad [ActiveConnection](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md) .  
  
## <a name="remarks"></a>Observaciones  
 El método **Open** genera un error si se omite cualquiera de sus parámetros y el valor de propiedad correspondiente no se ha establecido antes de intentar abrir el conjunto de **celdas**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de celdas (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de Cellset (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [Propiedad ActiveConnection (ADO MD)](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md)   
 [Método Close (ADO MD)](../../../ado/reference/ado-md-api/close-method-ado-md.md)   
 [Connection (objeto) (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Propiedad Source (ADO MD)](../../../ado/reference/ado-md-api/source-property-ado-md.md)   
 [State (propiedad) (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)
