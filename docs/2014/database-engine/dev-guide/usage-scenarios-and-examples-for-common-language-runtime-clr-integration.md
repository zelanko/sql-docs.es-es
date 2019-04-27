---
title: Escenarios de uso y ejemplos de integración de Common Language Runtime (CLR) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- scenarios [CLR integration]
- common language runtime [SQL Server], samples
- examples [CLR integration]
- sample applications [CLR integration]
- database objects [CLR integration], samples
- managed code [SQL Server], samples
ms.assetid: 33aac25f-abb4-4f29-af88-4a0dacd80ae7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3718a084211e7c3b2b7a14973e195a4b1c3b6b1a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62780728"
---
# <a name="usage-scenarios-and-examples-for-common-language-runtime-clr-integration"></a>Escenarios de uso y ejemplos para la integración de Common Language Runtime (CLR)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluye aplicaciones de ejemplo, ejemplos de paquete y numerosos ejemplos de código que se pueden usar para aprender las características de programación de la integración con Common Language Runtime (CLR).  
  
 Para proyectos de Visual Studio completados implementan estos ejemplos y materiales adicionales, visite [Microsoft SQL Server Community Projects & Samples de CodePlex](https://go.microsoft.com/fwlink/?LinkID=193935).  
  
|Name|Descripción|  
|----------|-----------------|  
|[Acceso a código nativo desde una UDF de CLR](../../../2014/database-engine/dev-guide/accessing-native-code-from-a-clr-udf.md)|Muestra cómo invocar una función en código C++ nativo (no administrado) desde una función definida por el usuario en un ensamblado, en la base de datos.|  
|[Ejemplo de parámetro de matriz](../../../2014/database-engine/dev-guide/array-parameter-sample.md)|Muestra cómo crear, actualizar o eliminar un conjunto de filas en una base de datos pasando una matriz de información desde un cliente a un procedimiento almacenado de integración con CLR en el servidor. Para ello se utiliza un UDT.|  
|[Ejemplo UDT para calendario fecha y hora](../../../2014/database-engine/dev-guide/calendar-aware-date-and-time-udt-sample.md)|Define dos UDT que proporcionan el tratamiento de fechas y horas para calendario.|  
|[Ejemplo de transacciones de CLR](../../../2014/database-engine/dev-guide/clr-transactions-sample.md)|Muestra el control de transacciones mediante el uso de las API administradas que se encuentran en el espacio de nombres System.Transactions.|  
|[Creación de contactos con CLR y XML](../../../2014/database-engine/dev-guide/contact-creation-using-clr-and-xml.md)|El ejemplo Contact para SQL Server proporciona algunas utilidades que forman un nivel adicional de funcionalidad sobre la base de datos de ejemplo AdventureWorks2012 básica. La primera utilidad crea registros de contacto para diversos tipos de personas involucradas en la base de datos AdventureWorks2012. La información de contacto se especifica utilizando XML y se pasa a un procedimiento almacenado basado en C# o VB para crear el XML y colocarlo en las tablas apropiadas con la base de datos.|  
|[Tipo moneda y función de conversión](../../../2014/database-engine/dev-guide/currency-type-and-conversion-function.md)|Define un tipo de datos Currency definido por el usuario utilizando C#.|  
|[Tratar objetos grandes con CLR](../../../2014/database-engine/dev-guide/handling-large-objects-using-clr.md)|Muestra la transferencia de objetos binarios grandes (LOB) entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y un sistema de archivos accesible para el servidor utilizando los procedimientos almacenados de CLR.|  
|[Ejemplo de Hola a todos preparado](../../../2014/database-engine/dev-guide/hello-world-ready-sample.md)|Muestra las operaciones básicas para crear, implementar y probar un procedimiento almacenado basado en la integración con CLR simple internacionalizado.|  
|[Ejemplo de Hola a todos](../../../2014/database-engine/dev-guide/hello-world-sample.md)|Muestra las operaciones básicas para crear, implementar y probar un procedimiento almacenado basado en la integración con CLR simple.|  
|[Ejemplo de acceso a datos en proceso](../../../2014/database-engine/dev-guide/in-process-data-access-sample.md)|Contiene varias funciones simples que muestran distintas características del proveedor de acceso a datos en proceso de CLR.|  
|[Ejemplo de conjunto de resultados](../../../2014/database-engine/dev-guide/result-set-sample.md)|Muestra cómo se ejecutan comandos mientras se leen resultados de una consulta sin abrir una nueva conexión y sin leer todos los resultados en la memoria.|  
|[Ejemplo de envío de conjunto de datos](../../../2014/database-engine/dev-guide/send-dataset-sample.md)|Muestra cómo devolver al cliente un objeto DataSet basado en ADO.NET dentro de un procedimiento almacenado basado en CLR del lado servidor en forma de conjunto de resultados.|  
|[Ejemplo de funciones de la utilidad String](../../../2014/database-engine/dev-guide/string-utility-functions-sample.md)|Contiene una función con valores de tabla (TVF) de transmisión de datos, escrita en Visual C# y Visual Basic, que divide una cadena separada por comas en una tabla con una columna.|  
|[Ejemplo de manipulación de cadenas que detectan caracteres complementarios](../../../2014/database-engine/dev-guide/supplementary-aware-string-manipulation-sample.md)|Muestra la implementación de cinco funciones de cadena [!INCLUDE[tsql](../../includes/tsql-md.md)] que detectan caracteres complementarios que pueden tratar tanto cadenas Unicode como cadenas suplentes.|  
|[Utilidades UDT](../../../2014/database-engine/dev-guide/udt-utilities.md)|Contiene varias funciones de utilidad de tipo de datos definido por el usuario (UDT).|  
|[Limpieza del ensamblado sin usar](../../../2014/database-engine/dev-guide/unused-assembly-cleanup.md)|Contiene un procedimiento almacenado de .NET que elimina los ensamblados no usados en la base de datos actual consultando los catálogos de metadatos.|  
|[Tipo definido por el usuario](../../../2014/database-engine/dev-guide/user-defined-type.md)|Muestra la creación y el uso de un UDT simple desde [!INCLUDE[tsql](../../includes/tsql-md.md)] y desde una aplicación cliente mediante System.Data.SqlClient.|  
|[UTF8 Tipo de datos definido por el usuario de la cadena &#40;UDT&#41;](../../../2014/database-engine/dev-guide/utf8-string-user-defined-data-type-udt.md)|Muestra la implementación de un UDT que amplía el sistema de tipos de la base de datos para proporcionar almacenamiento para valores de codificación UTF8.|  
  
  
