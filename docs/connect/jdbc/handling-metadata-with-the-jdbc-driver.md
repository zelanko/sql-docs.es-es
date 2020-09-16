---
description: Control de metadatos con el controlador JDBC
title: Control de metadatos con el controlador JDBC | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5cfb35d4-ddcd-40a2-8091-f29cddc32552
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 633629005eef8e9a47f616637e646886666f2200
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438427"
---
# <a name="handling-metadata-with-the-jdbc-driver"></a>Control de metadatos con el controlador JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] se puede usar para trabajar con metadatos en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de distintos modos. El controlador JDBC se puede usar para obtener metadatos sobre la base de datos, un conjunto de resultados o los parámetros.  
  
 El controlador JDBC proporciona tres clases para recuperar metadatos de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md), que se usa para devolver información sobre la base de datos conectada.  
  
-   [SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md), que se usa para devolver información sobre el conjunto de resultados.  
  
-   [SQLServerParameterMetaData](../../connect/jdbc/reference/sqlserverparametermetadata-class.md), que se usa para devolver información sobre los parámetros de instrucciones preparadas e invocables.  
  
 En los temas de esta sección se describe el uso de cada una de estas tres clases de metadatos para poder trabajar con los metadatos en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Dado que el uso de los métodos de metadatos analizados en esta sección suele ser costoso por lo que respecta al rendimiento de la aplicación, se deben usar con precaución.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Empleo de metadatos de la base de datos](../../connect/jdbc/using-database-metadata.md)|Describe cómo recuperar información de metadatos sobre la base de datos conectada.|  
|[Empleo de metadatos del conjunto de resultados](../../connect/jdbc/using-result-set-metadata.md)|Describe cómo recuperar información de metadatos sobre el conjunto de resultados actual.|  
|[Empleo de metadatos del parámetro](../../connect/jdbc/using-parameter-metadata.md)|Describe cómo recuperar información de metadatos sobre los parámetros de las instrucciones preparadas e invocables.|  
  
## <a name="see-also"></a>Consulte también  
 [Introducción al controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
