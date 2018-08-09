---
title: Ejemplos de tipos de datos SQLXML | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8f2ff25b-71fd-46d7-b6de-d656095d2aad
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 29dab6834b367d58f80471f920c7ab23d63fedae
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/02/2018
ms.locfileid: "39456709"
---
# <a name="sqlxml-data-type-sample"></a>Ejemplos de tipos de datos SQLXML

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

En esta aplicación de ejemplo de [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] se muestra cómo almacenar datos XML en una base de datos relacional, cómo recuperar datos XML desde una base de datos y cómo analizar datos XML con el tipo de datos **SQLXML** de Java.

Los ejemplos de código de esta sección usan un analizador Simple API for XML (SAX). SAX es un estándar desarrollado públicamente para el análisis basado en eventos de documentos XML. También proporciona una interfaz de programación de aplicaciones para trabajar con datos XML. Tenga en cuenta que las aplicaciones también pueden usar cualquier otro analizador XML, como Document Object Model (DOM), Streaming API for XML (StAX) o cualquier otro. 

Document Object Model (DOM) proporciona una representación programática de documentos, fragmentos, nodos y conjuntos de nodos XML. También proporciona una interfaz de programación de aplicaciones para trabajar con datos XML. Similarmente, Streaming API for XML (StAX) es una API basada en Java para análisis por extracciones de XML.

> [!IMPORTANT]  
> Para usar la API del analizador SAX, debe importar la implementación SAX estándar desde el paquete javax.xml.

El archivo de código de este ejemplo se denomina SqlXmlDataType.java y se encuentra en la siguiente ubicación:

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\datatypes
```

## <a name="requirements"></a>Requisitos

Para ejecutar esta aplicación de ejemplo, debe configurar la ruta de clase para que incluya el archivo sqljdbc4.jar. Si en la ruta de clase falta una entrada para sqljdbc4.jar, la aplicación de ejemplo genera la excepción común "Clase no encontrada". Para obtener más información sobre cómo establecer la ruta de clase, vea [con el controlador JDBC](../../../connect/jdbc/using-the-jdbc-driver.md).

Además, necesitará acceso a la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] para ejecutar esta aplicación de ejemplo.

## <a name="example"></a>Ejemplo

En el ejemplo siguiente, el código establece una conexión con la base de datos [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] y, después, llama al método createSampleTables.

El método createSampleTables quita las tablas de prueba, TestTable1 y TestTable2, si existen. Después, inserta dos filas en TestTable1.

Además, el código muestra incluye los tres métodos siguientes y una clase adicional, llamada ExampleContentHandler.

La clase ExampleContentHandler implementa un controlador de contenido personalizado, que define los métodos  para los eventos del analizador.

El método showGetters muestra cómo analizar los datos en el objeto SQLXML mediante SAX, ContentHandler y XMLReader. Primero, el ejemplo de código crea una instancia de un controlador de contenido personalizado, que es ExampleContentHandler. Después, crea y ejecuta una instrucción SQL que devuelve un conjunto de datos desde TestTable1. Después, el ejemplo de código obtiene un analizador SAX y analiza los datos XML.

El método showSetters muestra cómo establecer la columna **xml** mediante SAX, ContentHandler y ResultSet. Primero, crea un objeto SQLXML vacío mediante el método [createSQLXML](../../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) de la clase Connection. Después, obtiene una instancia de un controlador de contenido para escribir los datos en el objeto SQLXML. Después, el ejemplo de código escribe los datos en TestTable1. Finalmente, el código itera por las filas de datos que se encuentran en el conjunto de resultados y usa el método [getSQLXML](../../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md) para leer los datos XML.

El método showTransformer muestra cómo obtener un dato XML desde una tabla e insertarlo en otra utilizando SAX y Transformer. Primero, recupera el objeto SQLXML de origen desde TestTable1. Después, crea un objeto SQLXML de destino vacío mediante el método [createSQLXML](../../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) de la clase Connection. Después, actualiza el objeto SQLXML de destino y escribe los datos XML en TestTable2. Finalmente, el código de ejemplo itera por las filas de datos que se encuentran en el conjunto de resultados y usa el método [getSQLXML](../../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md) para leer los datos XML de TestTable2.

[!code[JDBC#UsingSQLXML1](../../../connect/jdbc/codesnippet/Java/sqlxml-data-type-sample_1.java)]

## <a name="see-also"></a>Ver también

[Trabajar con tipos de datos &#40;JDBC&#41;](../../../connect/jdbc/code-samples/working-with-data-types-jdbc.md)
