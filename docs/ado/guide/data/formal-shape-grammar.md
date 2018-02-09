---
title: "Gramática formal forma | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- shape commands [ADO], shape grammar
- data shaping [ADO], shape grammar
ms.assetid: ea691475-0f03-4abe-a785-b77e77712d1d
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f9eb99feba381701f7e590add3906cd0285b2720
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="formal-shape-grammar"></a>Gramática formal de forma
Se trata de la gramática formal para crear cualquier comando shape:  
  
-   Términos gramaticales necesarios son cadenas de texto delimitadas por corchetes angulares ("<>").  
  
-   Términos opcionales están delimitados por corchetes ("[]").  
  
-   Alternativas se indican mediante una barra vertical ("&#124;").  
  
-   Las alternativas extensibles se indican mediante un botón de puntos suspensivos ("...").  
  
-   *Alfa* indica una cadena de letras en orden alfabético.  
  
-   *Dígitos* indica una cadena de números.  
  
-   *Dígito de Unicode* indica una cadena de dígitos de unicode.  
  
 Todos los demás términos son literales.  
  
|Término|Definición|  
|----------|----------------|  
|\<shape-command>|SHAPE [\<table-exp> [[AS] \<alias>]][\<shape-action>]|  
|\<table-exp>|{\<provider-command-text>} &#124;<br /><br /> (\<shape-command>) &#124;<br /><br /> TABLA \<quoted-name > &#124;<br /><br /> \<quoted-name>|  
|\<acción de forma >|ANEXAR \<lista de campos de un alias > &#124;<br /><br /> COMPUTE \<aliased-field-list> [BY \<field-list>]|  
|\<aliased-field-list>|\<aliased-field> [, \<aliased-field...>]|  
|\<aliased-field>|\<field-exp> [[AS] \<alias>]|  
|\<field-exp>|(\<relación exp >) &#124;<br /><br /> \<calculated-exp> &#124;<br /><br /> \<exp agregado > &#124;<br /><br /> \<new-exp>|  
|<relation_exp>|\<table-exp> [[AS] \<alias>]<br /><br /> RELACIONAR \<relación-cond-list >|  
|\<relation-cond-list>|\<relation-cond> [, \<relation-cond>...]|  
|\<relation-cond>|\<field-name> TO \<child-ref>|  
|\<child-ref>|\<field-name> &#124;<br /><br /> PARÁMETRO \<ref de param >|  
|\<param-ref>|\<número >|  
|\<field-list>|\<field-name> [, \<field-name>]|  
|\<aggregate-exp>|SUM(\<qualified-field-name>) &#124;<br /><br /> AVG(\<qualified-field-name>) &#124;<br /><br /> MIN(\<qualified-field-name>) &#124;<br /><br /> MAX(\<qualified-field-name>) &#124;<br /><br /> COUNT(\<qualified-alias> &#124; \<qualified-name>) &#124;<br /><br /> STDEV(\<qualified-field-name>) &#124;<br /><br /> ANY(\<qualified-field-name>)|  
|\<calculated-exp>|CALC(\<expression>)|  
|\<qualified-field-name>|\<alias>.[\<alias>...]\<field-name>|  
|\<alias>|\<quoted-name>|  
|\<field-name>|\<quoted-name> [[AS] \<alias>]|  
|\<quoted-name>|"\<string>" &#124;<br /><br /> '\<string>' &#124;<br /><br /> [\<string>] &#124;<br /><br /> \<nombre >|  
|\<qualified-name>|alias[.alias...]|  
|\<nombre >|alfa [alpha &#124; dígito &#124; _ &#124; # &#124;: &#124;...]|  
|\<número >|dígito [dígitos...]|  
|\<new-exp>|NUEVA \<tipo de campo > [(\<número > [, \<número >])]|  
|\<field-type>|Un tipo de datos OLE DB o ADO.|  
|\<string>|unicode-char [unicode-char...]|  
|\<expresión >|Un Visual Basic para expresiones de las aplicaciones cuyos operandos son otras columnas no calculadas de la misma fila.|  
  
## <a name="see-also"></a>Vea también  
 [Acceso a las filas en un conjunto de registros jerárquico](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [Información general sobre la forma de datos](../../../ado/guide/data/data-shaping-overview.md)   
 [Proveedores deseados para dar forma a datos](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Cláusula APPEND Shape](../../../ado/guide/data/shape-append-clause.md)   
 [Comandos Shape en General](../../../ado/guide/data/shape-commands-in-general.md)   
 [Cláusula COMPUTE de forma](../../../ado/guide/data/shape-compute-clause.md)   
 [Visual Basic para las funciones de aplicaciones](../../../ado/guide/data/visual-basic-for-applications-functions.md)
