---
title: Sys.bandwidth_usage (base de datos de SQL Azure) | Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- bandwidth_usage
- sys.bandwidth_usage
- bandwidth_usage_TSQL
- sys.bandwidth_usage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.bandwidth_usage
- bandwidth_usage
ms.assetid: 43ed8435-f059-4907-b5c0-193a258b394a
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 046e9e651daeb2946538ff5ae269aaad27666fd0
ms.sourcegitcommit: 97340deee7e17288b5eec2fa275b01128f28e1b8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/30/2019
ms.locfileid: "55421312"
---
# <a name="sysbandwidthusage-azure-sql-database"></a>sys.bandwidth_usage (Azure SQL Database)

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

> [!NOTE]
> Esto se aplica únicamente a [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]V11.* *  
  
 Devuelve información sobre el ancho de banda de red utilizado por cada base de datos en un  **[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] servidor de base de datos de V11**,. Cada fila devuelta para una base de datos determinada resume una única dirección y clase de uso durante un período de una hora.  
  
 **Esto ha quedado obsoleto en un [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].**  
  
 El **sys.bandwidth_usage** vista contiene las siguientes columnas.  
  
|Column Name|Descripción|  
|-----------------|-----------------|  
|**time**|La hora a la que se utilizó el ancho de banda. Las filas de esta vista ofrecen información por horas. Por ejemplo, 2009-09-19 02:00:00.000 significa que el ancho de banda se consumió el 19 de septiembre de 2009 entre las 2:00 a. m. y las 3:00 a. m.|  
|**database_name**|El nombre de la base de datos que utilizó ancho de banda.|  
|**direction**|El tipo de ancho banda utilizado, que puede ser:<br /><br /> Entrada: Datos que se mueven a la [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br /> Salida: Datos que se mueven fuera de la [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
|**class**|La clase de ancho banda utilizada, que puede ser:<br />Interno: Datos que se mueven dentro de la plataforma Azure.<br />External: Datos que se mueven fuera de la plataforma Azure.<br /><br /> Se devuelve esta clase solamente si la base de datos está ocupada en una relación continua de copias entre las regiones ([!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)]). Si una base de datos no participa en una relación de copia continua, no se devuelven filas "Interlink". Para obtener más información, vea la sección “Comentarios” más adelante en este tema.|  
|**time_period**|El período de tiempo cuando se produjo el uso es pico o programarla. El valor Peak va en función de la región en la que se creó el servidor. Por ejemplo, si se creó un servidor en la región "US_Northwest”, las horas pico se definen como una hora comprendida entre las 10:00 a. m. y a las 06:00:00 p. m. PST.|  
|**Cantidad**|La cantidad de ancho banda consumido, en kilobytes (KB).|  
  
## <a name="permissions"></a>Permisos

 Esta vista solo está disponible en el **maestro** base de datos para el inicio de sesión de entidad de seguridad de nivel de servidor.  
  
## <a name="remarks"></a>Comentarios  
  
### <a name="external-and-internal-classes"></a>Clases externas e internas

 Para cada base de datos utilizada en un momento dado, el **sys.bandwidth_usage** vista devuelve las filas que muestran la clase y la dirección de uso de ancho de banda. En el ejemplo siguiente se muestran los datos que se pueden exponer para una base de datos determinada. En este ejemplo, el tiempo son las 17:00 2012-04-21: 00, que se produce durante el período de tiempo máximo. El nombre de base de datos es Db1. En este ejemplo, **sys.bandwidth_usage** ha devuelto una fila para las cuatro combinaciones de direcciones de entrada y salida y clases externas e internas, como sigue:  
  
|time|database_name|direction|class|time_period|quantity|  
|----------|--------------------|---------------|-----------|------------------|--------------|  
|2012-04-21 17:00:00|Db1|Ingress|External|Peak|66|  
|2012-04-21 17:00:00|Db1|Egress|External|Peak|741|  
|2012-04-21 17:00:00|Db1|Ingress|Internal|Peak|1052|  
|2012-04-21 17:00:00|Db1|Egress|Interno|Peak|3525|  
  
### <a name="interpreting-data-direction-for-includessgeodrincludesssgeodr-mdmd"></a>Interpretar la dirección de los datos para [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)]

 Para [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)], los datos de uso del ancho banda son visibles en la base de datos maestra lógica en ambos lados de una relación continua de copia. Por lo que debe interpretar la entrada y salida indicadores de dirección desde la perspectiva de las bases de datos que se están consultando. Por ejemplo, considere un flujo de replicación que transfiere 1 MB de datos del servidor de origen al de destino. En este caso, en el servidor de origen el 1MB se descontará datos enviados totales y en el servidor de destino, el 1MB se registra como datos recibidos.  
  
> [!NOTE]  
> La importación masiva de datos transferidos es del servidor de origen al de destino, en la dirección del flujo de datos de usuario. Sin embargo, algunas transferencias de datos se requieren en la otra dirección.  
