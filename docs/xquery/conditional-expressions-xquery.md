---
title: Expresiones condicionales (XQuery) | Microsoft Docs
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
- XQuery, conditional expressions
- expressions [XQuery], conditional
- effective Boolean value [XQuery]
- if-then-else statement [XQuery]
- conditional expressions [XQuery]
- EBV
ms.assetid: b280dd96-c80f-4c51-bc06-a88d42174acb
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3164d17169e0a90416c8131825c3d61b1ff5fe16
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51677594"
---
# <a name="conditional-expressions-xquery"></a>Expresiones condicionales (XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  XQuery admite lo siguiente condicional **if-then-else** instrucción:  
  
```  
if (<expression1>)  
then  
  <expression2>  
else  
  <expression3>  
```  
  
 Según el valor booleano efectivo de `expression1`, se evalúa `expression2` o `expression3`. Por ejemplo:  
  
-   Si la expresión de prueba `expression1` da como resultado una secuencia vacía, el resultado será False.  
  
-   Si la expresión de prueba `expression1` da como resultado un valor booleano simple, este valor será el resultado de la expresión.  
  
-   Si la expresión de prueba `expression1` da como resultado una secuencia de uno o varios nodos, el resultado de la expresión será True.  
  
-   De lo contrario, se generará un error estático.  
  
 También tenga en cuenta lo siguiente:  
  
-   La expresión de prueba se debe escribir entre paréntesis.  
  
-   El **else** expresión es necesaria. Si no la necesita, puede devolver " ( ) ", tal como se ilustra en los ejemplos de este tema.  
  
 Por ejemplo, se especifica la consulta siguiente contra la **xml** variable de tipo. El **si** condición prueba el valor de la variable SQL (@v) dentro de la expresión XQuery mediante el uso de la [:variable()](../xquery/xquery-extension-functions-sql-variable.md) función de extensión. Si el valor de la variable es "FirstName", devolverá el elemento <`FirstName`>. De lo contrario, devolverá el elemento <`LastName`>.  
  
```  
declare @x xml  
declare @v varchar(20)  
set @v='FirstName'  
set @x='  
<ROOT rootID="2">  
  <FirstName>fname</FirstName>  
  <LastName>lname</LastName>  
</ROOT>'  
SELECT @x.query('  
if ( sql:variable("@v")="FirstName" ) then  
  /ROOT/FirstName  
 else  
   /ROOT/LastName  
')  
```  
  
 El resultado es el siguiente:  
  
```  
<FirstName>fname</FirstName>  
```  
  
 La consulta siguiente recupera las dos primeras descripciones de características de la descripción del catálogo de productos de un modelo de producto determinado. Si hay más características en el documento, agrega un elemento <`there-is-more`> sin contenido.  
  
```  
SELECT CatalogDescription.query('  
     declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     <Product>   
          { /p1:ProductDescription/@ProductModelID }  
          { /p1:ProductDescription/@ProductModelName }   
          {  
            for $f in /p1:ProductDescription/p1:Features/*[position()\<=2]  
            return  
            $f   
          }  
          {  
            if (count(/p1:ProductDescription/p1:Features/*) > 2)  
            then \<there-is-more/>  
            else ()  
          }   
     </Product>          
') as x  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 En la consulta anterior, la condición en la **si** expresión comprueba si hay más de dos elementos secundarios de <`Features`>. Si éste es el caso, devuelve el elemento `\<there-is-more/>` en el resultado.  
  
 El resultado es el siguiente:  
  
```  
<Product ProductModelID="19" ProductModelName="Mountain 100">  
  \<p1:Warranty xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    \<p1:WarrantyPeriod>3 years\</p1:WarrantyPeriod>  
    \<p1:Description>parts and labor\</p1:Description>  
  \</p1:Warranty>  
  \<p2:Maintenance xmlns:p2="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    \<p2:NoOfYears>10 years\</p2:NoOfYears>  
    \<p2:Description>maintenance contract available through your dealer or any AdventureWorks retail store.\</p2:Description>  
  \</p2:Maintenance>  
  \<there-is-more />  
</Product>  
```  
  
 En la consulta siguiente, se devuelve un elemento <`Location`> con un atributo LocationID si la ubicación de centro de trabajo no especifica las horas de instalación.  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        for $WC in //AWMI:root/AWMI:Location  
        return  
        if ( $WC[not(@SetupHours)] )  
        then  
          <WorkCenterLocation>  
             { $WC/@LocationID }   
          </WorkCenterLocation>  
         else  
           ()  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 El resultado es el siguiente:  
  
```  
<WorkCenterLocation LocationID="30" />  
<WorkCenterLocation LocationID="45" />  
<WorkCenterLocation LocationID="60" />  
```  
  
 Esta consulta se puede escribir sin la **si** cláusula, tal como se muestra en el ejemplo siguiente:  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in //AWMI:root/AWMI:Location[not(@SetupHours)]   
        return  
          <Location>  
             { $WC/@LocationID }   
          </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
## <a name="see-also"></a>Vea también  
 [Expresiones XQuery](../xquery/xquery-expressions.md)  
  
  
