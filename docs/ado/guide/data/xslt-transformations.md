---
title: Transformaciones XSLT | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- XSLT transformations in ADO
ms.assetid: 1a46196e-839f-4734-a59e-2c64609ffb9e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2606733b3efc5a9641f8de0f544b3cff7c7e9a31
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67923340"
---
# <a name="xslt-transformations"></a>Transformaciones XSLT
XSLT se puede aplicar al XML generado para transformarlo en otro formato. Entender el formato XML en ADO ayuda a desarrollar plantillas XSLT que pueden transformarlas en un formato más fácil de utilizar.  
  
 Por ejemplo, sabe que cada fila del conjunto de registros se guarda como el elemento z:Row dentro del elemento RS: Data. Del mismo modo, cada campo del conjunto de registros se guarda como un par atributo-valor para este elemento.  
  
## <a name="remarks"></a>Observaciones  
 El siguiente script XSLT se puede aplicar al XML que se muestra en la sección anterior para transformarlo en una tabla HTML que se mostrará en el explorador:  
  
```  
<?xml version="1.0" encoding="ISO-8859-1"?>  
<html xmlns:xsl="http://www.w3.org/TR/WD-xsl">  
<body STYLE="font-family:Arial, helvetica, sans-serif; font-size:12pt; background-color:white">  
<table border="1" style="table-layout:fixed" width="600">  
  <col width="200"></col>  
  <tr bgcolor="teal">  
    <th><font color="white">CustomerId</font></th>  
    <th><font color="white">CompanyName</font></th>  
    <th><font color="white">ContactName</font></th>  
  </tr>  
<xsl:for-each select="xml/rs:data/z:row">  
  <tr bgcolor="navy">  
    <td><font color="white"><xsl:value-of select="@CustomerID"/></font></td>  
    <td><font color="white"><xsl:value-of select="@CompanyName"/></font></td>  
    <td><font color="white"><xsl:value-of select="@ContactName"/></font></td>   
  </tr>  
</xsl:for-each>  
</table>  
</body>  
</html>  
```  
  
 El XSLT convierte la secuencia XML generada por el método Save de ADO en una tabla HTML que muestra cada campo del conjunto de registros junto con un encabezado de tabla. También se asignan fuentes y colores diferentes a los encabezados y las filas de la tabla.  
  
## <a name="see-also"></a>Consulte también  
 [Almacenar registros en formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
