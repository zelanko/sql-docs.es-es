---
title: Gramática de forma formal | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO], shape grammar
- data shaping [ADO], shape grammar
ms.assetid: ea691475-0f03-4abe-a785-b77e77712d1d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 91bdf0cfbfe87075d2c9484bca7edd835a950ee6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67925347"
---
# <a name="formal-shape-grammar"></a>Gramática formal de forma
Esta es la gramática formal para crear cualquier comando de forma:  
  
-   Los términos gramaticales necesarios son cadenas de texto delimitadas por corchetes angulares ("<>").  
  
-   Los términos opcionales están delimitados por corchetes ("[]").  
  
-   Las alternativas se indican mediante un inversa ("&#124;").  
  
-   Las alternativas repetidas se indican mediante puntos suspensivos ("...").  
  
-   *Alpha* indica una cadena de letras en orden alfabético.  
  
-   *Digit* indica una cadena de números.  
  
-   *Unicode-digit* indica una cadena de dígitos Unicode.  
  
 Todos los demás términos son literales.  
  
|Término|Definición|  
|----------|----------------|  
|\<> de comandos de forma|FORMA [\<Table-exp> [[as] \<alias>]] [\<Shape-Action>]|  
|\<> de tabla-exp|{\<Provider-Command-Text>} &#124;<br /><br /> (\<> de comandos de forma) &#124;<br /><br /> TABLA \<entrecomillada: nombre> &#124;<br /><br /> \<nombre entre comillas>|  
|\<> de acción de forma|ANEXAr \<> &#124; de lista de campos con alias<br /><br /> CALCULAR \<aliased-Field-List> [por \<lista de campos>]|  
|\<> de lista de campos con alias|\<> de campo con alias [, \<campo con alias... >]|  
|\<> de campo con alias|\<Field-exp> [[AS] \<alias>]|  
|\<> de campo-exp|(\<relación-exp>) &#124;<br /><br /> \<calculado-exp> &#124;<br /><br /> \<> &#124; agregado-exp<br /><br /> \<New-exp>|  
|<relation_exp>|\<Table-exp> [[AS] \<alias>]<br /><br /> Relación \<relacional-Cond-List>|  
|\<> relación-Cond-List|\<relación-Cond> [, \<relación-Cond>...]|  
|\<relación-Cond>|\<nombre de campo> a \<> de referencia secundaria|  
|\<> de referencia secundaria|\<> &#124; de nombre de campo<br /><br /> PARÁMETRO \<param-Ref>|  
|\<parámetro-ref>|\<número>|  
|\<> de lista de campos|\<> de nombre de campo [ \<, nombre de campo>]|  
|\<> agregado-exp|SUM (\<Qualified-Field-Name>) &#124;<br /><br /> AVG (\<nombre de campo calificado>) &#124;<br /><br /> MIN (\<nombre de campo calificado>) &#124;<br /><br /> MAX (\<nombre de campo calificado>) &#124;<br /><br /> COUNT (\<alias calificado> &#124; \<nombre completo>) &#124;<br /><br /> STDEV (\<nombre de campo completo>) &#124;<br /><br /> ANY (\<Qualified-Field-Name>)|  
|\<calculado-exp>|CALC (\<expresión>)|  
|\<nombre de campo completo>|\<alias>.[\<alias>...]\<field-name>|  
|\<alias>|\<nombre entre comillas>|  
|\<> de nombre de campo|\<nombre entre comillas> [[AS \<] alias>]|  
|\<nombre entre comillas>|"\<String>" &#124;<br /><br /> '\<String> ' &#124;<br /><br /> [\<String>] &#124;<br /><br /> \<nombre>|  
|\<nombre completo>|alias [. alias...]|  
|\<nombre>|Alpha [alfa &#124; digit &#124; _ &#124; # &#124;: &#124;...]|  
|\<número>|dígito [dígito...]|  
|\<New-exp>|NUEVO \<> de tipo de campo [\<(número> [ \<, número>])]|  
|\<> de tipo de campo|Un tipo de datos OLE DB o ADO.|  
|\<> de cadena|Unicode-Char [Unicode-Char...]|  
|\<> de expresiones|Visual Basic para Aplicaciones expresión cuyos operandos son otras columnas que no son de cálculo en la misma fila.|  
  
## <a name="see-also"></a>Consulte también  
 [Obtener acceso a las filas de un conjunto de registros jerárquico](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [Información general sobre la forma de datos](../../../ado/guide/data/data-shaping-overview.md)   
 [Proveedores necesarios para el modelado de datos](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Cláusula APPEND de forma](../../../ado/guide/data/shape-append-clause.md)   
 [Comandos Shape en general](../../../ado/guide/data/shape-commands-in-general.md)   
 [Shape Compute (cláusula)](../../../ado/guide/data/shape-compute-clause.md)   
 [Visual Basic para las funciones de aplicaciones](../../../ado/guide/data/visual-basic-for-applications-functions.md)
