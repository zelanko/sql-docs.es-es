---
title: Gramática formal de forma | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 3b26eaeb804f8d92a7122814641cadf5889b77b8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47789273"
---
# <a name="formal-shape-grammar"></a>Gramática formal de forma
Se trata de la gramática formal para crear cualquier comando shape:  
  
-   Términos gramaticales necesarios son cadenas de texto delimitadas por corchetes angulares ("<>").  
  
-   Términos opcionales están delimitados por corchetes ("[]").  
  
-   Alternativas se indican mediante una barra diagonal ("&#124;").  
  
-   Repetición alternativas se indican mediante un botón de puntos suspensivos ("...").  
  
-   *Alfa* indica una cadena de letras en orden alfabético.  
  
-   *Dígito* indica una cadena de números.  
  
-   *Unicode-dígitos* indica una cadena de dígitos unicode.  
  
 Todos los demás términos son literales.  
  
|Término|Definición|  
|----------|----------------|  
|\<comando de Shape >|FORMA [\<tabla exp > [[AS] \<alias >]] [\<forma Acción >]|  
|\<exp de tabla >|{\<texto de comando de proveedor >}&#124;<br /><br /> (\<forma comando >)&#124;<br /><br /> TABLA \<quoted-name >&#124;<br /><br /> \<QUOTED-name >|  
|\<forma Acción >|ANEXAR \<lista de campos de un alias >&#124;<br /><br /> PROCESO \<lista de campos de un alias > [BY \<lista de campos >]|  
|\<lista de campos de un alias >|\<un alias de campo > [, \<un alias de campo... >]|  
|\<un alias de campo >|\<campo: exp > [[AS] \<alias >]|  
|\<campo: exp >|(\<relación exp >)&#124;<br /><br /> \<exp calculado >&#124;<br /><br /> \<agregado exp >&#124;<br /><br /> \<nueva exp >|  
|<relation_exp>|\<tabla exp > [[AS] \<alias >]<br /><br /> RELACIONAR \<relación-cond-list >|  
|\<relación-cond-list >|\<relación cond > [, \<relación cond >...]|  
|\<relación cond >|\<nombre de campo > TO \<secundarios ref >|  
|\<secundario-ref >|\<nombre de campo >&#124;<br /><br /> PARÁMETRO \<-ref param >|  
|\<-ref param >|\<número >|  
|\<lista de campos >|\<nombre de campo > [, \<nombre de campo >]|  
|\<agregado exp >|SUM (\<nombre de campo completo >)&#124;<br /><br /> AVG (\<nombre de campo completo >)&#124;<br /><br /> MIN (\<nombre de campo completo >)&#124;<br /><br /> MAX (\<nombre de campo completo >)&#124;<br /><br /> RECUENTO (\<calificado-alias > &#124; \<calificado-name >)&#124;<br /><br /> STDEV (\<nombre de campo completo >)&#124;<br /><br /> CUALQUIER (\<nombre de campo completo >)|  
|\<exp calculado >|CALC (\<expresión >)|  
|\<nombre del campo calificado >|\<alias>.[\<alias>...]\<field-name>|  
|\<alias >|\<QUOTED-name >|  
|\<nombre de campo >|\<QUOTED-name > [[AS] \<alias >]|  
|\<QUOTED-name >|"\<string >"&#124;<br /><br /> '\<cadena >'&#124;<br /><br /> [\<cadena >]&#124;<br /><br /> \<Nombre >|  
|\<nombre completo de >|alias [.alias...]|  
|\<Nombre >|alfa [alpha &#124; dígitos &#124; _ &#124; # &#124; : &#124; ...]|  
|\<número >|dígito [dígitos...]|  
|\<nueva exp >|NUEVO \<tipo de campo > [(\<número > [, \<número >])]|  
|\<tipo de campo >|Un tipo de datos OLE DB o ADO.|  
|\<cadena >|-char Unicode [-char unicode...]|  
|\<expresión >|Un objeto Visual expresión Basic para aplicaciones cuyos operandos son otras columnas no calculadas en la misma fila.|  
  
## <a name="see-also"></a>Vea también  
 [Acceso a las filas en un conjunto de registros jerárquico](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [Información general sobre la forma de datos](../../../ado/guide/data/data-shaping-overview.md)   
 [Proveedores deseados para dar forma a datos](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Cláusula APPEND Shape](../../../ado/guide/data/shape-append-clause.md)   
 [Comandos Shape en General](../../../ado/guide/data/shape-commands-in-general.md)   
 [Cláusula COMPUTE de forma](../../../ado/guide/data/shape-compute-clause.md)   
 [Visual Basic para las funciones de aplicaciones](../../../ado/guide/data/visual-basic-for-applications-functions.md)
