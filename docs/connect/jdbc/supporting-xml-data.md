---
title: Compatibilidad con datos XML | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 32b7217e-1f0c-473d-9a45-176daa81584e
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d23e602f9e1323f96bc350d2501dccf6e06b03ca
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="supporting-xml-data"></a>Compatibilidad con datos XML
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Proporciona un **xml** tipo de datos que le permite almacenar documentos XML y fragmentos en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos. El **xml** tipo de datos es un tipo de datos integrado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]y es en cierta forma es similar a otros tipos integrados, como **int** y **varchar**. Al igual que otros tipos integrados, puede usar el **xml** como de tipo de datos: un tipo de variable, un tipo de parámetro, un tipo de valor devuelto de función o una columna de tipo cuando se crea una tabla; o en [!INCLUDE[tsql](../../includes/tsql_md.md)] funciones CAST y CONVERT. En el controlador JDBC, el **xml** se puede asignar el tipo de datos como una cadena, matriz de bytes, secuencia, objeto CLOB, BLOB o SQLXML. Cadena es la asignación predeterminada.  
  
 El controlador JDBC ofrece compatibilidad con la API de JDBC 4.0, que presenta la interfaz SQLXML. La interfaz SQLXML define métodos para interactuar con los datos XML y manipularlos. El **SQLXML** es un tipo de datos de JDBC 4.0 y se asigna a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **xml** tipo de datos. Por tanto, para usar el tipo de datos SQLXML en sus aplicaciones, debe establecer la ruta de clase para incluir el archivo sqljdbc4.jar. Si la aplicación intenta usar sqljdbc3.jar cuando obtiene acceso al objeto SQLXML y sus métodos, se devuelve una excepción.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] valida siempre los datos XML antes de almacenarlos en la columna de base de datos. Las aplicaciones pueden usar **SQLXML** tipo de datos, porque el controlador JDBC los asigna a la **xml** automáticamente al tipo de datos. El **SQLXML** soporte técnico está disponible en sqljdbc4.jar. Vea [requisitos del sistema para el controlador JDBC](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md) para obtener la lista de versiones JRE compatibles con la [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].  
  
 Los temas de esta sección describen la interfaz SQLXML y cómo programar en el **SQLXML** tipo de datos mediante los métodos de la API de JDBC.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Description|  
|-----------|-----------------|  
|[Interfaz SQLXML](../../connect/jdbc/sqlxml-interface.md)|Describe la interfaz SQLXML y sus métodos.|  
|[Programar con SQLXML](../../connect/jdbc/programming-with-sqlxml.md)|Describe cómo utilizar el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] métodos de la API para almacenar y recuperar datos XML en y desde una base de datos relacional con el **SQLXML** tipo de datos de Java. También contiene información acerca de los tipos de objetos SQLXML y proporciona una lista de las instrucciones y las limitaciones importantes cuando se usan objetos SQLXML.|  
  
## <a name="see-also"></a>Vea también  
 [Describir los tipos de datos del controlador JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
