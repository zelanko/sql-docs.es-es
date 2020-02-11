---
title: Consultas XQuery que implica jerarquía | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- hierarchies [XQuery]
- XQuery, hierarchies
ms.assetid: 6953d8b7-bad8-4b64-bf7b-12fa4f10f65c
author: rothja
ms.author: jroth
ms.openlocfilehash: 8aa762af8e08c72f7f00369219771c371ce39aac
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67946101"
---
# <a name="xqueries-involving-hierarchy"></a>Consultas XQuery con jerarquía
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  La mayoría de las columnas de tipo **XML** de la base de datos **AdventureWorks** son documentos semiestructurados. Por lo tanto, los documentos almacenados en cada fila pueden tener un aspecto diferente. Los ejemplos de consultas incluidos en este tema muestran cómo extraer información de estos documentos.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-from-the-manufacturing-instructions-documents-retrieve-work-center-locations-together-with-the-first-manufacturing-step-at-those-locations"></a>A. A partir de los documentos de instrucciones de fabricación, recupere ubicaciones de los centros de trabajo junto con el primer paso del proceso de fabricación en esas ubicaciones  
 En el modelo de producto 7, la consulta crea XML que incluye el `ManuInstr` elemento <>, con los atributos **ProductModelID** y **ProductModelName** , y uno o `Location` varios <> elementos secundarios.  
  
 Cada <`Location` elemento> tiene su propio conjunto de atributos y un <`step`> elemento secundario. Esta <`step`> elemento secundario es el primer paso de fabricación en la ubicación del centro de trabajo.  
  
```sql
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
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
  
-   La palabra clave **namespace** del [prólogo de XQuery](../xquery/modules-and-prologs-xquery-prolog.md) define un prefijo de espacio de nombres. Este prefijo se utiliza posteriormente en el cuerpo de la consulta.  
  
-   Los tokens de contexto, {) y (}, se utilizan para cambiar la consulta de construcción de XML a evaluación de consulta.  
  
-   **SQL: column ()** se usa para incluir un valor relacional en el XML que se está construyendo.  
  
-   Al construir el elemento> `Location` de <, $WC/@ * recupera todos los atributos de ubicación del centro de trabajo.  
  
-   La función **String ()** devuelve el valor de cadena del elemento `step` <>.  
  
 Éste es un resultado parcial:  
  
```xml
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
 La siguiente consulta recupera números de teléfono adicionales para un contacto de cliente específico buscando en toda la jerarquía el elemento `telephoneNumber` de> de <. Dado que el `telephoneNumber` elemento de> de <puede aparecer en cualquier parte de la jerarquía, la consulta utiliza el operador descendiente y self (//) en la búsqueda.  
  
```sql
SELECT AdditionalContactInfo.query('  
 declare namespace ci="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
 declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
for $ph in /ci:AdditionalContactInfo//act:telephoneNumber  
   return  
      $ph/act:number  
') as x  
FROM  Person.Contact  
WHERE ContactID = 1  
```  
  
 El resultado es el siguiente:  
  
```xml
\<act:number   
  xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  111-111-1111  
\</act:number>  
\<act:number   
  xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  112-111-1111  
\</act:number>  
```  
  
 Para recuperar solo los números de teléfono de nivel superior, específicamente el `telephoneNumber` <> elementos secundarios de `AdditionalContactInfo` <>, la expresión for de la consulta cambia a  
  
 `for $ph in /ci:AdditionalContactInfo/act:telephoneNumber`.  
  
## <a name="see-also"></a>Consulte también  
 [Conceptos básicos de XQuery](../xquery/xquery-basics.md)   
 [Construcción XML &#40;XQuery&#41;](../xquery/xml-construction-xquery.md)   
 [Datos XML &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)  
  
  
