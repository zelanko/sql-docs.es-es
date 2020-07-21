---
title: Recuperar información de tipo de datos con SQLGetTypeInfo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL data types [ODBC], identifiers
- SQLGetTypeInfo function [ODBC], retrieving data type information
- retrieving data type information [ODBC]
- type identifiers [ODBC], SQL
- identifiers [ODBC], SQL type
- SQL type identifiers [ODBC]
ms.assetid: d4f8b152-ab9e-4d05-a720-d10a08a6df81
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4ec2bbba824eaf3d74133cf9754eca2593c9fb79
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300065"
---
# <a name="retrieving-data-type-information-with-sqlgettypeinfo"></a>Al recuperar la información de tipo de datos con SQLGetTypeInfo
Dado que las asignaciones de tipos de datos SQL subyacentes a identificadores de tipo ODBC son aproximadas, ODBC proporciona una función (**SQLGetTypeInfo**) a través de la cual un controlador puede describir por completo cada tipo de datos SQL en el origen de datos. Esta función devuelve un conjunto de resultados, cada fila de la que describe las características de un solo tipo de datos, como el nombre, el identificador de tipo, la precisión, la escala y la nulabilidad.  
  
 Esta información generalmente la usan las aplicaciones genéricas que permiten al usuario crear y modificar tablas. Estas aplicaciones llaman a **SQLGetTypeInfo** para recuperar la información del tipo de datos y, a continuación, presentar parte o la totalidad del usuario. Estas aplicaciones deben tener en cuenta dos cosas:  
  
-   Se puede asignar más de un tipo de datos SQL a un identificador de tipo único, lo que puede dificultar la determinación del tipo de datos que se va a utilizar. Para solucionar este motivo, el conjunto de resultados se ordena primero por el identificador de tipo y el segundo por la proximidad de la definición del identificador de tipo. Además, los tipos de datos definidos por el origen de datos tienen prioridad sobre los tipos de datos definidos por el usuario. Por ejemplo, supongamos que un origen de datos define los tipos de datos Integer y COUNTER para que sean iguales, salvo que el contador se incrementa automáticamente. Supongamos también que el tipo definido por el usuario WHOLENUM es un sinónimo de entero. Cada uno de estos tipos se asigna a SQL_INTEGER. En el conjunto de resultados **SQLGetTypeInfo** , el entero aparece primero, seguido de WHOLENUM y, a continuación, el contador. WHOLENUM aparece después de un entero porque está definido por el usuario, pero antes del contador porque coincide más estrechamente con la definición del identificador de tipo SQL_INTEGER.  
  
-   ODBC no define nombres de tipos de datos para usarlos en las instrucciones **CREATE TABLE** y **ALTER TABLE** . En su lugar, la aplicación debe usar el nombre devuelto en la columna TYPE_NAME del conjunto de resultados devuelto por **SQLGetTypeInfo**. La razón de esto es que aunque la mayoría de SQL no varía mucho en los DBMS, los nombres de tipo de datos varían enormemente. En lugar de forzar que los controladores analicen instrucciones SQL y reemplacen nombres de tipos de datos estándar por nombres de tipos de datos específicos de DBMS, ODBC requiere que las aplicaciones usen los nombres específicos del DBMS en primer lugar.  
  
 Tenga en cuenta que **SQLGetTypeInfo** no describe necesariamente todos los tipos de datos que puede encontrar una aplicación. En concreto, los conjuntos de resultados pueden contener tipos de datos no admitidos directamente por el origen de datos. Por ejemplo, ODBC define los tipos de datos de las columnas de los conjuntos de resultados devueltos por las funciones de catálogo y es posible que el origen de datos no admita estos tipos de datos. Para determinar las características de los tipos de datos de un conjunto de resultados, una aplicación llama a **SQLColAttribute**.
