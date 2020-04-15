---
title: Recuperación de la información del tipo de datos con SQLGetTypeInfo Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300065"
---
# <a name="retrieving-data-type-information-with-sqlgettypeinfo"></a>Al recuperar la información de tipo de datos con SQLGetTypeInfo
Dado que las asignaciones de tipos de datos SQL subyacentes a identificadores de tipo ODBC son aproximadas, ODBC proporciona una función (**SQLGetTypeInfo**) a través de la cual un controlador puede describir completamente cada tipo de datos SQL en el origen de datos. Esta función devuelve un conjunto de resultados, cada fila de la que describe las características de un único tipo de datos, como nombre, identificador de tipo, precisión, escala y nulabilidad.  
  
 Esta información generalmente la utilizan las aplicaciones genéricas que permiten al usuario crear y modificar tablas. Estas aplicaciones llaman a **SQLGetTypeInfo** para recuperar la información de tipo de datos y, a continuación, presentar parte o la totalidad de ella al usuario. Estas aplicaciones deben ser conscientes de dos cosas:  
  
-   Más de un tipo de datos SQL puede asignarse a un identificador de tipo único, lo que puede dificultar la determinación del tipo de datos que se va a usar. Para resolver esto, el conjunto de resultados se ordena primero por identificador de tipo y segundo por la cercanía a la definición del identificador de tipo. Además, los tipos de datos definidos por el origen de datos tienen prioridad sobre los tipos de datos definidos por el usuario. Por ejemplo, supongamos que un origen de datos define los tipos de datos INTEGER y COUNTER para que sean los mismos, excepto que COUNTER es el incremento automático. Supongamos también que el tipo definido por el usuario WHOLENUM es un sinónimo de INTEGER. Cada uno de estos tipos se asigna a SQL_INTEGER. En el conjunto de resultados **SQLGetTypeInfo,** INTEGER aparece primero, seguido de WHOLENUM y, a continuación, COUNTER. WHOLENUM aparece después de INTEGER porque está definido por el usuario, pero antes de COUNTER porque coincide más estrechamente con la definición del identificador de tipo SQL_INTEGER.  
  
-   ODBC no define nombres de tipo de datos para su uso en instrucciones **CREATE TABLE** y **ALTER TABLE.** En su lugar, la aplicación debe usar el nombre devuelto en la columna TYPE_NAME del conjunto de resultados devuelto por **SQLGetTypeInfo**. La razón de esto es que aunque la mayoría de SQL no varía mucho entre los DBMS, los nombres de tipo de datos varían enormemente. En lugar de obligar a los controladores a analizar instrucciones SQL y reemplazar nombres de tipo de datos estándar por nombres de tipo de datos específicos de DBMS, ODBC requiere que las aplicaciones usen los nombres específicos de DBMS en primer lugar.  
  
 Tenga en cuenta que **SQLGetTypeInfo** no describe necesariamente todos los tipos de datos que una aplicación puede encontrar. En particular, los conjuntos de resultados pueden contener tipos de datos no admitidos directamente por el origen de datos. Por ejemplo, ODBC define los tipos de datos de las columnas de los conjuntos de resultados devueltos por las funciones de catálogo y es posible que el origen de datos no admita estos tipos de datos. Para determinar las características de los tipos de datos de un conjunto de resultados, una aplicación llama a **SQLColAttribute**.
