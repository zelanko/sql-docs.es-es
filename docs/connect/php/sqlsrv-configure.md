---
title: sqlsrv_configure | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- sqlsrv_configure
apitype: NA
helpviewer_keywords:
- sqlsrv_configure
- API Reference, sqlsrv_configure
ms.assetid: 9393f975-a4ef-4c50-b4dd-14892fc55cc9
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ea82fe41ac7a95fbdf1907709a34ad57f8a82495
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
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
|ClientBufferMaxKBSize<sup>1</sup>|Un número no negativo hasta el límite de memoria PHP.<br /><br />Cero (0) significa que no hay límite en el tamaño de búfer.|10240|  
|LogSeverity<sup>2</sup>|SQLSRV_LOG_SEVERITY_ALL (-1)<br /><br />SQLSRV_LOG_SEVERITY_ERROR (1)<br /><br />SQLSRV_LOG_SEVERITY_NOTICE (4)<br /><br />SQLSRV_LOG_SEVERITY_WARNING (2)|SQLSRV_LOG_SEVERITY_ERROR (1)|  
|LogSubsystems<sup>2</sup>|SQLSRV_LOG_SYSTEM_ALL (-1)<br /><br />SQLSRV_LOG_SYSTEM_CONN (2)<br /><br />SQLSRV_LOG_SYSTEM_INIT (1)<br /><br />SQLSRV_LOG_SYSTEM_OFF (0)<br /><br />SQLSRV_LOG_SYSTEM_STMT (4)<br /><br />SQLSRV_LOG_SYSTEM_UTIL (8)|SQLSRV_LOG_SYSTEM_OFF (0)|  
|WarningsReturnAsErrors<sup>3</sup>|**True** (1) o **false** (0)|**true** (1)|  
  
## <a name="return-value"></a>Valor devuelto  
Si se llama a **sqlsrv_configure** con un valor o una configuración no compatibles, la función devuelve el valor **False**. De lo contrario, devuelve **True**.  
  
## <a name="remarks"></a>Comentarios  
(1) para obtener más información acerca de las consultas de cliente, consulte [tipos de Cursor &#40;controlador SQLSRV&#41;](../../connect/php/cursor-types-sqlsrv-driver.md).  
  
(2) para obtener más información acerca de la actividad de registro, consulte [Logging Activity](../../connect/php/logging-activity.md).  
  
(3) para obtener más información acerca de cómo configurar el control de errores y advertencia, consulte [Cómo: configurar el control de errores y advertencia con el controlador SQLSRV](../../connect/php/how-to-configure-error-and-warning-handling-using-the-sqlsrv-driver.md).  
  
## <a name="see-also"></a>Vea también  
[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Programación de guía para los controladores de Microsoft para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md) 
  
