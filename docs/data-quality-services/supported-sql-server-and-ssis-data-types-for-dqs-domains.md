---
title: Compatibilidad con los tipos de datos en SQL Server y SSIS para dominios DQS | Microsoft Docs
ms.custom: 
ms.date: 11/08/2011
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: 
ms.component: data-quality-services
ms.reviewer: 
ms.suite: sql
ms.technology: data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4931143a-b84d-478b-9b45-174128d36ed3
caps.latest.revision: "7"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ef8b4bd18c917cf515c120d9f6164c8da7f28c78
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/19/2018
---
# <a name="supported-sql-server-and-ssis-data-types-for-dqs-domains"></a>Compatibilidad con los tipos de datos en SQL Server y SSIS para dominios DQS
  Hay muchos tipos de datos en SQL Server y SQL Server Integration Services (SSIS), pero solo cuatro tipos de datos para dominios DQS: Date, Decimal, Integer y String. No todos los tipos de datos en SQL Server y SSIS se admiten en DQS. Solo puede asignar los datos de origen para un dominio DQS a fin de realizar actividades de calidad de datos únicamente si el tipo de datos de origen se admiten en DQS y coincide con el tipo de datos de dominio DQS. Este tema proporciona información acerca de los tipos de datos de SSIS y SQL Server que se admiten y están disponibles para asignar a cada uno de los cuatro tipos de dominio en DQS.  
  
> [!NOTE]  
>  En los archivos .xlsx y .xls, el tipo de datos de la columna de origen está determinado por el tipo de datos más frecuente de las ocho primeras filas. Si una celda no se ajusta a dicho tipo de datos, se le asignará un valor NULL. De igual modo, en los archivos .csv, el tipo de datos de la columna de origen está determinado por el tipo de datos más frecuente de las ocho primeras filas.  
  
##  <a name="SQLServer"></a> Tipos de datos de SQL Server admitidos  
 En la tabla siguiente se proporciona información acerca de los tipos de datos de SQL Server admitidos para cada tipo de datos de dominio DQS:  
  
|Tipo de datos de dominio DQS|Tipo de datos de SQL Server admitido|  
|--------------------------|------------------------------------|  
|date|Date|  
|Decimal|Decimal<br /><br /> FLOAT<br /><br /> money<br /><br /> NUMERIC<br /><br /> REAL<br /><br /> SMALLMONEY|  
|Integer|BIGINT<br /><br /> INT<br /><br /> smallint<br /><br /> TINYINT|  
|String|char<br /><br /> NCHAR<br /><br /> NVARCHAR<br /><br /> varchar|  
  
 El resto de los tipos de datos de SQL Server no se admiten en DQS. Para obtener información sobre todos los tipos de datos de SQL Server, vea [Tipos de datos &#40;Transact-SQL&#41;](../t-sql/data-types/data-types-transact-sql.md).  
  
##  <a name="SSIS"></a> Tipos de datos de SSIS admitidos  
 En la tabla siguiente se proporciona información acerca de los tipos de datos de SSIS admitidos para cada tipo de datos de dominio DQS:  
  
|Tipo de datos de dominio DQS|Tipo de dato de SSIS admitido|  
|--------------------------|------------------------------|  
|date|DT_DATE|  
|Decimal|DT_DECIMAL<br /><br /> DT_NUMERIC<br /><br /> DT_R4<br /><br /> DT_R8|  
|Integer|DT_I1<br /><br /> DT_I2<br /><br /> DT_I4<br /><br /> DT_I8<br /><br /> DT_U1<br /><br /> DT_U2<br /><br /> DT_U4<br /><br /> DT_U8|  
|String|DT_STR<br /><br /> DT_WSTR|  
  
 El resto de los tipos de datos de SSIS no se admiten en DQS. Para obtener información acerca de todos los tipos de datos SSIS, vea [Integration Services Data Types](../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="see-also"></a>Ver también  
 [Administrar un dominio](../data-quality-services/managing-a-domain.md)  
  
  
