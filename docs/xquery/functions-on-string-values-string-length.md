---
title: Función String-length (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- string-length function
- fn:string-length function
ms.assetid: 7cd69c8b-cf2c-478c-b9a3-e0e14e1aa8aa
author: rothja
ms.author: jroth
ms.openlocfilehash: 12ae1efbf900a505a5f257f9684842a0ad9ff21f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004653"
---
# <a name="functions-on-string-values---string-length"></a>Funciones usadas en valores de cadena: string-length
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve la longitud de la cadena en caracteres.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
fn:string-length() as xs:integer  
fn:string-length($arg as xs:string?) as xs:integer  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Cadena de origen cuya longitud se va a calcular.  
  
## <a name="remarks"></a>Comentarios  
 Si el valor de *$arg* es una secuencia vacía, un **xs: Integer** devuelve el valor de 0.  
  
 El comportamiento de los pares suplentes en funciones XQuery depende del nivel de compatibilidad de la base de datos. Si el nivel de compatibilidad es 110 o superior, cada par suplente se cuenta como un carácter individual. Para los niveles de compatibilidad inferiores, se cuentan como dos caracteres. Para obtener más información, consulte [nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41; ](../t-sql/statements/alter-database-transact-sql-compatibility-level.md) y [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md).  
  
 Si el valor contiene un carácter Unicode de 4 bytes representado por dos caracteres suplentes, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] contará los caracteres suplentes individualmente.  
  
 El **string-length()** sin un parámetro solo se puede usar dentro de un predicado. Por ejemplo, la consulta siguiente devuelve el <`ROOT`> elemento:  
  
```  
DECLARE @x xml;  
SET @x='<ROOT>Hello</ROOT>';  
SELECT @x.query('/ROOT[string-length()=5]');  
```  
  
## <a name="supplementary-characters-surrogate-pairs"></a>Caracteres adicionales (pares suplentes)  
 El comportamiento de pares suplentes en las funciones XQuery depende del nivel de compatibilidad de la base de datos y, en algunos casos, del URI del espacio de nombres predeterminado de las funciones. Para obtener más información, vea la sección "XQuery funciones detectan los caracteres suplentes" en el tema [cambios recientes en las características del motor de base de datos en SQL Server 2016](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md). Consulte también [nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41; ](../t-sql/statements/alter-database-transact-sql-compatibility-level.md) y [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="examples"></a>Ejemplos  
 En este tema se proporciona ejemplos de XQuery con instancias XML almacenadas en varias **xml** columnas de tipo en la base de datos AdventureWorks.  
  
### <a name="a-using-the-string-length-xquery-function-to-retrieve-products-with-long-summary-descriptions"></a>A. Usar la función string-length() de XQuery para recuperar productos con descripciones resumidas largas  
 Para los productos cuya descripción resumida tiene más de 50 caracteres, la consulta siguiente recupera el identificador de producto, la longitud de la descripción resumida y el resumen en Sí, el <`Summary`> elemento.  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' as pd)  
SELECT CatalogDescription.query('  
      <Prod ProductID= "{ /pd:ProductDescription[1]/@ProductModelID }" >  
       <LongSummary SummaryLength =   
           "{string-length(string( (/pd:ProductDescription/pd:Summary)[1] )) }" >  
           { string( (/pd:ProductDescription/pd:Summary)[1] ) }  
       </LongSummary>  
      </Prod>  
 ') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.value('string-length( string( (/pd:ProductDescription/pd:Summary)[1]))', 'decimal') > 200;  
```  
  
 Observe lo siguiente en la consulta anterior:  
  
-   La condición de la cláusula WHERE recupera solo las filas donde la descripción resumida almacenada en el documento XML tiene más de 200 caracteres. Usa el [método value() (tipo de datos XML)](../t-sql/xml/value-method-xml-data-type.md).  
  
-   La cláusula SELECT genera solo el XML que desea. Usa el [método query() (tipo de datos XML)](../t-sql/xml/query-method-xml-data-type.md) para construir el XML y especificar la expresión XQuery necesaria para recuperar datos del documento XML.  
  
 Éste es un resultado parcial:  
  
```  
Result  
-------------------  
<Prod ProductID="19">  
      <LongSummary SummaryLength="214">Our top-of-the-line competition   
             mountain bike. Performance-enhancing options include the  
             innovative HL Frame, super-smooth front suspension, and   
             traction for all terrain.  
      </LongSummary>  
</Prod>  
...  
```  
  
### <a name="b-using-the-string-length-xquery-function-to-retrieve-products-whose-warranty-descriptions-are-short"></a>b. Usar la función de XQuery string-length() para recuperar productos cuya descripción de garantía es corta  
 Para los productos cuya descripción de garantía tienen menos de 20 caracteres, la consulta siguiente recupera XML que incluye el identificador de producto, longitud, la descripción de garantía, y la <`Warranty`> propio elemento.  
  
 Warranty es una de las características del producto. Opcional <`Warranty`> elemento secundario sigue después de la <`Features`> elemento.  
  
```  
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
SELECT CatalogDescription.query('  
      for   $ProdDesc in /pd:ProductDescription,  
            $pf in $ProdDesc/pd:Features/wm:Warranty  
      where string-length( string(($pf/wm:Description)[1]) ) < 20  
      return   
          <Prod >  
             { $ProdDesc/@ProductModelID }  
             <ShortFeature FeatureDescLength =   
                             "{string-length( string(($pf/wm:Description)[1]) ) }" >  
                 { $pf }  
             </ShortFeature>  
          </Prod>  
     ') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('/pd:ProductDescription')=1;  
```  
  
 Observe lo siguiente en la consulta anterior:  
  
-   **pd** y **wm** son los prefijos de espacio de nombres utilizados en esta consulta. Identifican los mismos espacios de nombres utilizados en el documento que se va a consultar.  
  
-   La consulta XQuery especifica un bucle FOR anidado. El bucle FOR externo es necesario, ya que van a recuperar el **ProductModelID** los atributos de la <`ProductDescription`> elemento. El bucle FOR interno es necesario, porque solo desea obtener aquellos productos que tengan descripciones de garantía con menos de 20 caracteres.  
  
 Éste es el resultado parcial:  
  
```  
Result  
-------------------------  
<Prod ProductModelID="19">  
  <ShortFeature FeatureDescLength="15">  
    <wm:Warranty   
       xmlns:wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
      <wm:WarrantyPeriod>3 years</wm:WarrantyPeriod>  
      <wm:Description>parts and labor</wm:Description>  
    </wm:Warranty>  
   </ShortFeature>  
</Prod>  
...  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones de XQuery con el tipo de datos xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
