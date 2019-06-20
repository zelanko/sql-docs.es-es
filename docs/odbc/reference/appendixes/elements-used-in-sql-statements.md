---
title: Elementos que se usan en instrucciones SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], elements supported
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: 85777525-1555-4731-8309-63a464c6b43a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9e33beff29463172a26d53953dd5f563fe1f3f5c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63240960"
---
# <a name="elements-used-in-sql-statements"></a>Elementos que se usan en instrucciones SQL
Los elementos siguientes se usan en las instrucciones SQL mencionadas anteriormente.  
  
## <a name="element"></a>Elemento  
 *identificador de la tabla de base* :: = *nombre definido por el usuario*  
  
 *nombre de la tabla de base* :: = *identificador de la tabla de base*  
  
 *factor de booleano* :: = [NOT] *principal de un valor booleano*  
  
 *boolean-primary* ::= comparison *-predicate* &#124; ( *search-condition* )  
  
 *valor booleano término* :: = *factor de booleano* [AND *término de valor booleano*]  
  
 *character-string-literal* ::= ''{*character*}...'' (*carácter* es cualquier carácter del juego de caracteres del origen de datos del controlador. Para incluir un carácter de comilla literal (") en un literal de cadena de caracteres, use dos caracteres de comilla literal ['' '].)  
  
 *column-identifier* ::= *user-defined-name*  
  
 *nombre de columna* :: = [*nombre-tabla*.] *identificador de columna*  
  
 *comparison-operator* ::= < &#124; > &#124; \<= &#124; >= &#124; = &#124; <>  
  
 *predicado de comparación* :: = *expresión* expresión de operador de comparación  
  
 *tipo de datos* :: = *tipo de cadena de caracteres* (*tipo de cadena de caracteres* es cualquier tipo de datos para que la columna "" DATA_TYPE"" en el conjunto de resultados devuelto por SQLGetTypeInfo es cualquier SQL_CHAR o SQL_VARCHAR.)  
  
 *digit* ::= 0 &#124; 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9  
  
 *dynamic-parameter* ::= ?  
  
 *expresión* :: = término &#124; expresión {+&#124;-} término  
  
 *factor* :: = [*+*&#124;*-*]*principal*  
  
 *valor de inserción* :: =  
  
 *dynamic-parameter*  
  
 &#124; *literal*  
  
 &#124; NULL  
  
 &AMP;#124;USUARIO  
  
 *letter* ::= *lower-case-letter &#124; upper-case-letter*  
  
 *literal* ::= *character-string-literal*  
  
 *minúsculas caso letras* :: = un &#124; b &#124; c &#124; d. &#124; e &#124; f &#124; g &#124; h &#124; &#124; j &#124; k &#124; l &#124; m &#124; n &#124; o &#124; p &#124; q &#124; r &#124; s &#124; t &#124; u &#124; v &#124; w &#124; x &#124; y &#124; z  
  
 *cláusula ORDER by* :: = ORDER BY *especificación de ordenación* [, *especificación de ordenación*]...  
  
 *primary* ::= *column-name*  
  
 &#124; *dynamic-parameter*  
  
 &#124; *literal*  
  
 &#124; ( *expression* )  
  
 *condición de búsqueda* :: = *booleano término* [o *condición de búsqueda*]  
  
 *lista de selección* :: = \* &#124; *seleccione sublista* [, *seleccione sublista*]...  (*lista de selección* no puede contener parámetros.)  
  
 *select-sublist* ::= *expression*  
  
 *sort-specification* ::= {*unsigned-integer &#124; column-name*} [*ASC &#124; DESC*]  
  
 *table-identifier* ::= *user-defined-name*  
  
 *table-name* ::= *table-identifier*  
  
 *table-reference* ::= *table-name*  
  
 *lista de referencias de tabla* :: = *referencia de tabla* [,*referencia de tabla*]...  
  
 *term* ::= *factor* &#124; *term* {\*&#124;*/*} *factor*  
  
 *unsigned-integer* ::= {*digit*}  
  
 *superior minúscula* :: = *A &#124; B &#124; C &#124; d. &#124; E &#124; F &#124; G &#124; H &#124; me &#124; J &#124; K &#124; L &#124; M &#124; N &#124; O &#124; P &#124;Q &#124; R &#124; S &#124; T &#124; U &#124; V &#124; W &#124; X &#124; Y &#124; Z*  
  
 *user-defined-name* ::= *letter*[*digit* &#124; *letter* &#124; *_*]...
