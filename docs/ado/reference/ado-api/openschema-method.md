---
title: Método OpenSchema | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::OpenSchema
- Connection15::raw_OpenSchema
helpviewer_keywords:
- OpenSchema method [ADO]
ms.assetid: 850cf3ce-f18f-4e7c-8597-96c1dc504866
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b2080145e00c658288f9d34e3fa42ed335e0c1d9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931862"
---
# <a name="openschema-method"></a>Método OpenSchema
Obtiene información de esquema de base de datos del proveedor.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Set recordset = connection.OpenSchema(QueryType, Criteria, SchemaID)  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto que contiene información de esquema. El **Recordset** se abrirá como un cursor estático de solo lectura. El *QueryType* determina qué columnas aparecen en la **Recordset**.  
  
#### <a name="parameters"></a>Parámetros  
 *QueryType*  
 Cualquier [SchemaEnum](../../../ado/reference/ado-api/schemaenum.md) valor que representa el tipo de consulta de esquema que se ejecuta.  
  
 *Criterios*  
 Opcional. Una matriz de restricciones de consulta para cada *QueryType* opción, como se muestra en [SchemaEnum](../../../ado/reference/ado-api/schemaenum.md).  
  
 *SchemaID*  
 El GUID para una consulta de esquema del proveedor no definido por la especificación de OLE DB. Este parámetro es obligatorio si *QueryType* está establecido en **adSchemaProviderSpecific**; en caso contrario, no se utiliza.  
  
## <a name="remarks"></a>Comentarios  
 El **OpenSchema** método devuelve información autodescriptiva sobre el origen de datos, por ejemplo, ¿cuáles son las tablas del origen de datos, las columnas en las tablas, y admiten los tipos de datos.  
  
 El *QueryType* argumento es un GUID que indica las columnas devueltas (esquemas). La especificación OLE DB tiene una lista completa de los esquemas.  
  
 El *criterios* argumento limita los resultados de una consulta de esquema. *Criterios* especifica una matriz de valores que se debe producir en un subconjunto de columnas, denominadas columnas de restricción, en el cuadro correspondiente **Recordset**.  
  
 La constante **adSchemaProviderSpecific** se usa para la *QueryType* argumento si el proveedor define sus propias consultas de esquema no estándar fuera de los mencionados anteriormente. Cuando se usa esta constante, el *SchemaID* argumento es necesario pasar el identificador GUID de la consulta de esquema para ejecutar. Si *QueryType* está establecido en **adSchemaProviderSpecific** pero *SchemaID* es no siempre, se producirá un error.  
  
 Los proveedores no son necesarios para admitir todas las consultas de esquema estándar de OLE DB. En concreto, solo **adSchemaTables**, **adSchemaColumns**, y **adSchemaProviderTypes** requeridos por la especificación OLE DB. Sin embargo, el proveedor no es necesario para admitir la *criterios* restricciones enumeran anteriormente para las consultas de esquema.  
  
> [!NOTE]
>  **Uso del servicio de datos remoto** el **OpenSchema** método no está disponible en un cliente [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
> [!NOTE]
>  En Visual Basic, las columnas que tienen un entero sin signo de cuatro bytes (DBTYPE UI4) en el **Recordset** devuelto desde el **OpenSchema** método en el **conexión** no objeto se compara con otras variables. Para obtener más información acerca de los tipos de datos OLE DB, consulte [tipos de datos de OLE DB (OLE DB)](https://msdn.microsoft.com/6039292f-74e0-49b2-b133-17bc117ebf6a) y [Apéndice A: Tipos de datos](https://msdn.microsoft.com/e3a0533a-2196-4eb0-a31e-92fe9556ada6) en referencia del programador de OLE DB de Microsoft.  
  
> [!NOTE]
>  **Visual C /C++ usuarios** al no utilizar cursores de cliente, recuperando "ORDINAL_POSITION" de un esquema de columna en ADO devuelve una variante de tipo VT_R8 en Windows Data Access Components (Windows DAC) 6.0, mientras que el tipo utilizado, MDAC 2.8 y MDAC 2.7 en la versión 2.6 de MDAC era VT_I4. Los programas escritos para MDAC 2.6 que solo buscan una variante devuelven de tipo que VT_I4 obtendría un cero por cada ordinal si se ejecutan en MDAC 2.7, MDAC 2.8 y 6.0 de Windows DAC sin ninguna modificación. Este cambio se realizó porque el tipo de datos OLE DB devuelve es DBTYPE_UI4 y, en el tipo con signo de VT_I4 no hay espacio suficiente para contener todos los valores posibles sin truncamiento, posiblemente, que se producen y lo que provocaría una pérdida de datos.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo del método OpenSchema (VB)](../../../ado/reference/ado-api/openschema-method-example-vb.md)   
 [Ejemplo del método OpenSchema (VC ++)](../../../ado/reference/ado-api/openschema-method-example-vc.md)   
 [Método Open (conexión de ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Método Open (Record ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Método Open (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Método Open (Stream de ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Apéndice A: proveedores](../../../ado/guide/appendixes/appendix-a-providers.md)
