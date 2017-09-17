---
title: Elementos que se usan en instrucciones SQL | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], elements supported
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: 85777525-1555-4731-8309-63a464c6b43a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c29dcd40090a380c124a0c72b07d5993d4295829
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="elements-used-in-sql-statements"></a>Elementos que se usan en instrucciones SQL
Los elementos siguientes se usan en las instrucciones SQL indicadas anteriormente.  
  
## <a name="element"></a>Elemento  
 *identificador de la tabla de base* :: = *nombre definido por el usuario*  
  
 *nombre de la tabla de base de* :: = *identificador de la tabla de base*  
  
 *un valor booleano factor* :: = [NOT] *principal de un valor booleano*  
  
 *un valor booleano principal* :: = comparación*-predicado* &#124; ( *condición de búsqueda* )  
  
 *un valor booleano término* :: = *factor de un valor booleano* [AND *término de un valor booleano*]  
  
 *literal de cadena de caracteres* :: = "{*caracteres*}... ''. (*caracteres* es cualquier carácter del juego de caracteres del origen de datos del controlador. Para incluir un carácter de comilla literal (") en un literal de cadena de caracteres, use dos caracteres de comillas literal ['' '].)  
  
 *identificador de la columna* :: = *nombre definido por el usuario*  
  
 *nombre de la columna* :: = [*nombre de la tabla*.] *identificador de columna*  
  
 *operador de comparación* :: = < &#124; > &#124; \<= &#124; > = &#124; = &#124; <>  
  
 *predicado de comparación* :: = *expresión* expresión de operador de comparación  
  
 *tipo de datos* :: = *tipo de cadena de caracteres* (*tipo de cadena de caracteres* es cualquier tipo de datos para los que la columna "" DATA_TYPE"" en el conjunto de resultados devuelto por SQLGetTypeInfo es cualquier SQL_CHAR o SQL_VARCHAR.)  
  
 *dígitos* :: = 0 &#124; 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9  
  
 *¿parámetro dinámico* :: =?  
  
 *expresión* :: = término &#124; expresión {+ &#124; –} término  
  
 *factor* :: = [*+*&#124;* –*]*principal*  
  
 *valor de inserción* :: =  
  
 *parámetro dinámico*  
  
 &#124; *literal*  
  
 &#124; ES NULL  
  
 &#124; USUARIO  
  
 *letra* :: = *letras en minúscula caso &#124; superior mayúscula*  
  
 *literal* :: = *literal de cadena de caracteres*  
  
 *letras en minúscula caso* :: = un &#124; b &#124; c &#124; d &#124; e &#124; f &#124; g &#124; h &#124; i &#124; j &#124; k &#124; l &#124; m &#124; n &#124; o &#124; p &#124; q &#124; r &#124; s &#124; t &#124; u &#124; v &#124; cuan &#124; x &#124; y &#124; z  
  
 *cláusula ORDER by* :: = ORDER BY *especificación de ordenación* [, *especificación de ordenación*]...  
  
 *principal* :: = *nombre de columna*  
  
 &#124; *parámetro dinámico*  
  
 &#124; *literal*  
  
 &#124; ( *expresión* )  
  
 *condición de búsqueda* :: = *término booleano* [o *condición de búsqueda*]  
  
 *lista de selección* :: = \* &#124; *seleccione sublista* [, *seleccione sublista*]...  (*lista de selección* no puede contener parámetros.)  
  
 *Seleccione sublista* :: = *expresión*  
  
 *especificación de ordenación* :: = {*entero sin signo &#124; nombre de la columna*} [*ASC &#124; DESC*]  
  
 *identificador de tabla* :: = *nombre definido por el usuario*  
  
 *nombre de la tabla* :: = *identificador de tabla*  
  
 *referencia de tabla* :: = *nombre de la tabla*  
  
 *lista de referencias de tabla* :: = *referencia de tabla* [,*referencia de tabla*]...  
  
 *término* :: = *factor* &#124; *término* {\*&#124;* / *} *factor*  
  
 *entero sin signo* :: = {*dígitos*}  
  
 *superior mayúscula* :: = *A &#124; B &#124; C &#124; N &#124; E &#124; F &#124; G &#124; H &#124; &#124; J &#124; K &#124; L &#124; M &#124; N &#124; Co &#124; P &#124; Q &#124; R &#124; S &#124; T &#124; U &#124; V &#124; Cuan &#124; X &#124; Y &#124; Z*  
  
 *nombre definido por el usuario* :: = *letra*[*dígitos* &#124; *letra* &#124; *_*]...

