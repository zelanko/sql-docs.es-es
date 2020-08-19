---
description: Gramática formal de forma
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 6a8d92abc3a1b0d7e6d39ac4149c186c5a2fc2eb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453377"
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
|\<shape-command>|FORMA [ \<table-exp> [[as] \<alias> ]] [ \<shape-action> ]|  
|\<table-exp>|{ \<provider-command-text> } &#124;<br /><br /> ( \<shape-command> ) &#124;<br /><br /> &#124; de tabla \<quoted-name><br /><br /> \<quoted-name>|  
|\<shape-action>|ANEXAr \<aliased-field-list> &#124;<br /><br /> Compute \<aliased-field-list> [by \<field-list> ]|  
|\<aliased-field-list>|\<aliased-field> [, \<aliased-field...>]|  
|\<aliased-field>|\<field-exp> [[AS] \<alias> ]|  
|\<field-exp>|( \<relation-exp> ) &#124;<br /><br /> \<calculated-exp> &#124;<br /><br /> \<aggregate-exp> &#124;<br /><br /> \<new-exp>|  
|<relation_exp>|\<table-exp> [[AS] \<alias> ]<br /><br /> TIENEN \<relation-cond-list>|  
|\<relation-cond-list>|\<relation-cond> [, \<relation-cond>...]|  
|\<relation-cond>|\<field-name> Para \<child-ref>|  
|\<child-ref>|\<field-name> &#124;<br /><br /> PARÁMETRO \<param-ref>|  
|\<param-ref>|\<number>|  
|\<field-list>|\<field-name> [, \<field-name>]|  
|\<aggregate-exp>|SUM ( \<qualified-field-name> ) &#124;<br /><br /> AVG ( \<qualified-field-name> ) &#124;<br /><br /> MIN ( \<qualified-field-name> ) &#124;<br /><br /> MAX ( \<qualified-field-name> ) &#124;<br /><br /> COUNT ( \<qualified-alias> &#124; \<qualified-name> ) &#124;<br /><br /> STDEV ( \<qualified-field-name> ) &#124;<br /><br /> ANY ( \<qualified-field-name> )|  
|\<calculated-exp>|CALC ( \<expression> )|  
|\<qualified-field-name>|\<alias>.[\<alias>...]\<field-name>|  
|\<alias>|\<quoted-name>|  
|\<field-name>|\<quoted-name> [[AS] \<alias> ]|  
|\<quoted-name>|" \<string> " &#124;<br /><br /> ' \<string> ' &#124;<br /><br /> [ \<string> ] &#124;<br /><br /> \<name>|  
|\<qualified-name>|alias [. alias...]|  
|\<name>|Alpha [alfa &#124; digit &#124; _ &#124; # &#124;: &#124;...]|  
|\<number>|dígito [dígito...]|  
|\<new-exp>|NUEVO \<field-type> [( \<number> [, \<number> ])]|  
|\<field-type>|Un tipo de datos OLE DB o ADO.|  
|\<string>|Unicode-Char [Unicode-Char...]|  
|\<expression>|Visual Basic para Aplicaciones expresión cuyos operandos son otras columnas que no son de cálculo en la misma fila.|  
  
## <a name="see-also"></a>Consulte también  
 [Obtener acceso a las filas de un conjunto de registros jerárquico](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [Información general sobre la forma de datos](../../../ado/guide/data/data-shaping-overview.md)   
 [Proveedores necesarios para el modelado de datos](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Cláusula APPEND de forma](../../../ado/guide/data/shape-append-clause.md)   
 [Comandos Shape en general](../../../ado/guide/data/shape-commands-in-general.md)   
 [Shape Compute (cláusula)](../../../ado/guide/data/shape-compute-clause.md)   
 [Visual Basic para las funciones de aplicaciones](../../../ado/guide/data/visual-basic-for-applications-functions.md)
