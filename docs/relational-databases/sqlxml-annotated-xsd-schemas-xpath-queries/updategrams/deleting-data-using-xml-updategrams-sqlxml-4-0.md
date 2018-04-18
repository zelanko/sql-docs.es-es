---
title: Eliminar datos con diagramas de actualización XML (SQLXML 4.0) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- <after> block
- updategrams [SQLXML], deleting data
- <before> block
- mapping-schema attribute
- record deletions [SQLXML]
ms.assetid: 4fb116d7-7652-474a-a567-cb475a20765c
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 9d71554373fab48fe3636500a70c800d66ec9863
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="deleting-data-using-xml-updategrams-sqlxml-40"></a>Eliminar datos con diagramas de actualización XML (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Un diagrama de actualización indica una operación de eliminación cuando una instancia de registro aparece en el  **\<antes >** bloque con ningún registro correspondiente en el  **\<después >** bloque. En este caso, el diagrama de actualización elimina el registro en el  **\<antes >** bloque desde la base de datos.  
  
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
  
 Puede omitir el  **\<después >** etiqueta si el diagrama de actualización está realizando una operación de eliminación. Si no se especifica la parte opcional **esquema de asignación** atributo, el  **\<ElementName >** especificado en el diagrama de actualización se asigna a una tabla de base de datos y la asignación de elementos o atributos secundarios a columnas de la tabla.  
  
 Si un elemento especificado en el diagrama de actualización coincide con más de una fila en la tabla o no coincide con ninguna fila, el diagrama de actualización devuelve un error y se cancela todo el  **\<sincronización >** bloque. Un elemento del diagrama de actualización solamente puede eliminar un registro a la vez.  
  
## <a name="examples"></a>Ejemplos  
 Los ejemplos de esta sección utilizan una asignación predeterminada (es decir, no se especifica ningún esquema de asignación en el diagrama de actualización). Para obtener más ejemplos de los diagramas de actualización que utilizan los esquemas de asignación, consulte [especificar un esquema de asignación anotados en un diagrama de actualización &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
 Para crear ejemplos funcionales mediante los siguientes ejemplos, debe cumplir los requisitos especificados en [requisitos para ejecutar los ejemplos de SQLXML](../../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-deleting-a-record-by-using-an-updategram"></a>A. Eliminar un registro mediante un diagrama de actualización  
 Los siguientes diagramas de actualización eliminan dos registros de la tabla HumanResources.Shift.  
  
 En estos ejemplos, el diagrama de actualización no especifica ningún esquema de asignación. Por tanto, el diagrama de actualización utiliza la asignación predeterminada, en la que el nombre de elemento se asigna a un nombre de tabla y los atributos o subelementos se asignan a columnas.  
  
 Este primer diagrama de actualización está centrado en atributos e identifica dos turnos (Day-Evening y Evening-Night) en el  **\<antes >** bloque. Porque no hay ningún registro correspondiente en el  **\<después >** bloque, se trata de una operación de eliminación.  
  
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
  
1.  Complete el ejemplo B ("insertar varios registros utilizando un diagrama de actualización") en [insertar datos utilizando XML los diagramas de actualización &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md).  
  
2.  Copie el diagrama de actualización anterior en el Bloc de notas y guárdelo como Updategram-RemoveShifts.xml en la misma carpeta que se utilizó para completar ("insertar varios registros utilizando un diagrama de actualización") en [insertar datos utilizando XML los diagramas de actualización &#40;SQLXML 4.0&#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md).  
  
3.  Cree y use el script de prueba de SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar el diagrama de actualización.  
  
     Para obtener más información, consulte [utilizar ADO para ejecutar consultas de SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
## <a name="see-also"></a>Vea también  
 [Consideraciones de seguridad de updategram &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
