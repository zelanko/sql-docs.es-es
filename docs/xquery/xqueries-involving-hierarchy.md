---
title: "Consultas XQuery con jerarquía | Documentos de Microsoft"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- hierarchies [XQuery]
- XQuery, hierarchies
ms.assetid: 6953d8b7-bad8-4b64-bf7b-12fa4f10f65c
caps.latest.revision: 25
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 013f30f34a09de280e3c16e44ecef4c9ee58b9eb
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="xqueries-involving-hierarchy"></a>Consultas XQuery con jerarquía
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  La mayoría **xml** escriba columnas en la **AdventureWorks** base de datos son documentos semiestructurados. Por lo tanto, los documentos almacenados en cada fila pueden tener un aspecto diferente. Los ejemplos de consultas incluidos en este tema muestran cómo extraer información de estos documentos.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-from-the-manufacturing-instructions-documents-retrieve-work-center-locations-together-with-the-first-manufacturing-step-at-those-locations"></a>A. A partir de los documentos de instrucciones de fabricación, recupere ubicaciones de los centros de trabajo junto con el primer paso del proceso de fabricación en esas ubicaciones  
 Para el modelo de producto 7, la consulta genera XML que incluye el <`ManuInstr`> elemento, con **ProductModelID** y **ProductModelName** atributos y uno o más <`Location`> elementos secundarios.  
  
 Cada elemento <`Location`> tiene su propio conjunto de atributos y un elemento secundario <`step`>. Este elemento secundario <`step`> es el primer paso del proceso de fabricación en la ubicación del centro de trabajo.  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   \<ManuInstr  ProdModelID = "{sql:column("Production.ProductModel.ProductModelID") }"   
                ProductModelName = "{ sql:column("Production.ProductModel.Name") }" >  
            {   
              for $wc in //AWMI:root/AWMI:Location  
              return  
                <Location>  
                 {$wc/@* }  
                 <step1> { string( ($wc//AWMI:step)[1] ) } </step1>  
                </Location>  
            }  
          </ManuInstr>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Observe lo siguiente en la consulta anterior:  
  
-   El **espacio de nombres** palabra clave en el [prólogo de XQuery](../xquery/modules-and-prologs-xquery-prolog.md) define un prefijo de espacio de nombres. Este prefijo se utiliza posteriormente en el cuerpo de la consulta.  
  
-   Los tokens de contexto, {) y (}, se utilizan para cambiar la consulta de construcción de XML a evaluación de consulta.  
  
-   El **SQL:Column()** se usa para incluir un valor relacional en el XML que se está construyendo.  
  
-   Al construir el elemento <`Location`>, $wc/@* recupera todos los atributos de ubicación de centros de trabajo.  
  
-   El **string()** función devuelve el valor de cadena de la <`step`> elemento.  
  
 Éste es un resultado parcial:  
  
```  
<ManuInstr ProdModelID="7" ProductModelName="HL Touring Frame">  
   <Location LocationID="10" SetupHours="0.5"   
            MachineHours="3" LaborHours="2.5" LotSize="100">  
     <step1>Insert aluminum sheet MS-2341 into the T-85A   
             framing tool.</step1>  
   </Location>  
   <Location LocationID="20" SetupHours="0.15"   
            MachineHours="2" LaborHours="1.75" LotSize="1">  
      <step1>Assemble all frame components following   
             blueprint 1299.</step1>  
   </Location>  
...  
</ManuInstr>   
```  
  
### <a name="b-find-all-telephone-numbers-in-the-additionalcontactinfo-column"></a>B. Buscar todos los números de teléfono de la columna AdditionalContactInfo  
 La siguiente consulta recupera números de teléfono adicionales para un contacto de cliente específico buscando el elemento <`telephoneNumber`> en toda la jerarquía. Dado que el elemento <`telephoneNumber`> puede aparecer en cualquier lugar de la jerarquía, la consulta usa el operador descendant y self (//) en la búsqueda.  
  
```  
SELECT AdditionalContactInfo.query('  
 declare namespace ci="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
 declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
for $ph in /ci:AdditionalContactInfo//act:telephoneNumber  
   return  
      $ph/act:number  
') as x  
FROM  Person.Contact  
WHERE ContactID = 1  
```  
  
 El resultado es el siguiente:  
  
```  
\<act:number   
  xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  111-111-1111  
\</act:number>  
\<act:number   
  xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  112-111-1111  
\</act:number>  
```  
  
 Para recuperar únicamente los números de teléfono de nivel superior, específicamente los elementos secundarios <`telephoneNumber`> de <`AdditionalContactInfo`>, la expresión FOR de la consulta cambia a  
  
 `for $ph in /ci:AdditionalContactInfo/act:telephoneNumber`.  
  
## <a name="see-also"></a>Vea también  
 [Conceptos básicos de XQuery](../xquery/xquery-basics.md)   
 [Construcción de XML &#40; XQuery &#41;](../xquery/xml-construction-xquery.md)   
 [Datos XML &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)  
  
  

