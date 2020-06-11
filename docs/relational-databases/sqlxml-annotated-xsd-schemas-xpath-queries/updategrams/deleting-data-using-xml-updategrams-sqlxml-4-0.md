---
title: Eliminar datos mediante diagramas XML (SQLXML)
description: Obtenga información sobre cómo eliminar datos mediante una diagrama XML en SQLXML 4,0.
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- <after> block
- updategrams [SQLXML], deleting data
- <before> block
- mapping-schema attribute
- record deletions [SQLXML]
ms.assetid: 4fb116d7-7652-474a-a567-cb475a20765c
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f32c1107d886b7bc84590abbd6bab5343d2a2b8b
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/08/2020
ms.locfileid: "84529837"
---
# <a name="deleting-data-using-xml-updategrams-sqlxml-40"></a>Eliminar datos con diagramas de actualización XML (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Un diagrama indica una operación de eliminación cuando una instancia de registro aparece en el **\<before>** bloque sin registros correspondientes en el **\<after>** bloque. En este caso, el diagrama elimina el registro del **\<before>** bloque de la base de datos.  
  
 Éste es el formato del diagrama de actualización para una operación de eliminación:  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync [mapping-schema="SampleSchema.xml"]  >  
   <updg:before>  
       <ElementName />  
      [<ElementName .../>... ]  
   </updg:before>  
    [<updg:after>  
    </updg:after>]  
  </updg:sync>  
</ROOT>  
```  
  
 Puede omitir la **\<after>** etiqueta si diagrama está realizando solo una operación de eliminación. Si no especifica el atributo **mapping-schema** opcional, el **\<ElementName>** especificado en diagrama se asigna a una tabla de base de datos y los elementos secundarios o atributos se asignan a las columnas de la tabla.  
  
 Si un elemento especificado en diagrama coincide con más de una fila de la tabla o no coincide con ninguna fila, diagrama devuelve un error y cancela el **\<sync>** bloque completo. Un elemento del diagrama de actualización solamente puede eliminar un registro a la vez.  
  
## <a name="examples"></a>Ejemplos  
 Los ejemplos de esta sección utilizan una asignación predeterminada (es decir, no se especifica ningún esquema de asignación en el diagrama de actualización). Para obtener más ejemplos de diagramas que usan esquemas de asignación, vea [especificar un esquema de asignación anotado en un diagrama &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
 Para crear ejemplos funcionales mediante los ejemplos siguientes, debe cumplir los requisitos especificados en [requisitos para ejecutar ejemplos de SQLXML](../../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-deleting-a-record-by-using-an-updategram"></a>A. Eliminar un registro mediante un diagrama de actualización  
 Los siguientes diagramas de actualización eliminan dos registros de la tabla HumanResources.Shift.  
  
 En estos ejemplos, el diagrama de actualización no especifica ningún esquema de asignación. Por tanto, el diagrama de actualización utiliza la asignación predeterminada, en la que el nombre de elemento se asigna a un nombre de tabla y los atributos o subelementos se asignan a columnas.  
  
 Esta primera diagrama está centrada en atributos e identifica dos turnos (día y noche) en el **\<before>** bloque. Dado que no hay ningún registro correspondiente en el **\<after>** bloque, se trata de una operación de eliminación.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
  <updg:before>  
       <HumanResources.Shift ShiftID="4"  
                        Name="Day-Evening"  
                        StartTime="1900-01-01 11:00:00.000"  
                        EndTime="1900-01-01 19:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
       <HumanResources.Shift ShiftID="5"  
                        Name="Evening-Night"  
                        StartTime="1900-01-01 19:00:00.000"  
                        EndTime="1900-01-01 03:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
  </updg:before>  
  <updg:after>  
  </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>Para probar el diagrama de actualización  
  
1.  Complete el ejemplo B ("insertar varios registros mediante un diagrama") en la [inserción de datos mediante XML diagramas &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md).  
  
2.  Copie el diagrama anterior en el Bloc de notas y guárdelo como Updategram-RemoveShifts.xml en la misma carpeta que se usó para completar ("insertar varios registros mediante un diagrama") en la [inserción de datos con XML diagramas &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md).  
  
3.  Cree y use el script de prueba de SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar el diagrama de actualización.  
  
     Para obtener más información, vea [usar ado para ejecutar consultas SQLXML 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
## <a name="see-also"></a>Consulte también  
 [Consideraciones de seguridad de diagrama &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
