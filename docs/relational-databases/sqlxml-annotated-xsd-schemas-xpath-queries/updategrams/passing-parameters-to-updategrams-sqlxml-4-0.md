---
title: Pasar parámetros a diagramas de actualización (SQLXML 4.0) | Microsoft Docs
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
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5359edb43af047edaf2a061b33aeeb7baaac78f3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47635473"
---
# <a name="passing-parameters-to-updategrams-sqlxml-40"></a>Pasar parámetros a diagramas de actualización (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Los diagramas de actualización son plantillas; por consiguiente, se les pueden pasar parámetros. Para obtener más información sobre cómo pasar parámetros a plantillas, consulte [consideraciones de seguridad de Updategram &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md).  
  
 Los diagramas de actualización le permiten pasar NULL como un valor del parámetro. Para pasar el valor del parámetro es NULL, especifique el **nullvalue** atributo. El valor que se asigna a la **nullvalue** atributo, a continuación, se proporciona como el valor del parámetro. Los diagramas de actualización tratan este valor como NULL.  
  
> [!NOTE]  
>  En  **\<sql:header >** y  **\<updg:header >**, debe especificar el **nullvalue** como no calificado; mientras que, en  **\<updg:sync >**, especifique el **nullvalue** como completo (por ejemplo, **updg:nullvalue**).  
  
## <a name="examples"></a>Ejemplos  
 Para crear ejemplos funcionales mediante los siguientes ejemplos, debe cumplir los requisitos especificados en [requisitos para ejecutar los ejemplos de SQLXML](../../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
 Antes de usar los ejemplos del diagrama de actualización, tenga en cuenta lo siguiente:  
  
-   En los ejemplos se usa una asignación predeterminada (es decir, ningún esquema de asignación se especifica en el diagrama de actualización). Para obtener más ejemplos de diagramas de actualización que utilizan los esquemas de asignación, consulte [especificar un esquema de asignación anotados en un diagrama de actualización &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
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
  
2.  Prepare el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) en [utilizar ADO para ejecutar consultas de SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md) para ejecutar el diagrama de actualización agregando las líneas siguientes después de la `cmd.Properties("Output Stream").Value = outStream`:  
  
    ```  
    cmd.NamedParameters = True  
    ' CreateParameter arguments: Name, Type, Direction, Size, Value  
    cmd.Parameters.Append cmd.CreateParameter("@ShiftID",  2, 1,  0, 1)  
    cmd.Parameters.Append cmd.CreateParameter("@Name",   200, 1, 50, "New Name")  
    ```  
  
### <a name="b-passing-null-as-a-parameter-value-to-an-updategram"></a>B. Pasar NULL como un valor del parámetro a un diagrama de actualización  
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
  
2.  Prepare el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) en [utilizar ADO para ejecutar consultas de SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md) para ejecutar el diagrama de actualización agregando las líneas siguientes después de la `cmd.Properties("Output Stream").Value = outStream`:  
  
    ```  
    cmd.NamedParameters = True  
    ' CreateParameter arguments: Name, Type, Direction, Size, Value   
    cmd.Parameters.Append cmd.CreateParameter("@EmployeeID", 3, 1, 0, 1)  
    cmd.Parameters.Append cmd.CreateParameter("@ManagerID",  3, 1, 0, Null)  
    ```  
  
## <a name="see-also"></a>Vea también  
 [Consideraciones de seguridad de updategram &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
