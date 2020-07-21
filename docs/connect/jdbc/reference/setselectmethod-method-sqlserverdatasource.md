---
title: Método setSelectMethod (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setSelectMethod
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7934276d-5ac9-4cbc-a2a0-2c65c93733ac
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7df9d7f066e9ddf076ba23b88c1d22b14d0f009d
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80925506"
---
# <a name="setselectmethod-method-sqlserverdatasource"></a>Método setSelectMethod (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el tipo de cursor predeterminado que se utiliza para todos los conjuntos de resultados que se crean con el objeto [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setSelectMethod(java.lang.String selectMethod)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *selectMethod*  
  
 Un valor **String** que contiene el tipo de cursor predeterminado.  
  
## <a name="remarks"></a>Observaciones  
 El cursor selectMethod es el tipo de cursor predeterminado que se utiliza en un conjunto de resultados. Esta propiedad es útil cuando se estén abordando grandes conjuntos de resultados y no se quiera almacenar el conjunto de resultados entero del lado cliente. Si se establece la propiedad en "cursor", podrá crear un cursor en el lado del servidor que puede capturar fragmentos más pequeños de cada vez. Si no se establece la propiedad selectMethod, el método [getSelectMethod](../../../connect/jdbc/reference/getselectmethod-method-sqlserverdatasource.md) devuelve el valor predeterminado "direct".  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
