---
title: sqlsrv_get_config | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_get_config
apitype: NA
helpviewer_keywords:
- API Reference, sqlsrv_get_config
- sqlsrv_get_config
ms.assetid: ce2befc2-af98-45bb-8d41-60f1674dccfc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f94c20c8aa6cf603c6588586e072813682b2ce68
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992702"
---
# <a name="sqlsrvgetconfig"></a>sqlsrv_get_config
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Devuelve el valor actual de la configuración especificada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sqlsrv_get_config( string $setting )  
```  
  
#### <a name="parameters"></a>Parámetros  
*$setting*: la configuración para la que se devuelve el valor. Para obtener una lista de valores configurables, consulte [sqlsrv_configure](../../connect/php/sqlsrv-configure.md).  
  
## <a name="return-value"></a>Valor devuelto  
El valor de la configuración especificado mediante el parámetro *$setting* . Si se especifica una configuración no válida, se devuelve **False** y se agrega un error a la colección de errores.  
  
## <a name="remarks"></a>Notas  
Si **False** config **sqlsrv_get_config**, debe llamar a [sqlsrv_errors](../../connect/php/sqlsrv-errors.md) para determinar si se produjo un error o si **False** es el valor de la configuración especificada mediante el parámetro *$setting* .  
  
## <a name="see-also"></a>Consulte también  
[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  

[sqlsrv_configure](../../connect/php/sqlsrv-configure.md)  

[sqlsrv_errors](../../connect/php/sqlsrv-errors.md)  
  
