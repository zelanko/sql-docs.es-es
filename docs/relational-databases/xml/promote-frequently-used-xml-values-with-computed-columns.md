---
title: Promoción de los valores XML usados con frecuencia con columnas calculadas | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- promoting properties [XML in SQL Server]
- property promotion [XML in SQL Server]
ms.assetid: f5111896-c2fd-4209-b500-f2baa45489ad
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 680232b1a65bf811c5281da715e4fb93fd2f416f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47735693"
---
# <a name="promote-frequently-used-xml-values-with-computed-columns"></a>Promover los valores XML usados con frecuencia con columnas calculadas
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Si se efectúan consultas principalmente en una cantidad pequeña de valores de elementos y atributos, puede que sea conveniente promover estas cantidades a columnas relacionales. Esto es útil cuando se ejecutan consultas en una pequeña parte de los datos XML mientras se recupera toda la instancia XML. No es necesario crear un índice XML en la columna XML. En lugar de ello, se puede indizar la columna promocionada. Las consultas se deben escribir de modo que usen la columna promocionada. Es decir, que el optimizador de consultas no dirige de nuevo las consultas de la columna XML a la columna promocionada.  
  
 La columna promocionada puede ser una columna calculada de la misma tabla o puede ser una columna aparte, mantenida por el usuario, de una tabla. Esto es suficiente cuando se promocionan valores singleton desde cada instancia XML. No obstante, en el caso de propiedades con varios valores, es necesario crear una tabla aparte para la propiedad, como se describe en la sección siguiente.  
  
## <a name="computed-column-based-on-the-xml-data-type"></a>Columna calculada basada en el tipo de datos xml  
 Una columna calculada se puede crear mediante una función definida por el usuario que invoque métodos de tipos de datos **xml** . El tipo de la columna calculada puede ser cualquiera SQL, incluido XML. Esto se muestra en el ejemplo siguiente.  
  
### <a name="example-computed-column-based-on-the-xml-data-type-method"></a>Ejemplo: columna calculada basada en el método de tipo de datos xml  
 Cree la función definida por el usuario para obtener el número ISBN de un libro:  
  
```  
CREATE FUNCTION udf_get_book_ISBN (@xData xml)  
RETURNS varchar(20)  
BEGIN  
   DECLARE @ISBN   varchar(20)  
   SELECT @ISBN = @xData.value('/book[1]/@ISBN', 'varchar(20)')  
   RETURN @ISBN   
END  
```  
  
 Agregue una columna calculada a la tabla para el ISBN:  
  
```  
ALTER TABLE      T  
ADD   ISBN AS dbo.udf_get_book_ISBN(xCol)  
```  
  
 La columna calculada se puede indizar de la manera habitual.  
  
### <a name="example-queries-on-a-computed-column-based-on-xml-data-type-methods"></a>Ejemplo: consultas en una columna calculada basada en métodos de tipo de datos xml  
 Para obtener el <`book`> cuyo ISBN es 0-7356-1588-2:  
  
```  
SELECT xCol  
FROM   T  
WHERE  xCol.exist('/book/@ISBN[. = "0-7356-1588-2"]') = 1  
```  
  
 La consulta en la columna XML se puede volver a escribir de modo que utilice la columna calculada, como se indica a continuación:  
  
```  
SELECT xCol  
FROM   T  
WHERE  ISBN = '0-7356-1588-2'  
```  
  
 Puede crear una función definida por el usuario que devuelva el tipo de datos **xml** y una columna calculada mediante la función definida por el usuario. Sin embargo, no puede crear un índice XML en la columna XML calculada.  
  
## <a name="creating-property-tables"></a>Crear tablas de propiedades  
 Tal vez desee promocionar algunas de las propiedades con varios valores desde los datos XML a una o más tablas, crear índices en estas tablas y orientar de nuevo las consultas para que las utilicen. Un escenario típico es el caso en que un pequeño número de propiedades cubre casi toda la carga de trabajo de la consulta. Puede hacer lo siguiente:  
  
-   Cree una o más tablas que contengan las propiedades con varios valores. Puede resultarle práctico almacenar una propiedad por tabla y duplicar la clave principal de la tabla base en las tablas de propiedades para combinarlas de nuevo con la tabla base.  
  
-   Si desea mantener el orden relativo de las propiedades, tiene que insertar una columna nueva para el orden relativo.  
  
