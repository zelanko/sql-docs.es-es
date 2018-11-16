---
title: Abrir (método) (ADO MD) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 091073431b3ff349b8ae107fcb6a37bfab94e46e
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2018
ms.locfileid: "51602785"
---
# <a name="open-method-ado-md"></a>Open (método) (ADO MD)
Recupera los resultados de una consulta multidimensional y devuelve los resultados a un [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Cellset.Open Source, ActiveConnection  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Source*  
 Opcional. Un **Variant** que se evalúa como una consulta multidimensional válida, por ejemplo, una consulta de expresiones multidimensionales (MDX). El *origen* argumento corresponde a la [origen](../../../ado/reference/ado-md-api/source-property-ado-md.md) propiedad. Para obtener más información acerca de MDX, vea el [OLE DB para OLAP Online Analytical Processing ()](https://msdn.microsoft.com/8a7673c6-3ca1-4411-9f1e-adf1e47df4f3) documentación en el SDK de Microsoft Data Access Components.  
  
 *ActiveConnection*  
 Opcional. Un **Variant** que se evalúa como una cadena que especifica un ADO válido [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto nombre de variable o una definición de una conexión. El *ActiveConnection* argumento especifica la conexión en el que se va a abrir el [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) objeto. Si se pasa una definición de conexión para este argumento, ADO abre una nueva conexión mediante los parámetros especificados. El *ActiveConnection* argumento corresponde a la [ActiveConnection](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md) propiedad.  
  
## <a name="remarks"></a>Comentarios  
 El **abrir** método genera un error si se omite cualquiera de sus parámetros y su correspondiente valor de propiedad no se ha establecido antes de intentar abrir el **Cellset**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de celdas (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de conjunto de celdas (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [ActiveConnection (propiedad, ADO MD)](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md)   
 [Close (método) (ADO MD)](../../../ado/reference/ado-md-api/close-method-ado-md.md)   
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Propiedad Source (ADO MD)](../../../ado/reference/ado-md-api/source-property-ado-md.md)   
 [State (propiedad) (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)
