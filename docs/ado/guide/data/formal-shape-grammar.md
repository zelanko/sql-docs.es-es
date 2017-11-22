---
title: "Gramática formal forma | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
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
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 48fb9c051deb490a2652bda4d8cd39be335c3270
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
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
|\<comando Shape >|FORMA [\<tabla exp > [[AS] \<alias >]] [\<forma Acción >]|  
|\<exp de tabla >|{\<texto de comando de proveedor >} &#124;<br /><br /> (\<comando shape >) &#124;<br /><br /> TABLA \<quoted-name > &#124;<br /><br /> \<QUOTED-name >|  
|\<acción de forma >|ANEXAR \<lista de campos de un alias > &#124;<br /><br /> PROCESO \<lista de campos de un alias > [BY \<lista de campos >]|  
|\<lista de campos de un alias >|\<campo de un alias > [, \<campos con alias... >]|  
|\<campo de un alias >|\<campo exp > [[AS] \<alias >]|  
|\<campo exp >|(\<relación exp >) &#124;<br /><br /> \<exp calcula > &#124;<br /><br /> \<exp agregado > &#124;<br /><br /> \<nueva exp >|  
|< relation_exp >|\<tabla exp > [[AS] \<alias >]<br /><br /> RELACIONAR \<relación-cond-list >|  
|\<relación-cond-list >|\<relación cond > [, \<relación cond >...]|  
|\<relación cond >|\<nombre del campo > TO \<ref secundarios >|  
|\<ref secundarios >|\<nombre del campo > &#124;<br /><br /> PARÁMETRO \<ref de param >|  
|\<ref de param >|\<número >|  
|\<lista de campos >|\<nombre del campo > [, \<nombre de campo >]|  
|\<exp agregado >|SUM (\<nombre de campo completo >) &#124;<br /><br /> AVG (\<nombre de campo completo >) &#124;<br /><br /> MIN (\<nombre de campo completo >) &#124;<br /><br /> MAX (\<nombre de campo completo >) &#124;<br /><br /> RECUENTO (\<calificado-alias > &#124; \<nombre calificado >) &#124;<br /><br /> STDEV (\<nombre de campo completo >) &#124;<br /><br /> CUALQUIER (\<nombre de campo completo >)|  
|\<exp calcula >|CALC (\<expresión >)|  
|\<nombre de campo completo >|\<alias >. [\<alias >...] \<nombre de campo >|  
|\<alias >|\<QUOTED-name >|  
|\<nombre de campo >|\<QUOTED-name > [[AS] \<alias >]|  
|\<QUOTED-name >|"\<cadena >" &#124;<br /><br /> '\<cadena >' &#124;<br /><br /> [\<cadena >] &#124;<br /><br /> \<nombre >|  
|\<nombre calificado >|alias [.alias...]|  
|\<nombre >|alfa [alpha &#124; dígito &#124; _ &#124; # &#124;: &#124;...]|  
|\<número >|dígito [dígitos...]|  
|\<nueva exp >|NUEVA \<tipo de campo > [(\<número > [, \<número >])]|  
|\<tipo de campo >|Un tipo de datos OLE DB o ADO.|  
|\<cadena >|carácter Unicode [unicode-char...]|  
|\<expresión >|Un Visual Basic para expresiones de las aplicaciones cuyos operandos son otras columnas no calculadas de la misma fila.|  
  
## <a name="see-also"></a>Vea también  
 [Acceso a las filas en un conjunto de registros jerárquico](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [Información general sobre la forma de datos](../../../ado/guide/data/data-shaping-overview.md)   
 [Proveedores deseados para dar forma a datos](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Cláusula APPEND Shape](../../../ado/guide/data/shape-append-clause.md)   
 [Comandos Shape en General](../../../ado/guide/data/shape-commands-in-general.md)   
 [Cláusula COMPUTE de forma](../../../ado/guide/data/shape-compute-clause.md)   
 [Visual Basic para las funciones de aplicaciones](../../../ado/guide/data/visual-basic-for-applications-functions.md)