-   Cree desencadenadores en la columna XML para mantener las tablas de propiedades. En los desencadenadores, realice una de las siguientes operaciones:  
  
    -   Use métodos de tipo de datos **xml** , como **nodes()** y **value()**, para insertar y eliminar filas de las tablas de propiedades.  
  
    -   Cree funciones de transmisión por secuencias con valores de tabla en Common Language Runtime (CLR) para insertar y eliminar filas de las tablas de propiedades.  
  
    -   Escriba consultas para el acceso de SQL a las tablas de propiedades y para el acceso de XML a la columna XML de la tabla base, con combinaciones entre las tablas mediante el uso de su clave principal.  
  
### <a name="example-create-a-property-table"></a>Ejemplo: crear una tabla de propiedades  
 A modo de ilustración, suponga que desea promocionar el nombre de los autores. Los libros tienen uno o varios autores, por lo que sus nombres son una propiedad con varios valores. Cada nombre se almacena en una fila distinta de una tabla de propiedades. La clave principal de la tabla base se duplica en la tabla de propiedades para que se puedan volver a combinar más tarde.  
  
```  
create table tblPropAuthor (propPK int, propAuthor varchar(max))  
```  
  
### <a name="example-create-a-user-defined-function-to-generate-a-rowset-from-an-xml-instance"></a>Ejemplo: crear una función definida por el usuario para generar un conjunto de filas a partir de una instancia XML  
 La siguiente función con valores de tabla, udf_XML2Table, acepta un valor de clave principal y una instancia XML. Recupera el nombre de todos los autores de los elementos <`book`> y devuelve un conjunto de filas de pares de nombres y claves principales.  
  
```  
create function udf_XML2Table (@pk int, @xCol xml)  
returns @ret_Table table (propPK int, propAuthor varchar(max))  
with schemabinding  
as  
begin  
      insert into @ret_Table   
      select @pk, nref.value('.', 'varchar(max)')  
      from   @xCol.nodes('/book/author/first-name') R(nref)  
      return  
end  
```  
  
### <a name="example-create-triggers-to-populate-a-property-table"></a>Ejemplo: crear desencadenadores para rellenar una tabla de propiedades  
 El desencadenador insert inserta filas en la tabla de propiedades:  
  
```  
create trigger trg_docs_INS on T for insert  
as  
      declare @wantedXML xml  
      declare @FK int  
      select @wantedXML = xCol from inserted  
      select @FK = PK from inserted  
  
   insert into tblPropAuthor  
   select * from dbo.udf_XML2Table(@FK, @wantedXML)  
```  
  
 El desencadenador delete elimina las filas de la tabla de propiedades basándose en el valor de la clave principal de las filas eliminadas:  
  
```  
create trigger trg_docs_DEL on T for delete  
as  
   declare @FK int  
   select @FK = PK from deleted  
   delete tblPropAuthor where propPK = @FK  
```  
  
 El desencadenador update elimina las filas existentes en la tabla de propiedades correspondientes a la instancia XML actualizada e inserta nuevas filas en la tabla de propiedades:  
  
```  
create trigger trg_docs_UPD  
on T  
for update  
as  
if update(xCol) or update(pk)  
begin  
      declare @FK int  
      declare @wantedXML xml  
      select @FK = PK from deleted  
      delete tblPropAuthor where propPK = @FK  
  
   select @wantedXML = xCol from inserted  
   select @FK = pk from inserted  
  
   insert into tblPropAuthor   
      select * from dbo.udf_XML2Table(@FK, @wantedXML)  
end  
```  
  
### <a name="example-find-xml-instances-whose-authors-have-the-same-first-name"></a>Ejemplo: buscar instancias XML cuyos autores tengan el mismo nombre  
 La consulta se puede formar en la columna XML. Otra posibilidad es buscar en la tabla de propiedades el nombre "David" y combinarla de nuevo con la tabla base para devolver la instancia XML. Por ejemplo:  
  
```  
SELECT xCol   
FROM     T JOIN tblPropAuthor ON T.pk = tblPropAuthor.propPK  
WHERE    tblPropAuthor.propAuthor = 'David'  
```  
  
### <a name="example-solution-using-the-clr-streaming-table-valued-function"></a>Ejemplo: solución mediante la función de transmisión por secuencias con valores de tabla de CLR  
 Esta solución consta de los siguientes pasos:  
  
1.  Defina una clase de CLR, SqlReaderBase, que implemente ISqlReader y genere una función de salida de transmisión por secuencias con valores de tabla aplicando una expresión de ruta de acceso en una instancia XML.  
  
