---
title: Problemas de simultaneidad de bases de datos en diagramas (SQLXML)
description: Aprenda a usar el mecanismo de control de simultaneidad optimista en diagramas (SQLXML 4,0) para controlar los problemas de simultaneidad de bases de datos.
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- <before> block
- low concurrency protection
- database concurrency [SQLXML]
- timestamp column [SQLXML]
- updategrams [SQLXML], database concurrency
- high concurrency protection [SQLXML]
- optimistic concurrency control
- concurrency [SQLXML]
- intermediate concurrency protection [SQLXML]
ms.assetid: d4b908d1-b25b-4ad9-8478-9cd882e8c44e
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 11e4a7a875dd2c9b9450619f389b2f082136c536
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85790587"
---
# <a name="handling-database-concurrency-issues-in-updategrams-sqlxml-40"></a>Controlar problemas de simultaneidad de base de datos en diagramas de actualización (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  Al igual que otros mecanismos de actualización de base de datos, los diagramas de actualización deben lidiar con actualizaciones simultáneas de datos en un entorno multiusuario. Los diagramas de actualización usan el control de simultaneidad optimista, que usa la comparación de datos de campos de selección como instantáneas para asegurarse de que otra aplicación de usuario no haya modificado los datos que van a actualizarse desde que se leyeron de la base de datos. Diagramas incluye estos valores de instantánea en el **\<before>** bloque de diagramas. Antes de actualizar la base de datos, diagrama comprueba los valores especificados en el **\<before>** bloque con los valores que hay actualmente en la base de datos para asegurarse de que la actualización es válida.  
  
 El control de simultaneidad optimista ofrece tres niveles de protección en un diagrama de actualización: bajo (ninguno), intermedio y alto. Puede decidir qué nivel de protección necesita especificando el diagrama de actualización en consecuencia.  
  
## <a name="lowest-level-of-protection"></a>Nivel de protección más bajo  
 Este nivel es en realidad una actualización “ciega”, donde la actualización se procesa sin hacer referencia a otras actualizaciones que se hayan realizado desde que la base de datos se leyó por última vez. En tal caso, solo se especifican las columnas de clave principal en el **\<before>** bloque para identificar el registro y se especifica la información actualizada en el **\<after>** bloque.  
  
 Por ejemplo, el nuevo número de teléfono del contacto en el diagrama de actualización siguiente es correcto, independientemente de cuál fuera el número de teléfono anterior. Observe cómo el **\<before>** bloque especifica únicamente la columna de clave principal (ContactID).  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
<updg:before>  
   <Person.Contact ContactID="1" />  
</updg:before>  
<updg:after>  
   <Person.Contact ContactID="1" Phone="111-111-1111" />  
</updg:after>  
</updg:sync>  
</ROOT>  
```  
  
## <a name="intermediate-level-of-protection"></a>Nivel de protección intermedio  
 En este nivel de protección, el diagrama de actualización compara los valores actuales de los datos que se están actualizando con los valores de las columnas de la base de datos para asegurarse de que ninguna otra transacción los haya modificado desde que la transacción del usuario leyó el registro.  
  
 Puede obtener este nivel de protección si especifica las columnas de clave principal y las columnas que se van a actualizar en el **\<before>** bloque.  
  
 Por ejemplo, este diagrama de actualización cambia el valor de la columna Phone de la tabla Person.Contact para el contacto cuyo ContactID es igual a 1. El **\<before>** bloque especifica el atributo **Phone** para asegurarse de que este valor de atributo coincide con el valor de la columna correspondiente en la base de datos antes de aplicar el valor actualizado.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
<updg:before>  
   <Person.Contact ContactID="1" Phone="398-555-0132" />  
</updg:before>  
<updg:after>  
   <Person.Contact ContactID="1" Phone="111-111-1111" />  
</updg:after>  
</updg:sync>  
</ROOT>  
```  
  
## <a name="high-level-of-protection"></a>Nivel de protección alto  
 Un nivel de protección alto se asegura de que el registro sigue siendo el mismo desde que la aplicación lo leyó por última vez (es decir, desde que la aplicación leyó el registro, ninguna otra transacción lo ha modificado).  
  
 Existen dos formas de obtener este nivel de protección alto en las actualizaciones simultáneas:  
  
