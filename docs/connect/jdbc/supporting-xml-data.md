---
title: Compatibilidad con datos XML | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 32b7217e-1f0c-473d-9a45-176daa81584e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 799b22cfac669846c606456f1911e27353a9ba9f
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "69027714"
---
# <a name="supporting-xml-data"></a>Compatibilidad con datos XML
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona un tipo de datos **xml** que permite almacenar documentos y fragmentos XML en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El tipo de datos **xml** es un tipo de datos integrado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y es de algún modo similar a otros tipos integrados, como **int** y **varchar**. Como sucede con otros tipos integrados, se puede usar el tipo de datos **xml** como: un tipo de variable, un tipo de parámetro, un tipo de valor devuelto de función o un tipo de columna cuando se crea una tabla, o bien en funciones CAST y CONVERT de [!INCLUDE[tsql](../../includes/tsql-md.md)]. En el controlador JDBC, el tipo de datos **xml** se puede asignar como una cadena, una matriz de bytes, un flujo o un objeto CLOB, BLOB o SQLXML. Cadena es la asignación predeterminada.  
  
 El controlador JDBC ofrece compatibilidad con la API de JDBC 4.0, que presenta la interfaz SQLXML. La interfaz SQLXML define métodos para interactuar con los datos XML y manipularlos. **SQLXML** es un tipo de datos de JDBC 4.0 y se asigna al tipo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]xml**de**. Por tanto, para usar el tipo de datos SQLXML en sus aplicaciones, debe establecer la ruta de clase para incluir el archivo sqljdbc4.jar. Si la aplicación intenta usar sqljdbc3.jar cuando obtiene acceso al objeto SQLXML y sus métodos, se devuelve una excepción.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] valida siempre los datos XML antes de almacenarlos en la columna de base de datos. Las aplicaciones pueden usar el tipo de datos **SQLXML**, ya que el controlador JDBC lo asigna automáticamente al tipo de datos **xml**. La compatibilidad de **SQLXML** está disponible en sqljdbc4.jar. Vea [Requisitos del sistema para el controlador JDBC](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md) para obtener la lista de versiones de JRE compatibles con [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].  
  
 En los temas de esta sección se describe la interfaz SQLXML y se explica cómo programar en el tipo de datos **SQLXML** con los métodos de la API de JDBC.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Interfaz SQLXML](../../connect/jdbc/sqlxml-interface.md)|Describe la interfaz SQLXML y sus métodos.|  
|[Programar con SQLXML](../../connect/jdbc/programming-with-sqlxml.md)|Describe cómo usar los métodos de la API de [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] para almacenar y recuperar datos XML en y desde una base de datos relacional con el tipo de datos **SQLXML** de Java. También contiene información acerca de los tipos de objetos SQLXML y proporciona una lista de las instrucciones y las limitaciones importantes cuando se usan objetos SQLXML.|  
  
## <a name="see-also"></a>Consulte también  
 [Descripción de los tipos de datos del controlador JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