2.  Cree un ensamblado y una función Transact-SQL definida por el usuario para iniciar la clase de CLR.  
  
3.  Defina los desencadenadores insert, update y delete mediante la función definida por el usuario para mantener tablas de propiedades.  
  
 Para ello, primero deberá crear la función de transmisión por secuencias de CLR. El tipo de datos **xml** se expone como una clase administrada SqlXml en ADO.NET y admite el método **CreateReader()** que devuelve un XmlReader.  
  
> [!NOTE]  
>  El código de ejemplo de esta sección usa XPathDocument y XPathNavigator. De este modo, se fuerza la carga de todos los documentos XML en la memoria. Si utiliza código similar en su aplicación para procesar varios documentos XML grandes, este código no es escalable. En lugar de ello, mantenga asignaciones de memoria de pequeño tamaño y use interfaces de transmisión por secuencias siempre que sea posible. Para obtener más información sobre el rendimiento, vea [Arquitectura de integración CLR](http://msdn.microsoft.com/library/05e4b872-3d21-46de-b4d5-739b5f2a0cf9).  
  
```  
public class c_streaming_xml_tvf {  
   public static ISqlReader streaming_xml_tvf   
(SqlXml xmlDoc, string pathExpression) {  
      return (new TestSqlReaderBase (xmlDoc, pathExpression));  
   }  
}  
  
// Class that implements ISqlReader  
public class TestSqlReaderBase : ISqlReader {  
XPathNodeIterator m_iterator;           
   public SqlChars FirstName;  
// Metadata for current resultset  
private SqlMetaData[] m_rgSqlMetaData;        
  
   public TestSqlReaderBase (SqlXml xmlDoc, string pathExpression) {     
      // Variables for XPath navigation  
      XPathDocument xDoc;  
      XPathNavigator xNav;  
      XPathExpression xPath;  
  
      // Set sql metadata  
      m_rgSqlMetaData = new SqlMetaData[1];  
      m_rgSqlMetaData[0] = new SqlMetaData ("FirstName",    
SqlDbType.NVarChar,50);     
  
      //Set up the Navigator  
      if (!xmlDoc.IsNull)  
          xDoc = new XPathDocument (xmlDoc.CreateReader());  
      else  
          xDoc = new XPathDocument ();  
      xNav = xDoc.CreateNavigator();  
      xPath = xNav.Compile (pathExpression);  
      m_iterator = xNav.Select(xPath);  
   }  
   public bool Read() {  
      bool moreRows = true;  
      if (moreRows = m_iterator.MoveNext())  
         FirstName = new SqlChars (m_iterator.Current.Value);  
      return moreRows;  
   }  
}  
```  
  
 A continuación, cree un ensamblado y una función [!INCLUDE[tsql](../../includes/tsql-md.md)] definida por el usuario, SQL_streaming_xml_tvf (no se muestra), que corresponda a la función CLR, streaming_xml_tvf. La función definida por el usuario se utiliza para definir la función con valores de tabla, CLR_udf_XML2Table, para la generación de conjuntos de filas:  
  
```  
create function CLR_udf_XML2Table (@pk int, @xCol xml)  
returns @ret_Table table (FK int, FirstName varchar(max))  
with schemabinding  
as  
begin  
      insert into @ret_Table   
   select @pk, FirstName   
   FROM   SQL_streaming_xml_tvf (@xCol, '/book/author/first-name')  
      return  
end  
```  
  
 Por último, defina desencadenadores como se muestra en el ejemplo "Crear desencadenadores para rellenar una tabla de propiedades", pero sustituya udf_XML2Table por la función CLR_udf_XML2Table. El desencadenador insert se muestra en el ejemplo siguiente:  
  
```  
create trigger CLR_trg_docs_INS on T for insert  
as  
   declare @wantedXML xml  
   declare @FK int  
   select @wantedXML = xCol from inserted  
   select @FK = PK from inserted  
  
   insert into tblPropAuthor  
      select *  
   from    dbo.CLR_udf_XML2Table(@FK, @wantedXML)  
```  
  
 El desencadenador delete es idéntico a la versión no CLR. Sin embargo, el desencadenador update simplemente reemplaza la función udf_XML2Table() por CLR_udf_XML2Table().  
  
## <a name="see-also"></a>Ver también  
 [Usar XML en columnas calculadas](../../relational-databases/xml/use-xml-in-computed-columns.md)  
  
  
