---
title: Método getTrustStore (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- getTrustStore Method (SQLServerDataSource)
apilocation:
- getTrustStore Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 8f5850e4-8627-49a8-ba0e-b1f4014322a5
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 2af5dfa8b6f4fc5c509af26209962a246372bd3d
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66786097"
---
# <a name="gettruststore-method-sqlserverdatasource"></a>Método getTrustStore (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve la ruta de acceso (incluido el nombre de archivo) del archivo trustStore del certificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.lang.String getTrustStore()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor **String** que contiene la ruta de acceso (incluido el nombre de archivo) del archivo trustStore del certificado, o bien el valor NULL si no se ha establecido un valor.  
  
## <a name="remarks"></a>Notas  
 Si no se establece la propiedad trustStore, el método [getTrustStore](../../../connect/jdbc/reference/gettruststore-method-sqlserverdatasource.md) devuelve el valor NULL.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
