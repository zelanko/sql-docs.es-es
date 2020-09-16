---
description: Método updateNClob (int, java.io.Reader, long)
title: Método updateNClob (int, java.io.Reader, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 2bdbb539-0cb9-4047-98e3-7d6906af68f8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ff42e8389b3eeb74e8518787add914e7a1c8e1fa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88472065"
---
# <a name="updatenclob-method-int-javaioreader-long"></a>Método updateNClob (int, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Actualiza la columna designada mediante el objeto Reader especificado, cuya longitud queda establecida según el número de caracteres especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void updateNClob(int columnIndex,  
                        java.io.Reader reader,  
                        long length)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnIndex*  
  
 Valor **int** que indica el índice de la columna.  
  
 *reader*  
  
 Un objeto Reader.  
  
 *length*  
  
 El número de caracteres en los datos del parámetro.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método updateNClob especifica este método updateNClob en la interfaz java.sql.ResultSet.  
  
 Este método solo se admite en columnas **nvarchar (max)**, **ntext** y **xml**. Si se utiliza este método en cualquier otro tipo de datos, provocará una excepción.  
  
## <a name="see-also"></a>Consulte también  
 [Método updateNClob &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatenclob-method-sqlserverresultset.md)   
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
