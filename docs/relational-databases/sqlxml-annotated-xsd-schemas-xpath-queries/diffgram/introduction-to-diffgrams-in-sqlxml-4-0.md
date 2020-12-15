---
title: Introducción a los DiffGrams en SQLXML 4.0
description: Obtenga información sobre el formato, las anotaciones y la lógica de procesamiento de DiffGrams en SQLXML 4,0.
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotations [SQLXML]
- DiffGrams [SQLXML], about DiffGrams
ms.assetid: 1902d67f-baf3-46e6-a36c-b24b5ba6f8ea
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 66a58dfb19cf8f53f775bac663d5ba3e6147711b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97414997"
---
# <a name="introduction-to-diffgrams-in-sqlxml-40"></a>Introducción a los DiffGrams en SQLXML 4.0
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
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
  
 **\<DataInstance>**  
 El nombre de este elemento, **instanceof**, se utiliza con fines explicativos en esta documentación. Por ejemplo, si el DiffGram se generó a partir de un conjunto de elementos en el .NET Framework, el valor de la propiedad **Name** del conjunto de elementos se utilizaría como el nombre de este elemento. Este bloque contiene todos los datos relevantes tras el cambio, y es posible que incluya incluso los datos que no se han modificado. La lógica de procesamiento de DiffGram omite los elementos de este bloque para los que no se especifica el atributo **diffgr: hasChanges** .  
  
 **\<diffgr:before>**  
 Este bloque opcional contiene las instancias de registro (elementos) originales que deben actualizarse o eliminarse. Todas las tablas de base de datos que se van a modificar (actualizar o eliminar) por DiffGram deben aparecer como elementos de nivel superior en el **\<before>** bloque.  
  
 **\<diffgr:errors>**  
 La lógica de procesamiento de DiffGram omite este bloque opcional.  
  
## <a name="diffgram-annotations"></a>Anotaciones de DiffGram  
 Estas anotaciones se definen en el espacio de nombres de DiffGram **"urn: schemas-microsoft-com: XML-DiffGram-01"**:  
  
 **id**  
 Este atributo se usa para emparejar los elementos de los **\<before>** **\<DataInstance>** bloques y.  
  
 **hasChanges**  
 En el caso de una operación de inserción o de actualización, el DiffGram debe especificar este atributo con el valor **insertado** o **modificado**. Si este atributo no está presente, la lógica de procesamiento omite el elemento correspondiente de en **\<DataInstance>** y no se realiza ninguna actualización. Para obtener ejemplos de trabajo, vea los [ejemplos de DiffGram &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md).  
  
 **parentID**  
 Este atributo se usa para especificar las relaciones entre los elementos primarios y secundarios del DiffGram. Este atributo solo aparece en el \<before> bloque. SQLXML lo utiliza cuando aplica actualizaciones. La relación entre elementos primarios y secundarios se utiliza para determinar el orden en que deben procesarse los elementos del DiffGram.  
  
## <a name="understanding-the-diffgram-processing-logic"></a>Descripción de la lógica de procesamiento de DiffGram  
 La lógica de procesamiento de DiffGram utiliza ciertas reglas para determinar si una operación es una operación de inserción, actualización o eliminación. Estas reglas se describen en la siguiente tabla.  
  
|Operación|Descripción|  
|---------------|-----------------|  
|Insertar|Un DiffGram indica una operación de inserción cuando aparece un elemento en el **\<DataInstance>** bloque, pero no en el **\<before>** bloque correspondiente, y se especifica el atributo **diffgr: HasChanges** (**diffgr: HasChanges = Inserted**) en el elemento. En este caso, el DiffGram inserta la instancia de registro especificada en el bloque en **\<DataInstance>** la base de datos.<br /><br /> Si no se especifica el atributo **diffgr: hasChanges** , la lógica de procesamiento omite el elemento y no se realiza ninguna inserción. Para obtener ejemplos de trabajo, vea los [ejemplos de DiffGram &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md).|  
|Actualizar|El DiffGram indica una operación de actualización cuando hay un elemento en el \<before> bloque para el que hay un elemento correspondiente en el **\<DataInstance>** bloque (es decir, ambos elementos tienen un atributo **diffgr: ID** con el mismo valor) y el atributo **diffgr: hasChanges** se especifica con el valor **modificado** en el elemento del **\<DataInstance>** bloque.<br /><br /> Si el atributo **diffgr: hasChanges** no se especifica en el elemento del **\<DataInstance>** bloque, la lógica de procesamiento devuelve un error. Para obtener ejemplos de trabajo, vea los [ejemplos de DiffGram &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md).<br /><br /> Si se especifica **diffgr: parentId** en el **\<before>** bloque, la relación de elementos primarios y secundarios que especifica el **parentId** se usa para determinar el orden en que se actualizan los registros.|  
|Eliminar|Un DiffGram indica una operación de eliminación cuando un elemento aparece en el **\<before>** bloque, pero no en el **\<DataInstance>** bloque correspondiente. En este caso, el DiffGram elimina la instancia de registro especificada en el **\<before>** bloque de la base de datos. Para obtener ejemplos de trabajo, vea los [ejemplos de DiffGram &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md).<br /><br /> Si se especifica **diffgr: parentId** en el **\<before>** bloque, la relación de elementos primarios y secundarios que especifica el **parentId** se usa para determinar el orden en el que se eliminan los registros.|  
  
> [!NOTE]  
>  No pueden pasarse parámetros a los DiffGrams.  
  
  
