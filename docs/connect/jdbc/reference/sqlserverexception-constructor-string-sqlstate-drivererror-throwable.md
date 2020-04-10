---
title: Constructor SQLServerException (java.lang.String, SQLState, DriverError, java.lang.Throwable) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7a9e235417b1a682156d775b8a3458d73eba9e95
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80902613"
---
# <a name="sqlserverexception-constructor-javalangstring-sqlstate-drivererror-javalangthrowable"></a>Constructor SQLServerException (java.lang.String, SQLState, DriverError, java.lang.Throwable)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Inicializa una nueva instancia de la clase [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) cuando se proporciona un objeto de **cadena**, un objeto **sqlstate**, un objeto **drivererror** y un objeto **iniciable**.

## <a name="syntax"></a>Sintaxis  
  
```  
public SQLServerException(java.lang.String errText,
            SQLState sqlState,
            DriverError driverError,
            java.lang.Throwable cause)
            
```  
  
#### <a name="parameters"></a>Parámetros  
 *errText*  
  
 Cadena que contiene el texto del error.
  
 *sqlState*  
  
 Objeto de enumeración que contiene el estado de SQL.
 
 *driverError*  
  
 Objeto de enumeración que contiene el error de controlador.
 
 *cause*  
  
 Objeto iniciable que contiene la causa de la excepción.
  
## <a name="see-also"></a>Consulte también  
 [Constructores SQLServerException](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [Miembros SQLServerException](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [Clase SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
