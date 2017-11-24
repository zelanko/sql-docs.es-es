---
title: "Introducción a los diagramas de actualización (SQLXML 4.0) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- explicit schema mapping [SQLXML]
- updategrams [SQLXML], mapping schema specifying
- namespaces [SQLXML]
- updategrams [SQLXML], about updategrams
- attribute-centric mapping
- invalid characters [SQLXML]
- element-centric mapping [SQLXML]
- mapping schema [SQLXML], updategrams
- namespaces [SQLXML], updategrams
- executing updategrams [SQLXML]
- implicit schema mapping
ms.assetid: cfe24e82-a645-4f93-ab16-39c21f90cce6
caps.latest.revision: "12"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7b5a9ef6b56ee32f31b277273fb644a03925fdf0
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="introduction-to-updategrams-sqlxml-40"></a>Introducción a los diagramas de actualización (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]Puede modificar (Insertar, actualizar o eliminar) una base de datos en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] desde un documento XML de documento mediante un diagrama de actualización o el OPENXML [!INCLUDE[tsql](../../../includes/tsql-md.md)] función.  
  
 La función OPENXML modifica una base de datos dividiendo el documento XML existente y proporcionando un conjunto de filas que puede pasarse a una instrucción INSERT, UPDATE o DELETE. Con OPENXML, las operaciones se realizan directamente en las tablas de la base de datos. Por lo tanto, el uso de OPENXML resulta más adecuado siempre que los proveedores de conjuntos de filas, como una tabla, puedan aparecer como un origen.  
  
 Al igual que OPENXML, un diagrama de actualización permite insertar, actualizar o eliminar datos en la base de datos; sin embargo, un diagrama de actualización funciona con las vistas XML proporcionadas por el esquema XSD (o XDR) anotado; por ejemplo, las actualizaciones se aplican a la vista XML proporcionada por el esquema de asignación. El esquema de asignación, a su vez, incluye la información necesaria para asignar elementos y atributos XML a las columnas y tablas de base de datos correspondientes. El diagrama de actualización usa esta información de asignación para actualizar las columnas y tablas de base de datos.  
  
