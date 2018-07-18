---
title: Introducción a los DiffGrams en SQLXML 4.0 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- annotations [SQLXML]
- DiffGrams [SQLXML], about DiffGrams
ms.assetid: 1902d67f-baf3-46e6-a36c-b24b5ba6f8ea
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7c897d32c8373301f62e83ef35f868a6435c3dcf
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38053823"
---
# <a name="introduction-to-diffgrams-in-sqlxml-40"></a>Introducción a los DiffGrams en SQLXML 4.0
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  En este tema se ofrece una breve introducción a los DiffGrams.  
  
## <a name="diffgram-format"></a>Formato de un DiffGram  
 Éste es el formato general de un DiffGram:  
  
```  
<?xml version="1.0"?>  
<diffgr:diffgram   
         xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"  
         xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1"  
         xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
   <DataInstance>  
      ...  
   </DataInstance>  
   [<diffgr:before>  
        ...  
   </diffgr:before>]  
  
   [<diffgr:errors>  
        ...  
   </diffgr:errors>]  
</diffgr:diffgram>  
```  
  
 El formato de un DiffGram consta de estos bloques:  
  
 **\<DataInstance >**  
 El nombre de este elemento, **DataInstance**, se utiliza con fines explicativos en esta documentación. Por ejemplo, si el DiffGram se generaron a partir de un conjunto de datos en .NET Framework, el valor de la **nombre** propiedad del conjunto de datos que se usará como el nombre de este elemento. Este bloque contiene todos los datos relevantes tras el cambio, y es posible que incluya incluso los datos que no se han modificado. La lógica de procesamiento de DiffGram omite los elementos de este bloque para el que el **diffgr: HasChanges** no se especifica el atributo.  
  
 **\<diffgr: antes de >**  
 Este bloque opcional contiene las instancias de registro (elementos) originales que deben actualizarse o eliminarse. Las tablas de la base de datos que se va a modificar (actualizar o eliminar) el DiffGram deben aparecer como elementos de nivel superior en el  **\<antes >** bloque.  
  
 **\<diffgr:errors>**  
 La lógica de procesamiento de DiffGram omite este bloque opcional.  
  
## <a name="diffgram-annotations"></a>Anotaciones de DiffGram  
 Estas anotaciones se definen en el espacio de nombres de DiffGram **"urn: schemas-microsoft-com-diffgram-01"**:  
  
 **id**  
 Este atributo se utiliza para emparejar los elementos de la  **\<antes >** y  **\<DataInstance >** bloques.  
  
 **hasChanges**  
 Para una inserción o una operación de actualización, el DiffGram debe especificar este atributo con el valor **insertado** o **modificado**. Si este atributo no está presente, el elemento correspondiente en el  **\<DataInstance >** omite el procesamiento se llevan a cabo lógica y no hay actualizaciones. Para obtener ejemplos funcionales, consulte [ejemplos de DiffGram &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md).  
  
 **parentID**  
 Este atributo se usa para especificar las relaciones entre los elementos primarios y secundarios del DiffGram. Este atributo solamente aparece en el \<antes > bloque. SQLXML lo utiliza cuando aplica actualizaciones. La relación entre elementos primarios y secundarios se utiliza para determinar el orden en que deben procesarse los elementos del DiffGram.  
  
## <a name="understanding-the-diffgram-processing-logic"></a>Descripción de la lógica de procesamiento de DiffGram  
 La lógica de procesamiento de DiffGram utiliza ciertas reglas para determinar si una operación es una operación de inserción, actualización o eliminación. Estas reglas se describen en la siguiente tabla.  
  
|Operación|Descripción|  
|---------------|-----------------|  
|Insert|Un DiffGram indica una operación de inserción cuando aparece un elemento en el  **\<DataInstance >** bloque pero no en las correspondientes  **\<antes >** bloque y el **diffgr: HasChanges** se especifica el atributo (**diffgr: HasChanges = insertar**) en el elemento. En este caso, el DiffGram inserta la instancia de registro que se especifica en el  **\<DataInstance >** bloque en la base de datos.<br /><br /> Si el **diffgr: HasChanges** atributo no se especifica, se omite el elemento por la lógica de procesamiento y se realiza ninguna inserción. Para obtener ejemplos funcionales, consulte [ejemplos de DiffGram &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md).|  
|Update|El DiffGram indica una operación de actualización cuando hay un elemento en el \<antes > bloque para el que hay un elemento correspondiente en el  **\<DataInstance >** bloque (es decir, ambos elementos tienen un **diffgr: ID** atributo con el mismo valor) y la **diffgr: HasChanges** se especifica el atributo con el valor **modificado** en el elemento en el  **\<DataInstance >** bloque.<br /><br /> Si el **diffgr: HasChanges** no se especifica el atributo en el elemento en el  **\<DataInstance >** bloque, se devuelve un error por la lógica de procesamiento. Para obtener ejemplos funcionales, consulte [ejemplos de DiffGram &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md).<br /><br /> Si **diffgr: parentId** se especifica en el  **\<antes >** bloquear la relación de elementos primarios y secundarios de elementos que se especifican mediante **parentID** se usan en determinar el orden en que se actualizan registros.|  
|DELETE|Un DiffGram indica una operación de eliminación cuando un elemento aparece en el  **\<antes >** bloque pero no en las correspondientes  **\<DataInstance >** bloque. En este caso, el DiffGram elimina la instancia de registro que se especifica en el  **\<antes >** bloque desde la base de datos. Para obtener ejemplos funcionales, consulte [ejemplos de DiffGram &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md).<br /><br /> Si **diffgr: parentId** se especifica en el  **\<antes >** bloquear la relación de elementos primarios y secundarios de elementos que se especifican mediante **parentID** se usan en determinar el orden en el que se eliminan registros.|  
  
> [!NOTE]  
>  No pueden pasarse parámetros a los DiffGrams.  
  
  
