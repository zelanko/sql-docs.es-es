---
title: Método setCharacterStream (int, java.io.Reader) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b8d4e1f7-14fc-4590-af98-1eda30d2ca6d
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c8004a4bda2cb68beb619db852dbef083d84c7d7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="setcharacterstream-method-int-javaioreader"></a>Método setCharacterStream (int, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el parámetro designado para el objeto java.io.Reader especificado.  
  
> [!NOTE]  
>  Esta característica se incorpora a partir de la [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] versión 2.0 del controlador JDBC.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final void setCharacterStream(int parameterIndex,  
                              java.io.Reader reader)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *parameterIndex*  
  
 Un **int** que indica el número de parámetro.  
  
 *lector*  
  
 El objeto java.io.Reader que contiene los datos Unicode.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método setCharacterStream especificado por el método setCharacterStream en la interfaz java.sql.PreparedStatement.  
  
## <a name="see-also"></a>Vea también  
 [Método setCharacterStream &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setcharacterstream-method-sqlserverpreparedstatement.md)   
 [Miembros SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
