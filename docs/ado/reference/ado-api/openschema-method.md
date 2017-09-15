---
title: "Método OpenSchema | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Connection15::OpenSchema
- Connection15::raw_OpenSchema
helpviewer_keywords:
- OpenSchema method [ADO]
ms.assetid: 850cf3ce-f18f-4e7c-8597-96c1dc504866
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e5c547eb8a6c1208bedffb988096f45b4c871d09
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="openschema-method"></a>Método OpenSchema
Obtiene información de esquema de base de datos del proveedor.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Set recordset = connection.OpenSchema(QueryType, Criteria, SchemaID)  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto que contiene información de esquema. El **Recordset** se abrirá como un cursor estático de solo lectura. El *QueryType* determina qué columnas aparecen en la **conjunto de registros**.  
  
#### <a name="parameters"></a>Parámetros  
 *QueryType*  
 Cualquier [SchemaEnum](../../../ado/reference/ado-api/schemaenum.md) valor que representa el tipo de esquema que se va a ejecutar.  
  
 *Criterios*  
 Opcional. Una matriz de restricciones de consulta para cada *QueryType* opción, como se muestra en [SchemaEnum](../../../ado/reference/ado-api/schemaenum.md).  
  
 *SchemaID*  
 El GUID para una consulta de esquema del proveedor no definido por la especificación de OLE DB. Este parámetro es obligatorio si *QueryType* está establecido en **adSchemaProviderSpecific**; en caso contrario, no se utiliza.  
  
## <a name="remarks"></a>Comentarios  
 El **OpenSchema** método devuelve autodescriptiva información sobre el origen de datos, como qué son las tablas del origen de datos, las columnas en las tablas, y admiten los tipos de datos.  
  
 El *QueryType* argumento es un GUID que indica las columnas devueltas (esquemas). La especificación OLE DB tiene una lista completa de esquemas.  
  
 El *criterios* argumento limita los resultados de una consulta de esquema. *Criterios de* especifica una matriz de valores que se debe producir en un subconjunto de columnas, denominadas columnas de restricción, en el cuadro correspondiente **conjunto de registros**.  
  
 La constante **adSchemaProviderSpecific** se usa para la *QueryType* argumento si el proveedor define sus propias consultas de esquema no estándar fuera de esos indicadas anteriormente. Cuando se utiliza esta constante, el *SchemaID* argumento es necesario pasar el identificador GUID de la consulta de esquema para ejecutar. Si *QueryType* está establecido en **adSchemaProviderSpecific** pero *SchemaID* es no siempre, se producirá un error.  
  
 Los proveedores no son necesarios para admitir todas las consultas de esquema estándar de OLE DB. En concreto, solo **adSchemaTables**, **adSchemaColumns**, y **adSchemaProviderTypes** requeridos por la especificación de OLE DB. Sin embargo, el proveedor no es necesario para admitir la *criterios* restricciones enumeran anteriormente para esas consultas de esquema.  
  
> [!NOTE]
>  **Uso de servicios de datos remoto** el **OpenSchema** método no está disponible en un cliente [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
> [!NOTE]
>  En Visual Basic, las columnas que tienen un entero sin signo de cuatro bytes (DBTYPE UI4) en el **Recordset** devuelto desde el **OpenSchema** método en el **conexión** objeto no se puede se compara con otras variables. Para obtener más información acerca de los tipos de datos de OLE DB, vea [tipos de datos de OLE DB (OLE DB)](http://msdn.microsoft.com/en-us/6039292f-74e0-49b2-b133-17bc117ebf6a) y [Apéndice A: tipos de datos](http://msdn.microsoft.com/en-us/e3a0533a-2196-4eb0-a31e-92fe9556ada6) en el Microsoft OLE DB referencia del programador.  
  
> [!NOTE]
>  **Los usuarios de C o C++ Visual** si no usa cursores del lado cliente, recuperar "ORDINAL_POSITION" de un esquema de la columna de ADO devuelve una variante del tipo VT_R8 de MDAC 2.7 y MDAC 2.8, Windows Data Access Components (Windows DAC) 6.0, mientras que el tipo utilizado en MDAC 2.6 era VT_I4. Los programas escritos para MDAC 2.6 que solo buscan una variante devuelven de tipo que VT_I4 obtendría un cero para cada ordinal si se ejecutan en MDAC 2.7, MDAC 2.8 y 6.0 de Windows DAC sin ninguna modificación. Este cambio se realizó porque el tipo de datos OLE DB devuelve es DBTYPE_UI4 y en el tipo con signo VT_I4 no hay espacio suficiente para contener todos los valores posibles sin truncamiento posiblemente está produciendo y lo que causa una pérdida de datos.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo del método OpenSchema (VB)](../../../ado/reference/ado-api/openschema-method-example-vb.md)   
 [Ejemplo del método OpenSchema (VC ++)](../../../ado/reference/ado-api/openschema-method-example-vc.md)   
 [Open (método) (conexión de ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open (método) (registro de ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open (método) (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open (método) (Stream de ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Apéndice A: proveedores](../../../ado/guide/appendixes/appendix-a-providers.md)