> [!NOTE]  
>  En esta documentación se asume que está familiarizado con la compatibilidad de las plantillas y el esquema de asignación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obtener más información, vea [Introducción a los esquemas XSD anotados &#40; SQLXML 4.0 &#41; ](../../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md). Para obtener información sobre las aplicaciones heredadas que usan XDR, vea [esquemas XDR anotados &#40; funcionalidades desusadas en SQLXML 4.0 &#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md).  
  
## <a name="required-namespaces-in-the-updategram"></a>Espacios de nombres necesarios en el diagrama de actualización  
 Las palabras clave en un diagrama de actualización, como  **\<sincronización >**,  **\<antes >**, y  **\<después >**, existe en el **urn: schemas-microsoft-com: diagrama de actualización** espacio de nombres. Se usa un prefijo de espacio de nombres arbitrario. En esta documentación, el **updg** prefijo denota el **updategram** espacio de nombres.  
  
## <a name="reviewing-syntax"></a>Revisar la sintaxis  
 Un diagrama de actualización es una plantilla con  **\<sincronización >**,  **\<antes >**, y  **\<después >** bloques que forman la sintaxis de la diagrama de actualización. El código siguiente muestra esta sintaxis en su forma más simple:  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync [mapping-schema= "AnnotatedSchemaFile.xml"] >  
    <updg:before>  
        ...  
    </updg:before>  
    <updg:after>  
        ...  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 Las definiciones siguientes describen el rol de cada uno de estos bloques:  
  
 **\<antes de >**  
 Identifica el estado existente (que también recibe el nombre de "estado before") de la instancia de registro.  
  
 **\<una vez >**  
 Identifica el nuevo estado al que van a cambiarse los datos.  
  
 **\<sincronización >**  
 Contiene el  **\<antes >** y  **\<después >** bloques. A  **\<sincronización >** bloque puede contener más de un conjunto de  **\<antes >** y  **\<después >** bloques. Si hay más de un conjunto de  **\<antes >** y  **\<después >** bloques, estos bloques (incluso si están vacías) debe especificarse como pares. Además, un diagrama de actualización puede tener más de un  **\<sincronización >** bloque. Cada  **\<sincronización >** bloque es una unidad de transacción (lo que significa que cualquier todo el contenido de la  **\<sincronización >** bloque se realiza o no se hace nada). Si especifica varios  **\<sincronización >** bloques en un diagrama de actualización, el error de un  **\<sincronización >** bloque no afecta a los demás  **\<sincronización >** bloques.  
  
 Si un diagrama de actualización elimina, inserta o actualiza una instancia de registro depende del contenido de la  **\<antes >** y  **\<después >** bloques:  
  
-   Si una instancia de registro solamente aparece en el  **\<antes >** bloque sin ninguna instancia correspondiente en el  **\<después >** bloque, el diagrama de actualización realiza una operación de eliminación.  
  
-   Si una instancia de registro solamente aparece en el  **\<después >** bloque sin ninguna instancia correspondiente en el  **\<antes de >** bloque, que es una operación de inserción.  
  
-   Si una instancia de registro aparece en el  **\<antes de >** bloquear y tiene una instancia correspondiente el  **\<después >** bloque, que es una operación de actualización. En este caso, el diagrama de actualización actualiza la instancia de registro para los valores que se especifican en el  **\<después >** bloque.  
  
## <a name="specifying-a-mapping-schema-in-the-updategram"></a>Especificar un esquema de asignación en el diagrama de actualización  
 En un diagrama de actualización, la abstracción XML que se proporciona con un esquema de asignación (se admiten tanto esquemas XSD como esquemas XDR) puede ser implícita o explícita (es decir, un diagrama de actualización puede funcionar con o sin un esquema de asignación especificado). Si no especifica un esquema de asignación, el diagrama de actualización asume una asignación implícita (la asignación predeterminada), donde cada elemento de la  **\<antes >** bloque o  **\<después >** bloque que se asigna a una tabla y secundario del elemento cada elemento o atributo se asigna a una columna de la base de datos. Si especifica explícitamente un esquema de asignación, los elementos y atributos del diagrama de actualización deben coincidir con los elementos y los atributos del esquema de asignación.  
  
### <a name="implicit-default-mapping"></a>Asignación implícita (predeterminada)  
 En la mayoría de los casos, es posible que un diagrama de actualización que realiza actualizaciones simples no requiera un esquema de asignación. En este caso, el diagrama de actualización se basa en el esquema de asignación predeterminado.  
  
 En el diagrama de actualización siguiente se muestra una asignación implícita. En este ejemplo, el diagrama de actualización inserta un nuevo cliente en la tabla Sales.Customer. Dado que este diagrama de actualización usa una asignación implícita, el \<Sales.Customer > elemento se asigna a la tabla Sales.Customer y los atributos CustomerID y SalesPersonID se asignan a las columnas correspondientes en la tabla Sales.Customer.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
<updg:before>  
</updg:before>  
<updg:after>  
    <Sales.Customer CustomerID="1" SalesPersonID="277" />  
    </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
### <a name="explicit-mapping"></a>Asignación explícita  
 Si especifica un esquema de asignación (ya sea XSD o XDR), el diagrama de actualización usa dicho esquema para determinar las columnas y las tablas de base de datos que van a actualizarse.  
  
 Si el diagrama de actualización realiza una actualización compleja (por ejemplo, insertando registros en varias tablas basándose en la relación de elementos primarios y secundarios que se especifica en el esquema de asignación), debe proporcionar explícitamente el esquema de asignación mediante la  **esquema de asignación** atributo en que se ejecuta el diagrama de actualización.  
  
 Dado que un diagrama de actualización es una plantilla, la ruta de acceso especificada para el esquema de asignación en el diagrama de actualización es relativa a la ubicación del archivo de plantilla (con respecto al lugar donde se almacena el diagrama de actualización). Para obtener más información, vea [especificar un esquema de asignación anotados en un diagrama de actualización &#40; SQLXML 4.0 &#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
## <a name="element-centric-and-attribute-centric-mapping-in-updategrams"></a>Asignación centrada en elementos y centrada en atributos en diagramas de actualización  
 Con la asignación predeterminada (cuando el esquema de asignación no se especifica en el diagrama de actualización), los elementos del diagrama de actualización se asignan a tablas y los elementos secundarios (en el caso de la asignación centrada en elementos) y los atributos (en el caso de asignación centrada en atributos) se asignan a columnas.  
  
### <a name="element-centric-mapping"></a>Asignación centrada en elementos  
 En un diagrama de actualización centrado en elementos, un elemento contiene elementos secundarios que denotan las propiedades del elemento. Como ejemplo, consulte el diagrama de actualización siguiente. El  **\<Person.Contact >** elemento contiene el  **\<FirstName >**y  **\<LastName >** los elementos secundarios. Estos elementos secundarios son propiedades de la  **\<Person.Contact >** elemento.  
  
 Dado que este diagrama de actualización no especifica un esquema de asignación, el diagrama de actualización usa una asignación implícita, donde el  **\<Person.Contact >** elemento se asigna a la tabla Person.Contact y sus elementos secundarios se asignan a la FirstName y Columnas LastName.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
  <updg:after>  
    <Person.Contact>  
       <FirstName>Catherine</FirstName>  
       <LastName>Abel</LastName>  
    </Person.Contact>  
  </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
### <a name="attribute-centric-mapping"></a>asignación centrada en atributos  
 En una asignación centrada en atributos, los elementos tienen atributos. El diagrama de actualización siguiente usa la asignación centrada en atributos. En este ejemplo, el  **\<Person.Contact >** elemento consta de los **FirstName** y **LastName** atributos. Estos atributos son las propiedades de la  **\<Person.Contact >** elemento. Como se muestra en el ejemplo anterior, este diagrama de actualización no especifica ningún esquema de asignación, de modo que se basa en la asignación implícita para asignar el  **\<Person.Contact >** elemento a la tabla Person.Contact y los atributos del elemento a la columnas respectivas de la tabla.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
  <updg:before>  
  </updg:before>  
  <updg:after>  
    <Person.Contact FirstName="Catherine" LastName="Abel" />  
  </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
### <a name="using-both-element-centric-and-attribute-centric-mapping"></a>Usar asignaciones centradas en elementos y centradas en atributos  
 Puede especificar una combinación de asignaciones centradas en elementos y asignaciones centradas en atributos, tal y como se muestra en el diagrama de actualización siguiente. Tenga en cuenta que la  **\<Person.Contact >** elemento contiene un atributo y un elemento secundario. Asimismo, este diagrama de actualización se basa en la asignación implícita. Por lo tanto, la **FirstName** atributo y el  **\<LastName >** se asignan a las columnas correspondientes de la tabla Person.Contact.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
  <updg:before>  
  </updg:before>  
  <updg:after>  
    <Person.Contact FirstName="Catherine" >  
       <LastName>Abel</LastName>  
    </Person.Contact>  
  </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
## <a name="working-with-characters-valid-in-sql-server-but-not-valid-in-xml"></a>Trabajar con caracteres que son válidos en SQL Server pero que no son válidos en XML  
 En [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], los nombres de tabla pueden incluir un espacio. Sin embargo, este tipo de nombre de tabla no es válido en XML.  
  
 Para codificar los caracteres que son válidos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] identificadores pero no son identificadores XML válidos, use ' __xHHHH\_\_' como valor de codificación, donde HHHH representa el código UCS-2 hexadecimal de cuatro dígitos para el carácter en el máximo primer bit más significativo. Con este esquema de codificación, un carácter de espacio se reemplaza con x0020 (lo cuatro dígitos código hexadecimal para un carácter de espacio); por lo tanto, el nombre de tabla [Order Details] en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se convierte en _x005B_Order_x0020_Details_x005D\_ en XML.  
  
 De igual forma, tendrá que especificar nombres de elemento de tres partes, como \<[base de datos]. [ propietario]. [tabla] >. Dado que los caracteres de corchete de cierre ([y]) no son válidos en XML, debe especificar esta información como \<_x005B_database_x005D\_._x005B_owner_x005D\_._x005B_table_x005D\_>, donde _x005B\_ es el codificación para el corchete de apertura ([) y _x005D\_ es la codificación para el corchete de cierre (]).  
  
## <a name="executing-updategrams"></a>Ejecutar diagramas de actualización  
 Dado que un diagrama de actualización es una plantilla, todos los mecanismos de procesamiento de una plantilla se aplican al diagrama de actualización. Para SQLXML 4.0, puede ejecutar un diagrama de actualización de cualquiera de las siguientes formas:  
  
-   Enviándolo en un comando ADO.  
  
-   Enviándolo como un comando OLE DB.  
  
## <a name="see-also"></a>Vea también  
 [Consideraciones de seguridad de diagrama de actualización &#40; SQLXML 4.0 &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
