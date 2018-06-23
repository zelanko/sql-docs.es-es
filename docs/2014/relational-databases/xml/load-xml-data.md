---
title: Carga de datos XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- XML data [SQL Server], loading
- loading XML data
ms.assetid: d1741e8d-f44e-49ec-9f14-10208b5468a7
caps.latest.revision: 19
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: e3b250b955028e3f0843699688713cb731f00fee
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198849"
---
# <a name="load-xml-data"></a>Cargar datos XML
  Puede transferir los datos XML a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] de varias maneras. Por ejemplo:  
  
-   Si tiene datos en una columna [n]text o image en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , puede importar la tabla mediante [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Cambie el tipo de columna a XML mediante la instrucción ALTER TABLE.  
  
-   Puede realizar una copia masiva de los datos desde otra base de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante bcp out y, después, hacer una inserción masiva de los datos en la versión posterior de la base de datos mediante bcp in.  
  
-   Si tiene datos en columnas relacionales de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , cree una tabla nueva con una columna [n]text y, si lo desea, una columna de clave principal para disponer de un identificador de fila. Usar programación para recuperar el XML que se genera en el servidor con FOR XML del lado cliente y escribirlo en la `[n]text` columna. A continuación, use las técnicas mencionadas previamente para transferir datos a una base de datos de una versión posterior. Puede optar por escribir el XML directamente en una columna XML en la base de datos de la versión posterior.  
  
## <a name="bulk-loading-xml-data"></a>Carga masiva de datos XML  
 Puede realizar una carga masiva de datos XML en el servidor mediante las funciones de carga masiva de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como bcp. OPENROWSET permite cargar datos en una columna XML desde archivos. El siguiente ejemplo muestra esta función.  
  
##### <a name="example-loading-xml-from-files"></a>Ejemplo: cargar XML desde archivos  
 Este ejemplo muestra cómo insertar una fila en la tabla T. El valor de la columna XML se carga desde el archivo C:\MyFile\xmlfile.xml como CLOB y se suministra el valor 10 a la columna de enteros.  
  
```  
INSERT INTO T  
SELECT 10, xCol  
FROM    (SELECT *      
    FROM OPENROWSET (BULK 'C:\MyFile\xmlfile.xml', SINGLE_CLOB)   
 AS xCol) AS R(xCol)  
```  
  
## <a name="text-encoding"></a>Codificación de texto  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] almacena los datos XML en Unicode (UTF-16). Los datos XML recuperados del servidor se reciben con codificación UTF-16. Si desea otra codificación, tendrá que realizar la conversión necesaria en los datos recuperados. En ocasiones, los datos XML pueden tener una codificación distinta. Si éste es el caso, debe prestar atención al cargar los datos. Por ejemplo:  
  
-   Si el XML de texto es Unicode (UCS-2, UTF-16), puede asignarlo a una columna, una variable o un parámetro XML sin problemas.  
  
-   Si la codificación no es Unicode y está implícita, debido a la página de códigos original, la página de códigos de cadena de la base de datos debe coincidir o ser compatible con los puntos de código que desea cargar. Si es necesario, use COLLATE. Si no existe tal página de códigos de servidor, deberá agregar una declaración XML explícita con la codificación correcta.  
  
-   Para usar una codificación explícita, use la `varbinary()` escriba, que no tiene interacción con páginas de códigos, o utilice un tipo de cadena de la página de códigos apropiada. A continuación, asigne los datos a una columna, una variable o un parámetro XML.  
  
### <a name="example-explicitly-specifying-an-encoding"></a>Ejemplo: especificar explícitamente una codificación  
 Suponga que tiene un documento XML, vcdoc, almacenado como `varchar(max)`, que no dispone de una declaración XML explícita. La siguiente instrucción agrega una declaración XML con la codificación "iso8859-1", concatena el documento XML, convierte el resultado a `varbinary(max)` para que la representación de bytes se conservan y, a continuación, finalmente, lo convierte a XML. De este modo, se habilita el procesador XML para analizar los datos según la codificación especificada "iso8859-1" y generar la representación UTF-16 correspondiente para los valores de cadena.  
  
```  
SELECT CAST(   
CAST (('<?xml version="1.0" encoding="iso8859-1"?>'+ vcdoc) AS VARBINARY (MAX))   
 AS XML)  
```  
  
### <a name="string-encoding-incompatibilities"></a>Incompatibilidades de codificación de cadenas  
 Si se copia y se pega XML como un literal de cadena en una ventana del Editor de consultas de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], pueden producirse incompatibilidades de codificación de cadenas [N]VARCHAR. Esto dependerá de la codificación de la instancia XML. En muchos casos, es posible que se desee quitar la declaración XML. Por ejemplo:  
  
```  
<?xml version="1.0" encoding="UTF-8"?>  
  <xsd:schema …  
```  
  
 Debe incluirse una N a continuación para que la instancia XML sea una instancia de Unicode. Por ejemplo:  
  
```  
-- Assign XML instance to a variable.  
DECLARE @X XML  
SET @X = N'…'  
-- Insert XML instance into an xml type column.  
INSERT INTO T VALUES (N'…')  
-- Create an XML schema collection  
CREATE XML SCHEMA COLLECTION XMLCOLL1 AS N'<xsd:schema … '  
```  
  
## <a name="see-also"></a>Vea también  
 [Datos XML &#40;SQL Server&#41;](xml-data-sql-server.md)  
  
  