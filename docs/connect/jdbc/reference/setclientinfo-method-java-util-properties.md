---
title: Método setClientInfo (java.util.Properties) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b2a8ec0b-40a2-44d1-90d9-a810d4132e56
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a332f42c8193c851a33036af214ac31366986023
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "67974744"
---
# <a name="setclientinfo-method-javautilproperties"></a>Método setClientInfo (java.util.Properties)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el valor de las propiedades de información de cliente de la conexión.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setClientInfo (java.util.Properties properties)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *properties*  
  
 Un objeto Properties que contiene la lista de propiedades de información de cliente que se van a establecer.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método setClientInfo especifica este método setClientInfo en la interfaz java.sql.Connection.  
  
 El [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] no admite propiedades de información de cliente. Este método genera advertencias si el parámetro de entrada *properties* no hace referencia a un conjunto de propiedades vacías. Es decir, este método genera advertencias para las propiedades que desea establecer la aplicación. Las aplicaciones deberían utilizar el método [getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverconnection.md) de la clase [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) para recuperar cada advertencia.  
  
## <a name="see-also"></a>Consulte también  
 [Método setClientInfo &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/setclientinfo-method-sqlserverconnection.md)   
 [Miembros SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
