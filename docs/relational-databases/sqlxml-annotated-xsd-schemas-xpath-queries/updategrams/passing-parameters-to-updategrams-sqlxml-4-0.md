---
title: Pasar parámetros a diagramas (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- nullvalue attribute
- passing parameters [SQLXML]
- parameters [SQLXML]
- updategrams [SQLXML], passing parameters
- null values [SQLXML]
ms.assetid: 2354e6e7-1860-471f-8711-4e374c5a4ed2
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fc2617796c5abf7f94e85fc6397b780ea9c401c4
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907830"
---
# <a name="passing-parameters-to-updategrams-sqlxml-40"></a>Pasar parámetros a diagramas de actualización (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Los diagramas de actualización son plantillas; por consiguiente, se les pueden pasar parámetros. Para obtener más información sobre cómo pasar parámetros a plantillas, vea [Diagrama &#40;Security considerations SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md).  
  
 Los diagramas de actualización le permiten pasar NULL como un valor del parámetro. Para pasar el valor de parámetro NULL, especifique el atributo **NullValue** . El valor que se asigna al atributo **NullValue** se proporciona como el valor del parámetro. Los diagramas de actualización tratan este valor como NULL.  
  
> [!NOTE]  
>  En **\<SQL: header >** y **\<atributo updg: header >** , debe especificar el **NullValue** como Unqualified. mientras que en **\<atributo updg: sync >** , se especifica **NullValue** como Qualified (por ejemplo, **atributo updg: NullValue**).  
  
## <a name="examples"></a>Ejemplos  
 Para crear ejemplos funcionales mediante los ejemplos siguientes, debe cumplir los requisitos especificados en [requisitos para ejecutar ejemplos de SQLXML](../../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
 Antes de usar los ejemplos del diagrama de actualización, tenga en cuenta lo siguiente:  
  
-   En los ejemplos se usa una asignación predeterminada (es decir, ningún esquema de asignación se especifica en el diagrama de actualización). Para obtener más ejemplos de diagramas que usan esquemas de asignación, vea [especificar un esquema de asignación anotado en &#40;un diagrama&#41;SQLXML 4,0](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
### <a name="a-passing-parameters-to-an-updategram"></a>A. Pasar parámetros a un diagrama de actualización  
 En este ejemplo, el diagrama de actualización cambia el apellido de un empleado en la tabla HumanResources.Shift. Se pasan dos parámetros al diagrama de actualización: ShiftID, que se usa para identificar de manera única un cambio, y Nombre.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:header>  
  <updg:param name="ShiftID"/>  
  <updg:param name="Name" />  
</updg:header>  
  <updg:sync >  
    <updg:before>  
       <HumanResources.Shift ShiftID="$ShiftID" />  
    </updg:before>  
    <updg:after>  
      <HumanResources.Shift Name="$Name" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>Para probar el diagrama de actualización  
  
1.  Copie el diagrama de actualización anterior en el Bloc de notas y guárdelo en un archivo como UpdategramWithParameters.xml.  
  
2.  Prepare el script SQLXML 4,0 test (Sqlxml4test. vbs) en [usar ado para ejecutar consultas sqlxml 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md) para ejecutar el diagrama agregando las siguientes líneas después de la `cmd.Properties("Output Stream").Value = outStream`:  

    ```  
    cmd.NamedParameters = True  
    ' CreateParameter arguments: Name, Type, Direction, Size, Value  
    cmd.Parameters.Append cmd.CreateParameter("@ShiftID",  2, 1,  0, 1)  
    cmd.Parameters.Append cmd.CreateParameter("@Name",   200, 1, 50, "New Name")  
    ```  
  
### <a name="b-passing-null-as-a-parameter-value-to-an-updategram"></a>b. Pasar NULL como un valor del parámetro a un diagrama de actualización  
 Para ejecutar un diagrama de actualización, el valor "isnull" se asigna al parámetro que se desea establecer en NULL. El diagrama de actualización convierte el valor del parámetro "isnulll" en NULL y lo procesa de forma apropiada.  
  
 El diagrama de actualización siguiente establece un puesto de empleado en NULL:  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:header nullvalue="isnull" >  
  <updg:param name="EmployeeID"/>  
  <updg:param name="ManagerID" />  
</updg:header>  
  <updg:sync >  
    <updg:before>  
       <HumanResources.Employee EmployeeID="$EmployeeID" />  
    </updg:before>  
    <updg:after>  
      <HumanResources.Employee ManagerID="$ManagerID" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>Para probar el diagrama de actualización  
  
1.  Copie el diagrama de actualización anterior en el Bloc de notas y guárdelo en un archivo como UpdategramPassingNullvalues.xml.  
  
2.  Prepare el script SQLXML 4,0 test (Sqlxml4test. vbs) en [usar ado para ejecutar consultas sqlxml 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md) para ejecutar el diagrama agregando las siguientes líneas después de la `cmd.Properties("Output Stream").Value = outStream`:  
  
    ```  
    cmd.NamedParameters = True  
    ' CreateParameter arguments: Name, Type, Direction, Size, Value   
    cmd.Parameters.Append cmd.CreateParameter("@EmployeeID", 3, 1, 0, 1)  
    cmd.Parameters.Append cmd.CreateParameter("@ManagerID",  3, 1, 0, Null)  
    ```  
  
## <a name="see-also"></a>Ver también  
 [Consideraciones &#40;de seguridad de diagrama SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
