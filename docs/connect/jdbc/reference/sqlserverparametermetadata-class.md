---
title: Clase SQLServerParameterMetaData | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 546290e0-9411-4a2b-aa36-61251e70e9cf
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b0721341cbf095e0aa27fab392c8d03f72dc2e3a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67970892"
---
# <a name="sqlserverparametermetadata-class"></a>Clase SQLServerParameterMetaData
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Representa los metadatos para los parámetros de instrucción preparados.  
  
 **Paquete:** com.microsoft.sqlserver.jdbc  
  
 **Extiende:** java.lang.Object  
  
 **Implementa:** java.sql.ParameterMetaData  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public class SQLServerParameterMetaData  
```  
  
## <a name="remarks"></a>Notas  
 Para recuperar los metadatos de parámetro, las instrucciones preparadas se ejecutan con SET FMT ONLY. Las instrucciones invocables llaman a sp_sproc_columns para recuperar nombres y metadatos para los parámetros de procedimiento.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [Referencia de API del controlador JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
