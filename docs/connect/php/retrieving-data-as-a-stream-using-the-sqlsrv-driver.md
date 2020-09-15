---
description: Recuperación de datos como una secuencia con el controlador SQLSRV
title: Recuperación de datos como una secuencia con el controlador SQLSRV | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 17dc9129-04cd-430c-b5b3-82824116425d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cceb378b0571ff1fb6b3505abd1f6d8f4535a5cb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88414451"
---
# <a name="retrieving-data-as-a-stream-using-the-sqlsrv-driver"></a>Recuperación de datos como una secuencia con el controlador SQLSRV
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

La recuperación de datos como un flujo solo está disponible en el controlador SQLSRV de [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], pero no en el controlador PDO_SQLSRV.  
  
Los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] aprovechan las ventajas de las secuencias para recuperar grandes cantidades de datos. En los temas de esta sección se proporcionan detalles sobre cómo recuperar datos como una secuencia.  
  
En los pasos siguientes se resume cómo recuperar datos como una secuencia:  
  
1.  Prepare y ejecute una consulta de Transact-SQL con [sqlsrv_query](../../connect/php/sqlsrv-query.md), o bien la combinación de [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)/[sqlsrv_execute](../../connect/php/sqlsrv-execute.md).  
  
2.  Use [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md) para desplazarse a la siguiente fila del conjunto de resultados.  
  
3.  Use [sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md) para recuperar un campo de la fila. Especifique que los datos se recuperen como una secuencia mediante **SQLSRV_PHPTYPE_STREAM(<encoding>)** como tercer parámetro en la llamada a la función. En esta tabla se muestran las constantes que se utilizan para especificar las codificaciones y sus descripciones:  
  
    |Constante de SQLSRV|Descripción|  
    |-------------------|---------------|  
    |SQLSRV_ENC_BINARY|Los datos se devuelven del servidor como una secuencia de bytes sin procesar, sin que se realicen procesos de codificación o traducción.|  
    |SQLSRV_ENC_CHAR|Los datos se devuelven en caracteres de 8 bits tal y como se especifica en la página de códigos de la configuración regional de Windows del sistema. Los caracteres multibyte, o aquellos que no tengan una correspondencia con esta página de códigos, se sustituirán por un carácter de signo de interrogación de cierre (?) de un solo byte.|  
  
> [!NOTE]  
> Algunos tipos de datos se devuelven como secuencias de forma predeterminada. Para obtener más información, consulte [Default PHP Data Types](../../connect/php/default-php-data-types.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Descripción|  
|---------|---------------|  
|[Tipos de datos con compatibilidad con secuencias con el controlador SQLSRV](../../connect/php/data-types-with-stream-support-using-the-sqlsrv-driver.md)|Muestra los tipos de datos de SQL Server que se pueden recuperar como secuencias.|  
|[Procedimientos: Recuperación de datos de caracteres como secuencia mediante el controlador SQLSRV](../../connect/php/how-to-retrieve-character-data-as-a-stream-using-the-sqlsrv-driver.md)|Muestra cómo recuperar datos de caracteres como una secuencia.|  
|[Procedimientos: Recuperación de datos binarios como secuencia mediante el controlador SQLSRV](../../connect/php/how-to-retrieve-binary-data-as-a-stream-using-the-sqlsrv-driver.md)|Muestra cómo recuperar datos binarios como una secuencia.|  
  
## <a name="see-also"></a>Consulte también  
[Recuperación de datos](../../connect/php/retrieving-data.md)

[Constantes &#40;controladores de Microsoft para PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
  
