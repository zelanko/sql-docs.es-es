---
title: Elementos utilizados en las instrucciones SQL Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 49a1cd54957426d4d14d84d43df670c8c3d96189
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307026"
---
# <a name="elements-used-in-sql-statements"></a>Elementos que se usan en instrucciones SQL
Los siguientes elementos se utilizan en las instrucciones SQL enumeradas anteriormente.  
  
## <a name="element"></a>Elemento  
 *base-table-identifier* ::- *nombre definido por* el usuario  
  
 *base-table-name* ::- *base-table-identifier*  
  
 *factor booleano* :: [NOT] *booleano-primario*  
  
 *booleano-primario* ::- comparación *-predicate* &#124; ( *search-condition* )  
  
 *booleano-término* ::- *factor booleano* [Y *booleano-término*]  
  
 *carácter-cadena-literal* ::' '''*carácter*'...'' (*carácter* es cualquier carácter en el juego de caracteres del controlador/origen de datos. Para incluir un carácter de comillas literal ('') en un carácter-cadena-literal, utilice dos caracteres de comillas literales [''''].)  
  
 *identificador de columna* ::- *nombre definido por* el usuario  
  
 *nombre-columna* ::- [*nombre-tabla*.] *identificador de columna*  
  
 *comparison-operador* ::- \< < &#124; > &#124; , &#124; >, &#124;, &#124; <>  
  
 *comparison-predicate* ::- *expresión de expresión* comparison-operator expression expression  
  
 *tipo de datos* ::- *tipo de cadena-carácter* *(tipo de cadena de caracteres* es cualquier tipo de datos para el que la columna ""DATA_TYPE" del conjunto de resultados devuelto por SQLGetTypeInfo es SQL_CHAR o SQL_VARCHAR.)  
  
 *dígito* :: 0 &#124; 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9  
  
 *parámetro dinámico* ::? ?  
  
 *expresión* ::- Término &#124; expresión de&#124; - Término de&#124;  
  
 *factor* ::o*+* *-*[&#124;]*primaria*  
  
 *valor de inserción* ::  
  
 *parámetro dinámico*  
  
 &#124; *literal*  
  
 &#124; NULL  
  
 &#124; USUARIO  
  
 *letra* ::- *letra minúscula &#124; mayúscula-letra*  
  
 *literal* ::- *carácter-cadena-literal*  
  
 *letra inferior* :: a &#124; b &#124; c &#124; d &#124; e &#124; f f &#124; g &#124; h &#124; i &#124; j &#124; k &#124; &#124; m &#124; m &#124; n &#124; o p &#124; &#124; q &#124; r &#124; &#124; t &#124; u &#124; v &#124; &#124; x &#124; x y &#124; z  
  
 *orden-por-cláusula* ::-ORDER BY *sort-specification* [, *sort-specification*]...  
  
 *primaria* ::- *nombre-columna*  
  
 &#124; *parámetro dinámico*  
  
 &#124; *literal*  
  
 &#124; ( *expresión* )  
  
 *condición de búsqueda* :: - *término booleano* [OR *search-condition*]  
  
 *select-list* :: \* &#124; *select-sublist* [, *select-sublist*]...  (*select-list* no puede contener parámetros.)  
  
 *select-sublist* :: *expression*  
  
 *sort-specification* ::- -*unsigned-integer &#124; nombre-columna*? [*ASC &#124; DESC*]  
  
 *identificador de tabla* ::- *nombre definido por* el usuario  
  
 *nombre-tabla* ::- *identificador de tabla*  
  
 *referencia-tabla* ::- *nombre-tabla*  
  
 *table-reference-list* ::- *referencia-tabla* [,*referencia-tabla*]...  
  
 *término* ::- *factor* \* &#124; */* *término* -&#124;- *factor*  
  
 *unsigned-integer* ::- -*digitación*?  
  
 *letra* superior::A &#124; B &#124; C &#124; D &#124; E &#124; &#124; F &#124; G &#124; H &#124; I &#124; &#124; K &#124; *L &#124; M &#124; &#124; O &#124; P &#124; &#124; R &#124; S &#124; T &#124; U &#124; V &#124; W &#124; &#124; X y &#124; Z*  
  
 *nombre definido por el usuario* ::- *letra*[*dígito* &#124; *letra* &#124; *_*]...
