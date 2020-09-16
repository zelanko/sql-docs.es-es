---
description: Método setAsciiStream (java.lang.String, java.io.InputStream)
title: Método setAsciiStream para flujo de entrada | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: dc2caa44-9eb5-4ed8-a889-36148b50901d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2fef33d5b60bef1f26fde6711cf849d6fab7487f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88432577"
---
# <a name="setasciistream-method-javalangstring-javaioinputstream"></a>Método setAsciiStream (java.lang.String, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el parámetro designado en el flujo de entrada especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final void setAsciiStream(java.lang.String parameterName,  
                                java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *parameterName*  
  
 Objeto **String** que contiene el nombre del parámetro.  
  
 *x*  
  
 Un objeto InputStream.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método setAsciiStream especifica este método setAsciiStream en la interfaz java.sql.PreparedStatement.  
  
## <a name="see-also"></a>Consulte también  
 [setAsciiStream &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setasciistream-sqlservercallablestatement.md)   
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
