---
title: Contenedores de clase Java de ADO | Documentos de Microsoft
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 02/15/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- class wrappers [ADO]
ms.assetid: 1fc09dc1-9e32-412e-9f43-b8eb8bb483ca
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 08cbd288ba9f64816ae0c8fd62c18171967c4d0d
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="ado-java-class-wrappers"></a>Contenedores de clase Java de ADO
Este código declara una instancia de la propiedad ADO [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) contenedor de clase y lo inicializa, todo en la misma línea de código. Además, declara variables para cada uno de los argumentos de la [abiertos](../../../ado/reference/ado-api/open-method-ado-recordset.md) método, especialmente para [LockType](../../../ado/reference/ado-api/locktype-property-ado.md) y [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) (porque no es compatible con Java enumerado tipos). Se abre y cierra el **Recordset** objeto. Al establecer Rs1 en NULL simplemente programa esa variable se liberará cuando Java realice su liberación sistemática e intermitente de objetos no utilizados.  
  
```  
public static void main( String args[])  
{  
   msado15._Recordset   Rs1 = new msado15.Recordset();  
   Variant Source     = new Variant( "SELECT * FROM Authors" );  
   Variant Connect    = new Variant( "DSN=AdoDemo;UID=admin;PWD=;" );  
   int     LockType   = msado15.CursorTypeEnum.adOpenForwardOnly;  
   int     CursorType = msado15.LockTypeEnum.adLockReadOnly;  
   int     Options    = -1;  
  
   Rs1.Open( Source, Connect, LockType,  CursorType, Options );  
   Rs1.Close();  
   Rs1 = null;  
  
   System.out.println( "Success!\n" );  
}  
```  
  
## <a name="see-also"></a>Vea también  
 [Mediante el SDK de Microsoft para Java](../../../ado/guide/appendixes/using-the-microsoft-sdk-for-java.md)

