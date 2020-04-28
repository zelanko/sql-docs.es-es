---
title: Tipos de datos admitidos de SQL Server y SSIS para dominios DQS
description: Describe los cuatro tipos de datos de los dominios de Data Quality Services (DQS) (Data, decimal, integer y String) en SQL Server.
ms.custom: seo-lt-2019
ms.date: 11/08/2011
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 4931143a-b84d-478b-9b45-174128d36ed3
author: swinarko
ms.author: sawinark
ms.openlocfilehash: cff5cf3a2a6095b79537571d63ee428c500789c6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "75558175"
---
# <a name="supported-sql-server-and-ssis-data-types-for-dqs-domains"></a>Tipos de datos admitidos de SQL Server y SSIS para dominios DQS

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Hay muchos tipos de datos en SQL Server y SQL Server Integration Services (SSIS), pero solo cuatro tipos de datos para dominios DQS: Date, Decimal, Integer y String. No todos los tipos de datos en SQL Server y SSIS se admiten en DQS. Solo puede asignar los datos de origen para un dominio DQS a fin de realizar actividades de calidad de datos únicamente si el tipo de datos de origen se admiten en DQS y coincide con el tipo de datos de dominio DQS. Este tema proporciona información acerca de los tipos de datos de SSIS y SQL Server que se admiten y están disponibles para asignar a cada uno de los cuatro tipos de dominio en DQS.  
  
> [!NOTE]  
>  En los archivos .xlsx y .xls, el tipo de datos de la columna de origen está determinado por el tipo de datos más frecuente de las ocho primeras filas. Si una celda no se ajusta a dicho tipo de datos, se le asignará un valor NULL. De igual modo, en los archivos .csv, el tipo de datos de la columna de origen está determinado por el tipo de datos más frecuente de las ocho primeras filas.  
  
##  <a name="supported-sql-server-data-types"></a><a name="SQLServer"></a>Tipos de datos de SQL Server admitidos 
 En la tabla siguiente se proporciona información acerca de los tipos de datos de SQL Server admitidos para cada tipo de datos de dominio DQS:  
  
|Tipo de datos de dominio DQS|Tipo de datos de SQL Server admitido|  
|--------------------------|------------------------------------|  
|Date|date|  
|Decimal|Decimal<br /><br /> FLOAT<br /><br /> money<br /><br /> NUMERIC<br /><br /> real<br /><br /> SMALLMONEY|  
|Entero|bigint<br /><br /> int<br /><br /> SMALLINT<br /><br /> TINYINT|  
|String|char<br /><br /> NCHAR<br /><br /> NVARCHAR<br /><br /> varchar|  
  
 El resto de los tipos de datos de SQL Server no se admiten en DQS. Para obtener información sobre todos los tipos de datos de SQL Server, vea [Tipos de datos &#40;Transact-SQL&#41;](../t-sql/data-types/data-types-transact-sql.md).  
  
##  <a name="supported-ssis-data-types"></a><a name="SSIS"></a>Tipos de datos de SSIS admitidos  
 En la tabla siguiente se proporciona información acerca de los tipos de datos de SSIS admitidos para cada tipo de datos de dominio DQS:  
  
|Tipo de datos de dominio DQS|Tipo de dato de SSIS admitido|  
|--------------------------|------------------------------|  
|Date|DT_DATE|  
|Decimal|DT_DECIMAL<br /><br /> DT_NUMERIC<br /><br /> DT_R4<br /><br /> DT_R8|  
|Entero|DT_I1<br /><br /> DT_I2<br /><br /> DT_I4<br /><br /> DT_I8<br /><br /> DT_U1<br /><br /> DT_U2<br /><br /> DT_U4<br /><br /> DT_U8|  
|String|DT_STR<br /><br /> DT_WSTR|  
  
 El resto de los tipos de datos de SSIS no se admiten en DQS. Para obtener información acerca de todos los tipos de datos SSIS, vea [Integration Services Data Types](../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="see-also"></a>Consulte también  
 [Administrar un dominio](../data-quality-services/managing-a-domain.md)  
  
  
