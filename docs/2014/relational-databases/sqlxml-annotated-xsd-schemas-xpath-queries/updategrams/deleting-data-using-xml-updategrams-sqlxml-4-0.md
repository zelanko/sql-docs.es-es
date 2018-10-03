---
title: Eliminar datos con diagramas de actualización XML (SQLXML 4.0) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- <after> block
- updategrams [SQLXML], deleting data
- <before> block
- mapping-schema attribute
- record deletions [SQLXML]
ms.assetid: 4fb116d7-7652-474a-a567-cb475a20765c
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9d16d27583854988a6e937c0859239875e15616f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48220305"
---
# <a name="deleting-data-using-xml-updategrams-sqlxml-40"></a>Eliminar datos con diagramas de actualización XML (SQLXML 4.0)
  Un diagrama de actualización indica una operación de eliminación cuando una instancia de registro aparece en el  **\<antes >** bloque sin ningún registro correspondiente en el  **\<después >** bloque. En este caso, el diagrama de actualización elimina el registro en el  **\<antes >** bloque desde la base de datos.  
  
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
  
 Puede omitir el  **\<después >** si el diagrama de actualización realiza solo una operación de eliminación de etiquetas. Si no especifica el elemento opcional `mapping-schema` atributo, el  **\<ElementName >** especificado en el diagrama de actualización se asigna a una tabla de base de datos y lo secundarios elementos o atributos se asignan a columnas de la tabla.  
  
 Si un elemento especificado en el diagrama de actualización coincide con más de una fila en la tabla o no coincide con ninguna fila, el diagrama de actualización devuelve un error y cancela todo el  **\<sincronización >** bloque. Un elemento del diagrama de actualización solamente puede eliminar un registro a la vez.  
  
## <a name="examples"></a>Ejemplos  
 Los ejemplos de esta sección utilizan una asignación predeterminada (es decir, no se especifica ningún esquema de asignación en el diagrama de actualización). Para obtener más ejemplos de diagramas de actualización que utilizan los esquemas de asignación, consulte [especificar un esquema de asignación anotados en un diagrama de actualización &#40;SQLXML 4.0&#41;](specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
 Para crear ejemplos funcionales mediante los siguientes ejemplos, debe cumplir los requisitos especificados en [requisitos para ejecutar los ejemplos de SQLXML](../../sqlxml/requirements-for-running-sqlxml-examples.md).  
  
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
  
1.  Complete el ejemplo B ("insertar varios registros utilizando un diagrama de actualización") en [Updategrams de inserción de datos utilizando XML &#40;SQLXML 4.0&#41;](inserting-data-using-xml-updategrams-sqlxml-4-0.md).  
  
2.  Copie el diagrama de actualización anterior en el Bloc de notas y guárdelo como Updategram-RemoveShifts.xml en la misma carpeta que utilizó para completar ("insertar varios registros utilizando un diagrama de actualización") en [Updategrams de inserción de datos utilizando XML &#40;SQLXML 4.0&#41; ](inserting-data-using-xml-updategrams-sqlxml-4-0.md).  
  
3.  Cree y use el script de prueba de SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar el diagrama de actualización.  
  
     Para obtener más información, consulte [utilizar ADO para ejecutar consultas de SQLXML 4.0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
## <a name="see-also"></a>Vea también  
 [Consideraciones de seguridad de updategram &#40;SQLXML 4.0&#41;](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
