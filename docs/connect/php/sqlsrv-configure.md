---
title: sqlsrv_configure | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_configure
apitype: NA
helpviewer_keywords:
- sqlsrv_configure
- API Reference, sqlsrv_configure
ms.assetid: 9393f975-a4ef-4c50-b4dd-14892fc55cc9
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ae32c7693b724deec25c8d923e02cdf929e893ef
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66796976"
---
# <a name="sqlsrvconfigure"></a>sqlsrv_configure
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Cambia la configuración para el control de errores y las opciones de registro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sqlsrv_configure( string $setting, mixed $value )  
```  
  
#### <a name="parameters"></a>Parámetros  
*$setting*: el nombre del valor que se va a configurar. Consulte la tabla siguiente para obtener una lista de opciones.  
  
*$value*: el valor que se va a aplicar a la configuración especificada en el parámetro *$setting* . Los valores posibles para este parámetro dependen de la configuración especificada. En la siguiente tabla se incluyen las posibles combinaciones:  
  
|Configuración|Posibles valores para el parámetro $value (equivalente entero entre paréntesis)|Valor predeterminado|  
|-----------|------------------------------------------------------------------------------|-----------------|  
|ClientBufferMaxKBSize<sup>1</sup>|Un número no negativo hasta el límite de memoria PHP.<br /><br />No se permiten ni el cero ni los números negativos.|10240 KB|  
|LogSeverity<sup>2</sup>|SQLSRV_LOG_SEVERITY_ALL (-1)<br /><br />SQLSRV_LOG_SEVERITY_ERROR (1)<br /><br />SQLSRV_LOG_SEVERITY_NOTICE (4)<br /><br />SQLSRV_LOG_SEVERITY_WARNING (2)|SQLSRV_LOG_SEVERITY_ERROR (1)|  
|LogSubsystems<sup>2</sup>|SQLSRV_LOG_SYSTEM_ALL (-1)<br /><br />SQLSRV_LOG_SYSTEM_CONN (2)<br /><br />SQLSRV_LOG_SYSTEM_INIT (1)<br /><br />SQLSRV_LOG_SYSTEM_OFF (0)<br /><br />SQLSRV_LOG_SYSTEM_STMT (4)<br /><br />SQLSRV_LOG_SYSTEM_UTIL (8)|SQLSRV_LOG_SYSTEM_OFF (0)|  
|WarningsReturnAsErrors<sup>3</sup>|**true** (1) o **false** (0)|**true** (1)|  
  
## <a name="return-value"></a>Valor devuelto  
Si se llama a **sqlsrv_configure** con un valor o una configuración no compatibles, la función devuelve el valor **False**. De lo contrario, devuelve **True**.  
  
## <a name="remarks"></a>Notas  
1\) Para obtener más información sobre las consultas de cliente, vea [Cursor Types &#1;SQLSRV Driver&#40;](../../connect/php/cursor-types-sqlsrv-driver.md) (Tipos de cursor &#40;Controlador SQLSRV&#41;).  
  
2\) Para obtener más información sobre la actividad de registro, consulte [Logging Activity](../../connect/php/logging-activity.md) (Actividad de registro).  
  
3\) Para obtener más información sobre cómo configurar el control de errores y advertencias, vea [Cómo configurar el control de errores y advertencias con el controlador SQLSRV](../../connect/php/how-to-configure-error-and-warning-handling-using-the-sqlsrv-driver.md).  
  
## <a name="see-also"></a>Consulte también  
[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Programación de guía para los controladores de Microsoft para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md) 
  
