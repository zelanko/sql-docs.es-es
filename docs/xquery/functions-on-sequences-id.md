---
title: Id. de función (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:id function
- id function
ms.assetid: de99fc60-d0ad-4117-a17d-02bdde6512b4
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 39b389221613e6bc3d789f47cb9b972d96a53377
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47703843"
---
# <a name="functions-on-sequences---id"></a>Funciones usadas en secuencias: id
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve la secuencia de nodos de elemento con valores xs: ID que coinciden con los valores de uno o varios de los valores xs: IDREF proporcionados en *$arg*.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
fn:id($arg as xs:IDREF*) as element()*  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Uno o varios valores xs:IDREF.  
  
## <a name="remarks"></a>Comentarios  
 El resultado de la función es una secuencia de elementos de la instancia XML, en el orden del documento, que tiene un valor xs:ID equivalente a uno o varios de los valores xs:IDREF de la lista de posibles valores xs:IDREF.  
  
 Si el valor xs:IDREF no coincide con ningún elemento, la función devolverá la secuencia vacía.  
  
## <a name="examples"></a>Ejemplos  
 En este tema se proporciona ejemplos de XQuery con instancias XML almacenadas en varias **xml** escriba columnas en el [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] base de datos.  
  
### <a name="a-retrieving-elements-based-on-the-idref-attribute-value"></a>A. Recuperar elementos en función del valor del atributo IDREF  
 En el ejemplo siguiente se utiliza fn:id. para recuperar los elementos <`employee`>, en función del atributo IDREF manager. En este ejemplo, el atributo manager es de tipo IDREF y el atributo eid es de tipo ID.  
  
 Para un valor de atributo administrador específico, el **ID** función busca el <`employee`> elemento cuyo valor del atributo de tipo ID coincide con el valor IDREF de entrada. En otras palabras, para un empleado concreto, el **ID** función devuelve employee manager.  
  
 A continuación se expone lo que ocurre en el ejemplo:  
  
-   Se crea una colección de esquemas XML.  
  
-   Un tipo **xml** variable se crea mediante el uso de la colección de esquemas XML.  
  
-   La consulta recupera el elemento que tiene un valor de atributo de identificador al que hace referencia el **manager** atributo IDREF de la <`employee`> elemento.  
  
```  
-- If exists, drop the XML schema collection (SC).  
-- drop xml schema collection SC  
-- go  
  
create xml schema collection SC as  
'<schema xmlns="http://www.w3.org/2001/XMLSchema" xmlns:e="emp" targetNamespace="emp">  
            <element name="employees" type="e:EmployeesType"/>  
            <complexType name="EmployeesType">  
                 <sequence>  
                      <element name="employee" type="e:EmployeeType" minOccurs="0" maxOccurs="unbounded" />  
                 </sequence>  
            </complexType>    
  
            <complexType name="EmployeeType">  
                        <attribute name="eid" type="ID" />  
                        <attribute name="name" type="string" />  
                        <attribute name="manager" type="IDREF" />  
            </complexType>         
</schema>'  
go  
```  
  
```  
declare @x xml(SC)  
set @x='<e:employees xmlns:e="emp">  
<employee eid="e1" name="Joe" manager="e10" />  
<employee eid="e2" name="Bob" manager="e10" />  
<employee eid="e10" name="Dave" manager="e10" />  
</e:employees>'  
  
select @x.value(' declare namespace e="emp";   
 (fn:id(e:employees/employee[@name="Joe"]/@manager)/@name)[1]', 'varchar(50)')   
Go  
```  
  
 La consulta devuelve "Dave" como valor. Esto indica que Dave es el superior (manager) de Joe.  
  
### <a name="b-retrieving-elements-based-on-the-orderlist-idrefs-attribute-value"></a>B. Recuperar elementos en función del valor del atributo IDREFS OrderList  
 En el ejemplo siguiente, el atributo OrderList del elemento <`Customer`> es de tipo IDREFS. Enumera los Id. de orden del cliente en cuestión. Por cada id. de orden, existe un elemento secundario <`Order`> debajo del elemento <`Customer`> que proporciona el valor de orden.  
  
 La expresión de consulta, `data(CustOrders:Customers/Customer[1]/@OrderList)[1]`, recupera el primer valor de la lista IDRES para el primer cliente. Este valor, a continuación, se pasa a la **ID** función. La función, a continuación, busca el <`Order`> elemento cuyo valor de atributo OrderID coincide con la entrada a la **ID** función.  
  
```  
drop xml schema collection SC  
go  
create xml schema collection SC as  
'<schema xmlns="http://www.w3.org/2001/XMLSchema" xmlns:Customers="Customers" targetNamespace="Customers">  
            <element name="Customers" type="Customers:CustomersType"/>  
            <complexType name="CustomersType">  
                        <sequence>  
                            <element name="Customer" type="Customers:CustomerType" minOccurs="0" maxOccurs="unbounded" />  
                        </sequence>  
            </complexType>  
             <complexType name="OrderType">  
                <sequence minOccurs="0" maxOccurs="unbounded">  
                            <choice>  
                                <element name="OrderValue" type="integer" minOccurs="0" maxOccurs="unbounded"/>  
                            </choice>  
                </sequence>                                             
                <attribute name="OrderID" type="ID" />  
            </complexType>  
  
            <complexType name="CustomerType">  
                <sequence minOccurs="0" maxOccurs="unbounded">  
                            <choice>  
                                <element name="spouse" type="string" minOccurs="0" maxOccurs="unbounded"/>  
                                <element name="Order" type="Customers:OrderType" minOccurs="0" maxOccurs="unbounded"/>  
                            </choice>  
                </sequence>                                             
                <attribute name="CustomerID" type="string" />  
                <attribute name="OrderList" type="IDREFS" />  
            </complexType>  
 </schema>'  
go  
declare @x xml(SC)  
set @x='<CustOrders:Customers xmlns:CustOrders="Customers">  
                <Customer CustomerID="C1" OrderList="OrderA OrderB"  >  
                              <spouse>Jenny</spouse>  
                                <Order OrderID="OrderA"><OrderValue>11</OrderValue></Order>  
                                <Order OrderID="OrderB"><OrderValue>22</OrderValue></Order>  
  
                </Customer>  
                <Customer CustomerID="C2" OrderList="OrderC OrderD" >  
                                <spouse>John</spouse>  
                                <Order OrderID="OrderC"><OrderValue>33</OrderValue></Order>  
                                <Order OrderID="OrderD"><OrderValue>44</OrderValue></Order>  
  
                        </Customer>  
                <Customer CustomerID="C3"  OrderList="OrderE OrderF" >  
                                <spouse>Jane</spouse>  
                                <Order OrderID="OrderE"><OrderValue>55</OrderValue></Order>  
                                <Order OrderID="OrderF"><OrderValue>55</OrderValue></Order>  
                </Customer>  
                <Customer CustomerID="C4"  OrderList="OrderG"  >  
                                <spouse>Tim</spouse>  
                                <Order OrderID="OrderG"><OrderValue>66</OrderValue></Order>  
                        </Customer>  
                <Customer CustomerID="C5"  >  
                </Customer>  
                <Customer CustomerID="C6" >  
                </Customer>  
                <Customer CustomerID="C7"  >  
                </Customer>  
</CustOrders:Customers>'  
select @x.query('declare namespace CustOrders="Customers";  
  id(data(CustOrders:Customers/Customer[1]/@OrderList)[1])')  
  
-- result  
<Order OrderID="OrderA">  
  <OrderValue>11</OrderValue>  
</Order>  
```  
  
### <a name="implementation-limitations"></a>Limitaciones de la implementación  
 Éstas son las limitaciones:  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no se admite la versión de dos argumentos de **ID**.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] requiere que el tipo de argumento de **ID** para ser un subtipo de xs: IDREF *.  
  
## <a name="see-also"></a>Vea también  
 [Funciones usadas en secuencias](http://msdn.microsoft.com/library/672d2795-53ab-49c2-bf24-bc81a47ecd3f)  
  
  