-   Especifique columnas adicionales en la tabla en el **\<before>** bloque.  
  
     Si especifica columnas adicionales en el **\<before>** bloque, diagrama compara los valores especificados para estas columnas con los valores que estaban en la base de datos antes de aplicar la actualización. Si alguna de las columnas del registro ha cambiado desde que la transacción leyó el registro, el diagrama de actualización no realizará la actualización.  
  
     Por ejemplo, el siguiente diagrama actualiza el nombre de desplazamiento, pero especifica columnas adicionales (StartTime, EndTime) en el **\<before>** bloque, lo que solicita un mayor nivel de protección frente a las actualizaciones simultáneas.  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
    <updg:sync >  
    <updg:before>  
       <HumanResources.Shift ShiftID="1"   
                 Name="Day"   
                 StartTime="1900-01-01 07:00:00.000"   
                 EndTime="1900-01-01 15:00:00.000" />  
    </updg:before>  
    <updg:after>  
       <HumanResources.Shift Name="Morning" />  
    </updg:after>  
    </updg:sync>  
    </ROOT>  
    ```  
  
     Este ejemplo especifica el nivel de protección más alto especificando todos los valores de columna del registro en el **\<before>** bloque.  
  
-   Especifique la columna de marca de tiempo (si está disponible) en el **\<before>** bloque.  
  
     En lugar de especificar todas las columnas de registro en el bloque * * \<before**> , solo puede especificar la columna de marca de tiempo (si la tabla tiene una) junto con las columnas de clave principal en el **\<before>** bloque. La base de datos actualizará la columna de marca de tiempo a un valor único tras cada actualización del registro. En este caso, el diagrama de actualización compara el valor de la marca de tiempo con el valor correspondiente de la base de datos. El valor de marca de tiempo almacenado en la base de datos es un valor binario. Por lo tanto, la columna TIMESTAMP debe especificarse en el esquema como **DT: type = "bin. hex"**, **DT: type = "bin. base64"** o **SQL: DataType = "timestamp"**. (Puede especificar el tipo de datos **XML** o el [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipo de datos).  
  
#### <a name="to-test-the-updategram"></a>Para probar el diagrama de actualización  
  
1.  Cree esta tabla en la base de datos **tempdb** :  
  
    ```  
    USE tempdb  
    CREATE TABLE Customer (  
                 CustomerID  varchar(5),  
                 ContactName varchar(20),  
                 LastUpdated timestamp)  
    ```  
  
2.  Agregue este registro de ejemplo:  
  
    ```  
    INSERT INTO Customer (CustomerID, ContactName) VALUES   
                         ('C1', 'Andrew Fuller')  
    ```  
  
3.  Copie el siguiente esquema XSD y péguelo en el Bloc de notas. Guárdelo como ConcurrencySampleSchema.xml:  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
      <xsd:element name="Customer" sql:relation="Customer" >  
       <xsd:complexType>  
            <xsd:attribute name="CustomerID"    
                           sql:field="CustomerID"   
                           type="xsd:string" />   
  
            <xsd:attribute name="ContactName"    
                           sql:field="ContactName"   
                           type="xsd:string" />  
  
            <xsd:attribute name="LastUpdated"   
                           sql:field="LastUpdated"   
                           type="xsd:hexBinary"   
                 sql:datatype="timestamp" />  
  
        </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
4.  Copie el código del diagrama de actualización siguiente en Bloc de notas y guárdelo como ConcurrencySampleTemplate.xml en el mismo directorio donde guardó el esquema creado en el paso anterior. (Tenga en cuenta que el siguiente valor de marca de tiempo de LastUpdated variará con respecto a su tabla Customer de ejemplo, de modo que debe copiar el valor real de LastUpdated de la tabla y pegarlo en el diagrama de actualización.)  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
    <updg:sync mapping-schema="SampleSchema.xml" >  
    <updg:before>  
       <Customer CustomerID="C1"   
                 LastUpdated = "0x00000000000007D1" />  
    </updg:before>  
    <updg:after>  
       <Customer ContactName="Robert King" />  
    </updg:after>  
    </updg:sync>  
    </ROOT>  
    ```  
  
5.  Cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar la plantilla.  
  
     Para obtener más información, vea [usar ado para ejecutar consultas SQLXML 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Éste es el esquema XDR equivalente:  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:dt="urn:schemas-microsoft-com:datatypes"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
<ElementType name="Customer" sql:relation="Customer" >  
    <AttributeType name="CustomerID" />  
    <AttributeType name="ContactName" />  
    <AttributeType name="LastUpdated"  dt:type="bin.hex"   
                                       sql:datatype="timestamp" />  
    <attribute type="CustomerID" />  
    <attribute type="ContactName" />  
    <attribute type="LastUpdated" />  
</ElementType>  
</Schema>  
```  
  
## <a name="see-also"></a>Consulte también  
 [Consideraciones de seguridad de diagrama &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
