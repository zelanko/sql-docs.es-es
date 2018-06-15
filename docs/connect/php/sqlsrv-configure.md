---
title: sqlsrv_configure | Documentos de Microsoft
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- sqlsrv_configure
apitype: NA
helpviewer_keywords:
- sqlsrv_configure
- API Reference, sqlsrv_configure
ms.assetid: 9393f975-a4ef-4c50-b4dd-14892fc55cc9
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fde39c9d64ec23e13c83c8c85a3de05c1417194a
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35308734"
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
|ClientBufferMaxKBSize<sup>1</sup>|Un número no negativo hasta el límite de memoria PHP.<br /><br />No se permiten números negativos y cero.|10240 KB|  
|LogSeverity<sup>2</sup>|SQLSRV_LOG_SEVERITY_ALL (-1)<br /><br />SQLSRV_LOG_SEVERITY_ERROR (1)<br /><br />SQLSRV_LOG_SEVERITY_NOTICE (4)<br /><br />SQLSRV_LOG_SEVERITY_WARNING (2)|SQLSRV_LOG_SEVERITY_ERROR (1)|  
|LogSubsystems<sup>2</sup>|SQLSRV_LOG_SYSTEM_ALL (-1)<br /><br />SQLSRV_LOG_SYSTEM_CONN (2)<br /><br />SQLSRV_LOG_SYSTEM_INIT (1)<br /><br />SQLSRV_LOG_SYSTEM_OFF (0)<br /><br />SQLSRV_LOG_SYSTEM_STMT (4)<br /><br />SQLSRV_LOG_SYSTEM_UTIL (8)|SQLSRV_LOG_SYSTEM_OFF (0)|  
|WarningsReturnAsErrors<sup>3</sup>|**True** (1) o **false** (0)|**True** (1)|  
  
## <a name="return-value"></a>Valor devuelto  
Si se llama a **sqlsrv_configure** con un valor o una configuración no compatibles, la función devuelve el valor **False**. De lo contrario, devuelve **True**.  
  
## <a name="remarks"></a>Notas  
(1) para obtener más información acerca de las consultas de cliente, consulte [tipos de Cursor &#40;controlador SQLSRV&#41;](../../connect/php/cursor-types-sqlsrv-driver.md).  
  
(2) para obtener más información acerca de la actividad de registro, consulte [Logging Activity](../../connect/php/logging-activity.md).  
  
(3) para obtener más información acerca de cómo configurar el control de errores y advertencia, consulte [Cómo: configurar el control de errores y advertencia con el controlador SQLSRV](../../connect/php/how-to-configure-error-and-warning-handling-using-the-sqlsrv-driver.md).  
  
## <a name="see-also"></a>Vea también  
[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Programación de guía para los controladores de Microsoft para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md) 
  
