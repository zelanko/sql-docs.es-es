---
title: Compatibilidad del proveedor con ADOX (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADOX provider support [ADO]
ms.assetid: 64234ce5-dc46-4c8a-a316-61956b6b9abb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2b07f4563d54254310c08c8c132d0729b8ccdc6b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923216"
---
# <a name="provider-support-for-adox-ado"></a>Compatibilidad del proveedor con ADOX (ADO)
Algunas características de ADOX no son compatibles, dependiendo de su proveedor de datos OLE DB. ADOX es totalmente compatible con la [proveedor OLE DB para Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md). Las características no admitidas con el [proveedor Microsoft OLE DB para SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md), [proveedor Microsoft OLE DB para ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md), o el [proveedor Microsoft OLE DB para Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md) son se muestran en las tablas siguientes. ADOX no es compatible con cualquier otro proveedor Microsoft OLE DB.  
  
## <a name="microsoft-ole-db-provider-for-sql-server"></a>Proveedor Microsoft OLE DB para SQL Server  
  
|Objeto o colección|Restricción de uso|  
|--------------------------|-----------------------|  
|**Las tablas** colección|Las propiedades son de lectura/escritura antes de la creación de objetos y de solo lectura cuando se hace referencia a un objeto existente.|  
|**Vistas** colección|**Vistas** no se admite.|  
|**Procedimientos** colección|El **Append** y **eliminar** métodos no son compatibles.|  
|**Procedimiento** objeto|El **comando** no se admite la propiedad.|  
|**Las claves** colección|El **Append** y **eliminar** métodos no son compatibles.|  
|**Los usuarios** colección|**Los usuarios** no se admite.|  
|**Grupos** colección|**Grupos** no se admite.|  
  
## <a name="microsoft-ole-db-provider-for-odbc"></a>Proveedor Microsoft OLE DB para ODBC  
  
|Objeto o colección|Restricción de uso|  
|--------------------------|-----------------------|  
|**Catálogo** objeto|El **crear** no se admite el método.|  
|**Las tablas** colección|El **Append** y **eliminar** métodos no son compatibles. Las propiedades son de lectura/escritura antes de la creación de objetos y de solo lectura cuando se hace referencia a un objeto existente.|  
|**Procedimientos** colección|El **Append** y **eliminar** métodos no son compatibles.|  
|**Procedimiento** objeto|El **comando** no se admite la propiedad.|  
|**Los índices** colección|El **Append** y **eliminar** métodos no son compatibles.|  
|**Las claves** colección|El **Append** y **eliminar** métodos no son compatibles.|  
|**Los usuarios** colección|**Los usuarios** no se admite.|  
|**Grupos** colección|**Grupos** no se admite.|  
  
## <a name="microsoft-ole-db-provider-for-oracle"></a>proveedor Microsoft OLE DB para Oracle  
  
|Objeto o colección|Restricción de uso|  
|--------------------------|-----------------------|  
|**Catálogo** objeto|El **crear** no se admite el método.|  
|**Las tablas** colección|El **Append** y **eliminar** métodos no son compatibles. Las propiedades son de lectura/escritura antes de la creación de objetos y de solo lectura cuando se hace referencia a un objeto existente.|  
|**Vistas** colección|El **Append** y **eliminar** métodos no son compatibles.|  
|**Vista** objeto|El **comando** no se admite la propiedad.|  
|**Procedimientos** objeto|El **Append** y **eliminar** métodos no son compatibles.|  
|**Procedimiento** objeto|El **comando** no se admite la propiedad.|  
|**Los índices** colección|El **Append** y **eliminar** métodos no son compatibles.|  
|**Las claves** colección|El **Append** y **eliminar** métodos no son compatibles.|  
|**Los usuarios** colección|**Los usuarios** no se admite.|  
|**Grupos** colección|**Grupos** no se admite.|
