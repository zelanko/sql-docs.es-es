---
title: Contenedores de clases de Java de ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- class wrappers [ADO]
ms.assetid: 1fc09dc1-9e32-412e-9f43-b8eb8bb483ca
author: rothja
ms.author: jroth
ms.openlocfilehash: 485c53645387e5dafbe562442ec12503df0a6737
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760561"
---
# <a name="ado-java-class-wrappers"></a>Contenedores de clase Java de ADO
Este código declara una instancia del contenedor de clase de [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) de ADO y lo inicializa, todo en la misma línea de código. Además, declara variables para cada uno de los argumentos en el método [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) , especialmente para [LockType](../../../ado/reference/ado-api/locktype-property-ado.md) y [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) (porque Java no admite tipos enumerados). Se abre y se cierra el objeto de **conjunto de registros** . Establecer RS1 en NULL simplemente programa esa variable para que se libere cuando Java realiza su liberación sistemática y intermitente de objetos no utilizados.  
  
```java
public static void main( String args[])  
{  
   msado15._Recordset   Rs1 = new msado15.Recordset();  
   Variant Source     = new Variant( "SELECT * FROM Authors" );  
   Variant Connect    = new Variant( "DSN=AdoDemo;UID=admin;PWD=;" );  
   int     LockType   = msado15.CursorTypeEnum.adOpenForwardOnly;  
   int     CursorType = msado15.LockTypeEnum.adLockReadOnly;  
   int     Options    = -1;  
  
   Rs1.Open( Source, Connect, LockType,  CursorType, Options );  
   Rs1.Close();  
   Rs1 = null;  
  
   System.out.println( "Success!\n" );  
}  
```  
  
## <a name="see-also"></a>Consulte también  
 [Mediante el SDK de Microsoft para Java](../../../ado/guide/appendixes/using-the-microsoft-sdk-for-java.md)
