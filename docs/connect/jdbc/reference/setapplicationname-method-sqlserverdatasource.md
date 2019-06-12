---
title: Método setApplicationName (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setApplicationName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 24d6e48d-53c4-4da2-a6de-1cdff463c9cd
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9f4c4707e06b25e1bb9e394c141f5fb1afa90599
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66765328"
---
# <a name="setapplicationname-method-sqlserverdatasource"></a>Método setApplicationName (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el nombre de la aplicación.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setApplicationName(java.lang.String applicationName)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *applicationName*  
  
 Objeto **String** que contiene el nombre de la aplicación.  
  
## <a name="remarks"></a>Notas  
 El nombre de la aplicación se usa para identificar la aplicación específica en diversas herramientas de creación de perfiles y registros de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Si no se establece el nombre de aplicación, el método getApplicationName devuelve la cadena no localizada "[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]".  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
